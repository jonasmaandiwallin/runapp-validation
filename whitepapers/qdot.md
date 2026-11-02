---
title: "QDOT: A Sharpe Ratio for Training Plans"
type: reference
status: draft
version: "0.7"
date: "2026-11-02"
author: "Tooling & Architecture"
audience: "External — no IP disclosure. Readable without NDA."
reading_order: 3
package: validation
release: public
qdot_version: "0.4"
qdot_epoch: "v0.4"
framework:
  name: "Governed Agentic Engineering (GAE)"
  originator: "Jonas Maandi Wallin"
editor: "Jonas Maandi Wallin"
contact: "https://www.linkedin.com/in/jonasmaandiwallin"
author_llm:
  - model: null
    model_id: null
    roles: [drafting, technical-analysis]
    source: not-established
  - model: "Claude Opus 5.5"
    model_id: "claude-opus-5-5"
    roles: [editing, fact-check]
    source: platform
  - model: "Claude Fable 5.1"
    model_id: "claude-fable-5-1"
    roles: [review]
    source: handoff
ai_disclosure:
  - role: drafting
    status: complete
    scope: "Text and structure of versions up to 0.6 (2026-09-03), written by the Tooling & Architecture agent. The model of those sessions is not established: no handoff of that date names it."
    evidence: "The document's own text; each figure names its epoch (v0.4) and its source study or step."
    reason: null
  - role: technical-analysis
    status: complete
    scope: "Panel and three-step figures read from simulator cohort runs at epoch v0.4."
    evidence: "Sections 5 and 6 name the studies, the steps and the epoch behind each figure."
    reason: null
  - role: editing
    status: complete
    scope: "Version 0.7: sections numbered and reordered to the white-paper template (problem, mechanism, measurements, positioning, limitations, outlook, map); the closing map rewritten for the public repository; one paragraph added to section 6 stating that the study arms are run but not ranked, and the one cell where that changes the leader; the loss ranges in section 6 restated from a recomputation (73–97% where 74–96% stood) with the plans that fall below zero named; the protocol count restated (148 from 18 sources); the Esteve-Lanao sentence in section 1 and the panel's outcome measures in section 5 brought in line with the study and the evidence registry. After review: the loss ranges in section 6 scoped to the four tabulated distances; the Helgerud and Vesterinen study rankings in section 5 restated to what the studies report; the near-tie footnote restated as a standard-error comparison; the sensitivity sentence in section 9 scoped to consumer plans and the control; the Stöggl threshold-arm sentence in section 5 restated after the study's table was read."
    evidence: "The diff against version 0.6."
    reason: null
  - role: fact-check
    status: complete
    scope: "Every figure in sections 1, 5, 6 and 9 recomputed from the epoch v0.4 cohort runs in the simulation database; the panel's outcome measures and study rankings read against the evidence-registry entries of the six studies; claims the figures or sources did not bear were corrected. The threshold arm's −4.1% in section 5 read against the study's Table 2 (−4.1 ± 6.7%, not significant within the group) and the sentence restated accordingly."
    evidence: "The release fact-check report of 2026-11-02, one row per claim with its source, whether that source is primary, and the outcome."
    reason: null
  - role: review
    status: complete
    scope: "Adversarial review in two rounds against five classes: a figure without a source, a claim beyond its figures or source, NDA content in public text, two files of the release contradicting each other, and frontmatter."
    evidence: "Round 1 (2026-11-02): 5 blocking and 4 advisory findings, all corrected in this version. Round 2 (2026-11-02): no blocking or advisory findings."
    reason: null
license: "CC-BY-4.0"
repository: "https://github.com/jonasmaandiwallin/runapp-validation"
path: "whitepapers/qdot.md"
---

# QDOT: A Sharpe Ratio for Training Plans

*Quality-Adjusted Training Dose*

> *This document describes the intellectual framework and validation methodology behind QDOT. The formal mathematical system — including all parameter values, calibration procedures, and computational chain — is documented in the Mathematical Specification, available under NDA to research partners, investors, and potential collaborators. The training-plan optimization engine is proprietary to Jonas Maandi Wallin and is not disclosed.*

---

## 1 — The running industry has a measurement problem

