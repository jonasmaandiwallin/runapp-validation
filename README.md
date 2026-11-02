<!--
public-header:
  originator: "Jonas Maandi Wallin"
  editor: "Jonas Maandi Wallin"
  contact: "https://www.linkedin.com/in/jonasmaandiwallin"
  license: "CC-BY-4.0"
  repository: "https://github.com/jonasmaandiwallin/runapp-validation"
  path: "README.md"
-->
# Runapp Validation: Building a System That Validates a System

*How Runapp measures its own training plans before a runner follows them — with a simulator, a metric of its own, and the caveats that come with both.*

## 1 — The question

How do you know a training plan is good before anyone has run it?

You cannot field-test 153 training plans on real runners. The combinatorial space — seven race distances, multiple frequencies, varying fitness levels, time constraints — makes controlled trials impossible at this scale. And waiting for longitudinal outcome data means waiting years for answers to questions you can answer now.

So Runapp built an instrument: a simulator that runs a population of virtual runners through any plan, and a metric that turns what happens to them into one comparable number. This repository documents both — what they are, what they show, and where they stop.

## 2 — What it is

The simulator models three independent processes: **adaptation** (how fitness responds to training load, based on the Banister/Busso impulse-response model), **injury** (cumulative injury probability, modeled as a survival process with dose-dependent hazard), and **compliance** (how faithfully a runner executes the prescribed plan — sampled per runner from distributions whose *direction* is supported by adherence research but whose *magnitudes* are engineering defaults, not yet measured against real Runapp users). These processes combine through a Monte Carlo framework: 1,000 synthetic runners, each with individually sampled physiological parameters, are run through a training plan. The population-level outcome — mean fitness gain, mean injury probability, and the spread of both — characterizes the plan.

QDOT (Quality-Adjusted Training Dose) collapses that outcome into one signal: fitness gain adjusted for injury cost, per unit of time. The idea is borrowed from the Sharpe ratio in finance — return adjusted for risk. QDOT is normalized so that 1.0 equals the median plan in the current evaluation epoch.

The simulator's physiological models are grounded in published exercise science. Every parameter either traces to a specific study or is explicitly marked as an engineering default awaiting empirical calibration. The formal mathematical system — all parameters, calibration procedures, and the computational chain — is documented in the Mathematical Specification, available under NDA.

## 3 — The ideas

**Simulate before you validate.** A trial with fifteen to thirty runners per arm cannot see the differences that matter between plans, and no trial can compare more than a handful of plans at once. A simulator can put every plan on the same physiological model, with the same assumptions, and change one variable at a time. It does not replace empirical testing; it decides which empirical tests are worth running. → [The Runapp Training Simulator](whitepapers/simulator.md)

**Measure a plan by its return per unit of risk.** One-dimensional load metrics measure how much training a plan contains, not how much useful adaptation it produces. QDOT separates what coaching conflates: how much fitness a plan builds, how much injury risk it imposes, and the rate of gain per unit of risk — computed over a population, not a single idealized athlete, so the spread is part of the measurement. → [QDOT: A Sharpe Ratio for Training Plans](whitepapers/qdot.md)

**The simulator is a design partner, not only a judge.** When Runapp first ran its plans across a range of fitness levels, plans designed for mid-range runners systematically over-stressed lower-fitness runners and under-challenged higher-fitness runners; the fix was a structural redesign with session compositions per fitness tier. When it modeled runners with three sessions a week capped at 60 minutes, it found that naive truncation cut exactly the quality sessions that produce adaptation; the fix was an architecture that keeps quality sessions intact and lets volume absorb the constraint. Neither insight came from coaching intuition or literature review. They came from measuring plans against synthetic populations and finding the gaps.

## 4 — What is measured

All figures are from measurement epoch v0.4 and are documented, with their tables, in the two white papers.

- **The field.** 153 protocols across seven race distances — 148 from 18 sources, plus five diagnostic and reference runs — run in three steps: full adherence, a matched weekly budget for every platform, and realistic adherence. Among consumer plans, Runapp plans rank first at each of the four tabulated distances — 5K, 10K, half marathon and marathon — in all three steps. The arms of the six intervention studies are run but not ranked as consumer plans; with them included, one cell changes: under the matched budget at 10K, a polarized study arm scores above the leading Runapp plan. → QDOT white paper, section 6.
- **The constraint finding.** Under the matched budget, external protocols approach parity with Runapp at some distances — evidence of design insights Runapp's optimization has not yet captured. Under realistic adherence, app-based platforms pull ahead of book-based plans, because the sessions most likely to be skipped are the ones that contribute most to gain. → QDOT white paper, section 6.
- **External validation.** Sixteen protocol arms from six published intervention studies were simulated and compared against each study's measured outcome. Five of six rankings match; one is marginal, in a study that reports no test between its two arms — only that one arm improved significantly and the other did not. The panel validates ranking, not absolute magnitudes. → QDOT white paper, section 5.
- **The mixed field.** A virtual 10K with eleven training approaches, one thousand runners each and confirmed at ten thousand: structured plans improve their runners, unstructured training does not, and every app-delivered plan outperforms every book-based plan. → Simulator white paper, section 5.2.
- **Robustness.** At full execution, a 2×2 decomposition puts seven-eighths of Runapp's advantage in plan design and one-eighth in execution support; the ranking holds across five fitness levels, VDOT 35 to 55. → Simulator white paper, sections 5.5 and 5.6.