Every running app will tell you it has "the best training plan." None of them can tell you what that means — because the industry's standard metrics were never designed to answer the question that matters most: given two training plans for the same race, which one will produce more useful adaptation for the cost and risk it imposes?

One-dimensional load metrics like TRIMP, TSS, and "Load" measure how much training a plan contains, not how much useful adaptation it produces. They treat 100 points of easy aerobic running as interchangeable with 100 points of threshold intervals. When Esteve-Lanao et al. (2007) tested this assumption in a controlled trial — two groups, matched TRIMP load, different intensity distributions — the group that did four-fifths of its training at low intensity improved its race time more than the group that did a quarter of it at moderate intensity. A one-dimensional load metric scores the two plans as equal; it cannot tell them apart.

QDOT exists because this question needs a new instrument. It measures risk-adjusted training efficiency: not how much training a plan prescribes, but how much useful adaptation it produces relative to the injury cost it imposes. This white paper describes why the question matters, what the instrument looks like, and what it shows when applied to 153 protocols — 148 of them from 18 sources — across seven race distances.

---

## 2 — Beyond one dimension

To make the instrument reflect reality, we abandoned the single-load-axis assumption. Different intensity zones produce different adaptive responses with different time dynamics and different saturation characteristics. Aerobic base training builds durability that tolerates massive volume. Threshold training suffers from rapid diminishing returns — it quickly generates fatigue while its contribution to race capacity hits a ceiling. This is the mathematical representation of "the black hole": the moderate-intensity training that wears runners out without making them faster.

We are not alone in this direction. In February 2026, Kontro et al. published a three-dimensional impulse-response model (PLoS One 21(2): e0341721) that decomposes training load into energy-system-specific inputs, each with its own adaptation dynamics. Their rationale mirrors the conceptual foundation behind QDOT: adaptation tends to occur in the systems actually stressed, and a single load axis cannot represent that specificity. They demonstrate that programs with identical accumulated load can produce different performance peaks when temporal distribution differs, and that dose-response characteristics for different energy systems differ in both magnitude and time course.

Their model and ours address different layers of the same problem. Kontro et al. ask a modeling question: how should multidimensional training stress be represented? QDOT asks an optimization question: once adaptation and risk are represented explicitly, which training plan should we actually choose? Both share the premise that adaptation should not be modeled as a universal, linear response to training dose. And both are transparent about what remains unproven — the assumption of system-specific adaptation has not yet been subject to strict experimental testing.

---

## 3 — The Sharpe insight

In 1966, William Sharpe proposed a deceptively simple idea for financial markets: don't measure returns in isolation — measure them relative to the risk taken to achieve them. The Sharpe ratio became the standard way to compare investment strategies on equal footing.

Training plans have the same structure. A plan produces a return (fitness gain) and carries a risk (injury probability). A high-volume plan might produce impressive gains, but if it injures a large share of the runners who follow it, those gains come at an unacceptable cost. QDOT combines modeled adaptation, time efficiency, and injury risk into a single risk-adjusted quality signal. The formal mathematical system — nonlinear dose-response functions, temporal adaptation dynamics, cumulative risk modeling, and the explicit tradeoff between gain and risk — is documented in the Mathematical Specification.

Two design choices define what QDOT measures. First, it rewards *weekly efficiency* — a shorter plan delivering similar per-session quality scores higher than a longer plan with more total gain. The scale is normalized so that 1.0 equals the median plan. Second, the risk component applies a nonlinear discount whose strength is governed by an explicit risk-preference parameter. This parameter is normative: it expresses a preference about how to value adaptation relative to injury risk. Different values produce different leaderboard orderings.

Sharpe didn't make fund managers less ambitious — he gave them a language for *disciplined* ambition. The best-performing funds aren't the ones that avoid risk; they're the ones that take precisely the right amount. QDOT does the same for training. Runapp is offensive by default — not reckless, but aggressive within a boundary: the escalation gates, recovery enforcement, and load-spike detection in the training engine exist specifically to *enable* that aggressive stance, and QDOT is the instrument that measures whether the resulting plans pay for their risk. Without a risk-adjusted metric, an offensive engine has no way to tell disciplined ambition from recklessness.

---

## 4 — Three dimensions of training quality

QDOT rests on three dimensions. What follows is the reasoning behind each — what the instrument measures and why, without the implementation detail that lives in the Mathematical Specification.

**Adaptation.** The model uses a fitness-fatigue framework where each training session simultaneously builds fitness (slowly) and generates fatigue (quickly). Two features distinguish it from conventional load models: each intensity domain has its own nonlinear saturation behavior, so additional exposure does not translate into proportionally greater adaptation; and a maintenance threshold ensures that plans must produce net positive adaptation to receive QDOT credit. Plans that merely maintain fitness — or produce less than maintenance-level running — receive zero or genuinely negative gain.

**Cost.** The injury model accounts for three mechanistically distinct risk dimensions: acute load spikes (the "too much too soon" signal), cumulative volume, and recovery spacing. These reflect the epidemiological finding that sudden load increases are the strongest predictor of running injury, with cumulative exposure and recovery quality as secondary and tertiary contributors. Injury risk accumulates nonlinearly — each increment of training exposure does not carry the same marginal cost.

**Quality.** Adaptation and cost combine into a risk-adjusted measure of training efficiency. The result is a consistent framework for comparing training prescriptions under explicit assumptions, not a prediction of individual race performance. Cohort values are means over 1,000 virtual runners per plan.

*The formal parameterization, calibration history, and sensitivity analysis are documented in the Mathematical Specification and Technical Specification under NDA.*

---

## 5 — External validation: the panel

To stress-test external validity, we simulated sixteen protocol arms from six published intervention studies and compared QDOT rankings against each study's own measured outcome — the change in VO₂max or VO₂peak in most, race or time-trial performance in others. The studies span polarized, threshold, high-intensity interval, and mixed-intensity designs: Stöggl & Sperlich 2014 (4 arms), Helgerud et al. 2007 (4 arms), Esteve-Lanao et al. 2007 (2 arms), Muñoz et al. 2014 (2 arms), Carnes & Mahoney 2019 (2 arms), and Vesterinen et al. 2016 (2 arms). Where VO₂max or VO₂peak was measured, the changes ranged from −4.1% to +11.7%.

For each multi-arm study, we asked: does the QDOT ranking match the study's measured ranking? The study ranking orders the arms by their measured change; arms that did not change significantly are written as an unordered set in braces. Five of six comparisons pass. Vesterinen is marginal: the study reports no test between its two arms, only that the high-intensity arm improved significantly within its group and the high-volume arm did not, so QDOT's order agrees with the direction of the results but not with a tested difference. In earlier versions the Stöggl threshold arm was the one directional mismatch: the simulation gave it a positive gain, while its measured VO₂peak fell by 4.1% on average — a change that was not significant within the group, but significantly smaller than in the polarized and interval arms. With the maintenance threshold, the simulation now gives it near-zero, slightly negative gain.

| Study | Arms (QDOT) | Study ranking | Verdict |
|---|---|---|---|
| Stöggl 2014 | POL(1.41) > HIIT(0.97) > HVT(0.14) > THR(−0.03) | POL > HIIT > {THR, HVT} | ✓ PASS |
| Helgerud 2007 | 4×4(0.41) > 15/15(0.38) > LSD(−0.28) > LT(−1.17) | 4×4 > 15/15 > {LSD, LT} | ✓ PASS |
| Esteve-Lanao 2007 | Z1(0.37) > Z2(0.17) | Z1 > Z2 | ✓ PASS |
| Muñoz 2014 | POL(0.80) > THR(0.16) | POL > THR | ✓ PASS |
| Carnes 2019 | POL(0.85) > CFE(0.61) | POL > CFE | ✓ PASS |
| Vesterinen 2016 | HIT(0.65) > HVT(0.38) | HIT improved (P = 0.002), HVT n.s.; no between-arm test | ⚠ MARGINAL |

The panel validates QDOT as a ranking instrument — it does not validate it as a predictor of absolute outcome magnitudes. Detailed panel methodology, absolute-level analysis, and per-study caveats are documented in the Technical Specification.

---

## 6 — The experiment: 153 protocols in three steps