The detailed simulation data — per-distance tables, consumer scenarios, the fitness-level sweep and percentile spreads — is in the measurement reports under NDA.

## 5 — Why this is unusual

This repository publishes both how Runapp measures its plans and the strongest case against the results. That case is the optimization asymmetry.

Runapp's plans are optimized against the simulator. They were designed using simulator feedback, iterated through simulator measurements, and calibrated to perform well under the simulator's physiological model. Competitor plans were not: each was designed with its own methodology, and none was designed to optimize QDOT. The asymmetry is real, it is inherent, and it cannot be eliminated through methodology — only through external validation.

What can be said honestly:

- **Within the simulator's model of physiology, Runapp plans produce better outcomes.** The model is grounded in published exercise science, its assumptions are stated explicitly and are falsifiable, and the results are reproducible.
- **The asymmetry is a known limitation, not a hidden one.** It is stated in every white paper and with every comparative result. No claim is made that simulator superiority equals real-world superiority.
- **The simulator's value is comparative, not absolute.** It reveals relative differences between plans that no other methodology can measure at this scale.

This is the distinction Popper (1959) drew between a scientific model and a marketing assertion: the instrument's claims are falsifiable, and the path to falsify them is specified.

## 6 — Limitations

Every simplification carries consequences, and those consequences are tracked.

- **Adaptation model.** Each training session is treated as a single zone and duration. Within-session structure — intervals, repeats, warm-up and cool-down — is not represented.
- **Injury model.** The hazard model accounts for load spikes, cumulative volume and recovery spacing, and is calibrated against a published cohort's cumulative-incidence curve. Individual risk factors beyond aggregate modifiers (experience, previous injury) are not represented.
- **Compliance model.** The direction of the class-level differences — app-delivered plans are followed more reliably than book-based plans — has literature support; the magnitude does not. If the gap were zero, the adherence-adjusted results would collapse to the constraint-equalized results.
- **The escalation state machine is not modeled.** Runapp's protection mechanism, described in [runapp-platform](https://github.com/jonasmaandiwallin/runapp-platform), does not appear in the simulator. A narrower proxy — a load-ratio substitution rule — captures one of its effects. The proxy's effect on QDOT is not measured at the current instrument version. The simulator evaluates what a plan prescribes, not how the plan responds to signals during execution.
- **No prospective validation.** All results are simulated. Whether runners on high-QDOT plans get faster, adhere better and get injured less has not been tested.

The simulator and QDOT each have a caveat register under NDA, where every known limitation is classified by severity and tractability. Caveats are added when discovered, resolved as the model improves, and never silently removed.

## 7 — What comes next

Building the instrument is Stage 1. Optimizing Runapp's plans against it is Stage 2. Proving that the instrument predicts real-world outcomes is Stage 3. This repository describes Stages 1 and 2; Stage 3 is ahead. Prospective field studies, starting with Runapp users and expanding to controlled comparisons, will either confirm or challenge the simulator's rankings. The instrument and its documentation exist to make that validation possible — they are the infrastructure for a claim that has not yet been made.

(These are the stages of the instrument programme — not the three steps of the measurement experiment in the QDOT white paper, which are conditions within Stage 2.)

## 8 — Map

**White papers**
- [The Runapp Training Simulator](whitepapers/simulator.md) — the evaluation framework: model components, validation, the measurement campaigns and the mixed field.
- [QDOT: A Sharpe Ratio for Training Plans](whitepapers/qdot.md) — the quality instrument: what it measures, the three-step experiment, the external panel and the three public caveats.

**Reference**
- [Evidence Register: Simulator](reference/simulator-evidence-register.md) and [Evidence Register: QDOT](reference/qdot-evidence-register.md) — the literature behind each, every study tagged Foundation, Parameter support or Validation. The registers contain no parameter values and no mappings between studies and parameters.

**Under NDA** — shown in [nda/](nda/) as title and abstract only
- Mathematical Specification — the unified formal definition of the simulator and QDOT.
- QDOT Technical Specification — the three-step design, all distance tables, panel results, optimization history and epoch provenance.
- QDOT Computational Chain — a formula-by-formula trace through the calculation, verified against source code.
- QDOT Caveat Register and Simulator Caveats — every known limitation, classified by severity and tractability.
- Simulation Data — the measurement reports: the flagship cohort, consumer scenarios, the fitness-level sweep and the mixed field with named platforms.

**The other parts**
- What Runapp is — the training engine, the escalation mechanism, adaptation and motivation: [runapp-platform](https://github.com/jonasmaandiwallin/runapp-platform).
- How it was built — Governed Agentic Engineering: [governed-agentic-engineering](https://github.com/jonasmaandiwallin/governed-agentic-engineering).

## License and contact

Text in this repository is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/), attributed to Jonas Maandi Wallin. The full text is in `LICENSE`.

Each document in `whitepapers/`, `reference/` and `nda/` carries its own frontmatter with an `ai_disclosure` block: AI agents drafted the text and ran the measurements under the editor's direction, and the block says which roles were done and how each was checked. The editor takes full editorial responsibility for what is published.

Contact: [Jonas Maandi Wallin on LinkedIn](https://www.linkedin.com/in/jonasmaandiwallin).