We assembled training protocols from 18 sources — six app-based platforms (Garmin, Runna, Strava, Coros, NRC, Polar), four book-based programs (Daniels, Pfitzinger, Hansons, Higdon), six published intervention studies, Runapp, and a no-plan control — yielding 148 protocol×distance cells across seven race distances. Five more runs complete the batch of 153: three diagnostic dose ladders and two anecdotal reference plans used as order-of-magnitude checks. Each simulation placed 1,000 virtual runners on a plan and tracked their fitness trajectory and injury accumulation.

The experiment is structured in three steps. **Step 1** runs all plans at full adherence without constraints — the idealized case. **Step 2** constrains everyone to the same weekly budget (three sessions, 60 minutes each) — the defensible cross-platform comparison, since Step 1 is confounded by plan-length differences ranging from 24 to 106 sessions across the field, and by more than a factor of two within a single distance group. **Step 3** introduces realistic adherence profiles: app-based platforms achieve higher session completion rates than static book-based plans.

| Distance | Step 1 Runapp | Step 1 best ext | Step 2 Runapp | Step 2 best ext | Step 3 Runapp | Step 3 best ext |
|---|---:|---|---:|---|---:|---|
| 5k | 1.82 | 1.43 (Runna) | 1.84 | 1.68 (Runna) | 1.34 | 1.01 (Runna) |
| 10k | 1.98 | 1.47 (Runna) | 1.98 | 1.96 (Runna)† | 1.40 | 1.06 (Runna) |
| Half marathon | 2.52 | 1.81 (Runna) | 2.52 | 2.51 (Runna)† | 1.83 | 1.34 (Runna) |
| Marathon | 2.89 | 1.55 (Hansons) | 2.89 | 2.77 (Runna) | 2.25 | 1.13 (Runna) |

†The difference between the two plans is smaller than the standard error of either estimate (1,000 runners per plan).

**The study arms are run, not ranked.** The sixteen arms of the six intervention studies take part in all three steps, but the table ranks consumer plans only: a published study protocol cut to a consumer budget is not a plan anyone is sold. The exclusion matters in one cell. Under Step 2 at 10K, the polarized arm of Stöggl & Sperlich scores 2.11, above the leading Runapp plan's 1.98. In every other cell of the table the leading Runapp plan stays first with the study arms included.

**The three-step story.** Under constraint (Step 2), external protocols approach parity with Runapp at some distances *despite* not being optimized against QDOT — the near-ties suggest these plans contain design insights that Runapp's optimization has not yet fully captured. Under realistic adherence (Step 3), app-based platforms pull ahead because book-based plans lose a disproportionate share of their quality sessions — the ones most likely to be skipped are the ones that contribute most to gain. At the four distances in the table, among plans with a positive QDOT in both steps, book-based plans lose 73–97% of their Step 1 QDOT; app-delivered plans, Runapp's included, lose 8–38%. At the same four distances, two book-based plans — Daniels and Higdon at the half marathon — fall below zero under realistic adherence, and three plans at 5K (Higdon, Garmin and Runna) are below zero already in Step 1. These ranges and exceptions do not cover the three distances outside the table.

**The optimization asymmetry** applies to every comparison: Runapp's plans are iteratively refined against QDOT; the competitors' are not. A QDOT ranking between Runapp and non-Runapp protocols measures access to the optimization process as well as protocol quality. This asymmetry must always be stated alongside any comparative result. The full calibration history, plan design decisions driven by QDOT, and detailed per-step breakdowns are documented in the Technical Specification.

*QDOT v0.4 — 153 protocols (148 from 18 sources; 147 in leaderboard), 7 distances. Full simulation data available on request.*

---

## 7 — The meta-point

Running has no shortage of training philosophy. It has a shortage of measurement. Everyone agrees that a good plan balances stimulus and safety — but without a metric, "balance" means whatever the person selling the plan says it means.

QDOT reframes the debate. Instead of arguing about philosophy, we can argue about parameters. Instead of "Daniels is better than Higdon," we can ask "at what risk preference does Daniels beat Higdon?" Instead of "our plan is the best," we can say "our plan scores highest on this metric, with these assumptions, and here's what changes if the assumptions are wrong."

That's not a marketing message. It's a research program.

---

## 8 — What QDOT is not

**QDOT is not a score for runners.** It's a score for plans. The risk component measures what the plan imposes at full compliance — a property of the prescription, not the person.

**QDOT is not validated against real-world outcomes.** The gain comes from an impulse-response model. The injury probability comes from a survival model. Both are simulation constructs calibrated against published population data — not against a prospective cohort following these plans. QDOT measures "how good is this plan according to our model of physiology," not "how good is this plan, full stop."

**QDOT is an instrument, not a verdict.** Its value depends on the quality of the underlying models. We publish QDOT with its caveats because an explicit, quantified, debatable metric is more useful than an implicit, unquantified, undebatable marketing claim. The evidence hierarchy matters: published intervention data, observational findings, expert consensus, and engineering assumptions are not interchangeable forms of support. QDOT distinguishes empirical parameters from engineering defaults and treats replication across independent studies as a stronger test than confirmation within a single one — consistent with the principles of evidence-based practice (Sackett et al., 1996).

---

## 9 — Three public caveats

**The risk-preference parameter is normative.** It cannot be calibrated from data — the gain and risk domains carry no information about each other's units. It is a preference parameter encoding how much injury risk reduction a decision-maker would trade for a unit of gain. Its consequence is published rather than hidden: across a twenty-four-fold range of the parameter, among the consumer plans and the no-plan control at 10K under Step 1, the leading plan changes twice — from the highest-gain variant at low values to the lowest-risk variant at high values — while the top position stays with the same platform and the no-plan control finishes last at every value. The sensitivity table and the reading of the chosen value as "the risk at which a plan keeps half its gain" are in the Mathematical Specification.

**The adherence gap is an engineering default.** The difference between app and static adherence has directional support in the literature, but the magnitude is not measured against real Runapp users. If both classes had equal adherence, the Step 3 story collapses to Step 2.

**QDOT is an optimization objective, not an independent benchmark.** Runapp's engine is explicitly optimized to maximize QDOT. We built the instrument and then built our plans against it — parameter sweeps, methodology corrections, recalibrations, plan-composition adjustments — over approximately five months of iterative development, each step documented in the governance log. Runapp's QDOT score is therefore evidence that we have optimized against our own metric, not evidence of superior real-world outcomes. The appropriate test is prospective: do runners on high-QDOT plans get faster, adhere better, and experience fewer injuries? That test has not been run. Until it has, every comparative claim carries this qualification.

The complete caveat register — including model-level limitations, structural assumptions, and open research questions — is maintained in the QDOT Caveat Register under NDA.

---

## 10 — Where this is going

QDOT v0.4 has passed its external stress test and resolved the structural limitations identified in earlier versions — including the sole directional error in the panel, volume bias in the adaptation model, and the absence of formal derivation for the risk-preference parameter. What remains open:

**Prospective validation.** The ultimate test is whether runners assigned to high-QDOT plans actually get faster, adhere better, and experience fewer injuries. This requires real-world outcome data that can only be collected once the product is deployed at scale.

**Empirical adherence data.** The app-vs-static adherence split remains an engineering default, not measured against real Runapp users.

**Cross-validation against multidimensional models.** Work like Kontro et al. (2026) suggests that carefully quantified training blocks should be compared against actual performance outcomes. As wearable training data accumulates at scale, the possibility of testing multidimensional adaptation hypotheses against observed outcomes moves from theoretical to practical.

QDOT is designed as a falsifiable model rather than a claim of physiological truth. Its assumptions generate predictions that can be tested against independent interventions and revised when the evidence does not support them (Popper, 1959). Every caveat above is a specific prediction about where QDOT might fail. Stating them is a requirement for the instrument to be taken seriously.

---

## 11 — Map

**In this repository**
- The overview of how Runapp validates its plans: [README](../README.md).
- The simulation framework QDOT is computed in: [The Runapp Training Simulator](simulator.md).
- The studies behind QDOT's parameters and panel: [Evidence Register: QDOT](../reference/qdot-evidence-register.md).
- Under NDA, shown here as title and abstract only: the Mathematical Specification, the QDOT Technical Specification, the QDOT Computational Chain and the QDOT Caveat Register ([nda/](../nda/)).

**The other parts**
- What Runapp is — the training engine, the escalation mechanism, adaptation and motivation: [runapp-platform](https://github.com/jonasmaandiwallin/runapp-platform).
- How it was built — Governed Agentic Engineering: [governed-agentic-engineering](https://github.com/jonasmaandiwallin/governed-agentic-engineering).
