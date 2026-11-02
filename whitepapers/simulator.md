---
title: "The Runapp Training Simulator: Measuring What Matters Before Anyone Runs a Step"
type: reference
status: draft
version: "0.5"
date: "2026-11-02"
author: "Tooling & Architecture"
audience: "External — no IP disclosure. Readable without NDA."
reading_order: 2
package: validation
release: public
qdot_version: "0.4"
qdot_epoch: "v0.4"
simulator_head: "55f4bc9"
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
    scope: "Text and structure of versions up to 0.4 (2026-09-03), written by the Tooling & Architecture agent. The model of those sessions is not established: no handoff of that date names it."
    evidence: "The document's own text; each result names its epoch (v0.4), its mode (cohort or deterministic) and its runner count."
    reason: null
  - role: technical-analysis
    status: complete
    scope: "Result tables read from simulator runs at epoch v0.4, simulator commit 55f4bc9."
    evidence: "Section 5 names the epoch, mode and cohort size behind each table."
    reason: null
  - role: editing
    status: complete
    scope: "Version 0.5: sections numbered to the white-paper template; the glossary pointer for QDOT_raw replaced by its definition; the closing map rewritten for the public repository; the protocol count in sections 2 and 3.1 restated (148 from 18 sources plus five diagnostic and reference runs); the first reading of the mixed field (section 5.2) rewritten after a recomputation showed the wearable-native spread is three times the gap to either neighbouring class; the number of research groups behind the validation panel in section 6 corrected from four to five; two understatements in 5.3 and 5.4 made exact; the warm-up accounting and storage of the deterministic runs disclosed at the head of section 5. No measured figure changed."
    evidence: "The diff against version 0.4."
    reason: null
  - role: fact-check
    status: complete
    scope: "The cohort results in sections 5.1 and 5.2 recomputed from the stored epoch v0.4 runs; the deterministic results in sections 5.3 to 5.5, whose runs were never stored, re-run with the same configuration and found identical; section 5.6 read from its stored runs; the counts in sections 2, 3 and 6 checked against the protocol library and the evidence registry; claims the figures did not bear were corrected."
    evidence: "The release fact-check report of 2026-11-02, one row per claim with its source, whether that source is primary, and the outcome."
    reason: null
  - role: review
    status: complete
    scope: "Adversarial review in two rounds against five classes: a figure without a source, a claim beyond its figures or source, NDA content in public text, two files of the release contradicting each other, and frontmatter."
    evidence: "Round 1 (2026-11-02): 5 blocking and 4 advisory findings across the release, all corrected in this version. Round 2 (2026-11-02): no blocking or advisory findings."
    reason: null
license: "CC-BY-4.0"
repository: "https://github.com/jonasmaandiwallin/runapp-validation"
path: "whitepapers/simulator.md"
---

# The Runapp Training Simulator: Measuring What Matters Before Anyone Runs a Step

*A Monte Carlo framework for evaluating training plan quality*

> *This document describes the design rationale, validation methodology, and key findings of the Runapp training simulator. The formal mathematical system — including all parameter values, model equations, and calibration procedures — is documented in the Mathematical Specification, available under NDA. The simulator source code is proprietary to Jonas Maandi Wallin and is not disclosed.*

---

## 1 — The evaluation problem

The running industry builds training plans. It does not measure them.

There is no standard way to answer a straightforward question: if a recreational runner follows Plan A versus Plan B, which plan is more likely to make them faster — and at what injury cost? Coaches rely on experience and intuition. Apps rely on internal metrics that measure training load, not training outcome. Academic studies compare a handful of protocols in controlled settings with small sample sizes. Nobody runs a thousand virtual athletes through each plan and measures what happens.

This is the gap the Runapp simulator was built to fill. It is not a coaching tool. It is a measurement instrument — a controlled environment where training plans can be stress-tested under realistic conditions before they reach a single human runner.

---

## 2 — Why simulation?

Three problems make real-world evaluation of training plans impractical at the scale needed to make confident product decisions.

**The compliance problem.** In a clinical trial, subjects follow the protocol. In the real world, runners skip sessions, shorten workouts, run easy days too hard, and run hard days too easy. A plan's theoretical quality is irrelevant if human behavior degrades it. Any evaluation framework must model how plans perform under realistic execution, not just under perfect compliance.

**The scale problem.** A typical exercise-science RCT enrolls 15–30 subjects per arm. At that sample size, meaningful differences in training-plan quality are invisible against the noise of individual variation. Detecting a 0.5 VDOT difference between plans requires thousands of subjects. No study budget can fund that. Simulation can.

**The comparison problem.** Published studies compare two to four protocols within a single experimental design. The industry needs to compare well over a hundred protocols from many sources across seven race distances, under varying constraints. No experimental design can do this. A simulator can evaluate every protocol on the same physiological model, with the same assumptions, under the same conditions — and change one variable at a time.

Simulation does not replace empirical testing. It precedes it. The simulator identifies which comparisons matter, estimates effect sizes, and generates testable predictions. Empirical validation then tests those predictions against reality. The order matters: simulate first, then validate — not the reverse.

---

## 3 — Architecture

The simulator transforms a training plan into a predicted population outcome through a chain of interacting subsystems. Each subsystem is documented in the Mathematical Specification with full equations; this section describes the chain's logic without disclosing the formal system.

### 3.1 — Protocol input and session generation

Each training plan enters the simulator as a structured protocol definition specifying phases, weekly structure, and intensity distribution. The measurement batch of epoch v0.4 contains 153 protocols across seven race distances: 148 from 18 sources, plus three diagnostic dose ladders and two anecdotal reference plans used as order-of-magnitude checks. Six of those distances include a Runapp plan.

Sessions are generated deterministically from the protocol's phase structure. Each phase distributes its weekly volume across the declared number of sessions, assigning each session one of three model zones — easy, moderate, or hard — that group the standard pace categories from exercise physiology. The simulator models the zone and total duration of each session, not its internal structure.

### 3.2 — Compliance: adherence and intensity adherence

Two independent compliance mechanisms determine how much of the prescribed plan each virtual runner actually executes.

Session adherence governs whether each session is performed at all. Three delivery-form classes — app-delivered, static (published plans without interactive delivery), and supervised — replace the earlier binary split. Each class carries its own adherence distribution, reflecting the empirical observation that structured digital delivery supports higher session completion than an unmonitored written plan. In cohort mode, each session's execution is an independent probabilistic draw: a failed draw means the session is skipped entirely, contributing no training stimulus to the adaptation model — though it still counts as exposure in the injury model.

Intensity adherence captures how closely a runner's actual training matches the prescribed zone distribution. Platforms with real-time feedback (like Runapp) achieve higher zone fidelity than platforms where the runner self-monitors. The difference is small in any single session but compounds over weeks and months. Intensity adherence also degrades over time — a longitudinal decay that represents the gradual erosion of execution quality in longer plans.

This two-dimensional compliance model is important for interpretation. When the simulator shows that one plan outperforms another, the advantage may come from plan design, from execution support, or from both. The simulator can isolate these effects — a decomposition analysis presented in section 5.

### 3.3 — Training dose

Each performed session produces a training dose weighted by zone intensity, with an absorption ceiling that limits the effective contribution of very long sessions. Minutes beyond the ceiling lose effectiveness progressively, capturing the physiological reality that the fifth hour of an easy run does not produce the same adaptation stimulus as the first.

The raw dose passes through four independent modifiers: intensity adherence (how precisely the session hit its target zone), an optimality factor (how well the plan's intensity distribution matches the training phase), a recovery-violation penalty (accumulated cost of insufficient rest between hard sessions), and a frequency factor (diminishing returns from additional sessions within the same week).

The modified dose is what enters the adaptation model. It is not read by the injury model, which operates on the scheduled plan rather than the executed plan — a design choice that ensures injury risk reflects the plan's ambition, not the runner's compliance with it.

### 3.4 — Fitness–fatigue dynamics

The adaptation model implements a fitness–fatigue impulse-response framework in which each training session simultaneously builds fitness (with slow dynamics) and generates fatigue (with fast dynamics). The net performance at any point is the balance between accumulated fitness and residual fatigue — a temporal model that captures supercompensation, overreaching, and the delayed effects of training.

What distinguishes this implementation from conventional single-axis models is zone-specific saturation. Different training intensities contribute to adaptation through separate nonlinear channels, each with its own capacity and half-saturation point. Easy-zone volume accumulates fitness with high capacity and gradual diminishing returns. Hard-zone training generates adaptation more rapidly but saturates earlier. This architecture prevents the model from rewarding plans that stack a single intensity — the mathematical representation of the well-known problem where moderate-intensity training generates fatigue without proportional adaptation.

Because fatigue clears faster than fitness, performance continues to rise briefly after training ends. The simulator evaluates gain at the post-plan peak rather than at the last training day, capturing the taper effect.

### 3.5 — Gain mapping

The performance output of the fitness–fatigue model is an internal score, not a directly interpretable quantity. The gain mapping translates it into VDOT gain through two steps.

First, utilization measures activated physiological capacity relative to a maintenance threshold, with exponential saturation. A plan that fails to generate sufficient stimulus falls below the threshold and produces negative utilization — the runner detrains. This structural property correctly penalizes undertraining: plans must generate net positive adaptation to register any fitness gain.

Second, a piecewise gain-rate curve maps utilization to VDOT change per month. The curve is fitness-level-dependent: beginners gain more per unit of stimulus than advanced runners, consistent with the diminishing returns observed in training studies. The gain rate saturates at high utilization, preventing the model from predicting implausible gains from extreme training loads.

Final physiological gain incorporates plan duration and individual responsiveness — the well-documented observation that runners differ in how much they adapt to the same training stimulus.

### 3.6 — Injury model

The injury model represents cumulative injury probability as a survival process driven by three mechanistically distinct risk dimensions.

The spike component detects acute session-to-session load increases — sudden jumps in training stress relative to recent history. The volume component measures average weekly training volume against a distance- and fitness-dependent reference curve. The violation component accumulates the cost of insufficient recovery between hard sessions. These three dimensions combine into a composite risk score with a weighted sum, transformed through a convex hazard function that amplifies high-risk exposures.

Individual heterogeneity enters through a frailty multiplier drawn from a heavy-tailed distribution — some runners are constitutionally more injury-prone than others — and a previous-injury multiplier for runners with injury history.

The survival law converts the hazard into a cumulative probability of remaining injury-free over the plan's duration. The probability grows with session count but sub-linearly: doubling the number of sessions less than doubles the injury risk, reflecting the adaptation effect of regular training.

Injury is calibrated against published epidemiological data from a large cohort study. The calibration has been re-solved six times as the model evolved, always targeting the same empirical anchor.

### 3.7 — Monte Carlo population

In cohort mode, the simulator creates a population of virtual runners, each drawn from independent distributions of physiological time constants, fatigue sensitivity, training responsiveness, injury susceptibility, and compliance tendency. Each runner experiences the training plan independently, accumulating adaptation and injury risk according to their individual characteristics and stochastic session-level compliance outcomes.

The key output is not a single predicted outcome but a distribution: the mean, median, spread, and tails of the population's response to the training plan. This captures what clinical trials with small samples cannot — the probability that a randomly selected runner will improve, stagnate, or get worse on a given plan.

A deterministic mode runs a single runner with population-mean parameters and no stochastic variation, providing a clean comparison of plan design without compliance noise. Deterministic results carry no injury probability and therefore cannot produce QDOT.

---

## 4 — The quality metric: QDOT

The simulator produces raw outputs — fitness gain, injury probability, training load, weekly trajectories. These need to be collapsed into a single quality signal that allows direct comparison across plans.

That signal is QDOT. It combines the adaptation model's gain output with the injury model's probability output into a risk-adjusted efficiency metric, analogous to the Sharpe ratio in finance: higher QDOT means more adaptation per unit of risk, per unit of time. QDOT is described in detail in its own white paper.

QDOT's numerator derives from the adaptation pipeline described above — the same fitness–fatigue dynamics, gain mapping, and population sampling that produce the simulator's fitness predictions. Its denominator derives from the injury pipeline — the same hazard model, survival law, and frailty distribution. The simulator and QDOT are not independent instruments assembled from separate components; they share a single mathematical system. What separates them is the question they answer. The simulator asks: *what happens when a population follows this plan?* QDOT asks: *given what happened, was it worth the cost?* A criticism of the adaptation model affects both equally. A disagreement about how to weight injury risk against fitness gain is a QDOT question that leaves the simulator untouched. The two are documented separately because they can be evaluated on different grounds — but they cannot be evaluated as if they were built from different models.

QDOT is normalized so that the median plan in the current measurement epoch scores 1.0. Plans scoring above 1.0 produce more risk-adjusted adaptation per week than the median; plans below 1.0 produce less. QDOT can be negative — a plan that on average detrains its cohort receives a negative score.

---

## 5 — Results

We present results from five analysis dimensions, each designed to answer a specific question about training plan quality. All results are from measurement epoch v0.4. The cohort results (5.1 and 5.2) use the simulator's default accounting of warm-up time, in which warm-up minutes count as easy running. The deterministic results (5.3 to 5.6) use the alternative accounting, in which a session's whole duration counts at its own zone; it gives somewhat higher gains, so deterministic and cohort figures are not compared with each other. The runs behind 5.3 to 5.5 were not stored and are reproducible by re-running, not by query.

### 5.1 — Flagship cohort: one thousand virtual runners per plan

The definitive comparison. Each plan was simulated with one thousand runners drawn from the same population distribution, at the same starting fitness (VDOT 45, the trained-tier anchor of the gain model), with realistic compliance behavior.

**Median fitness gain by distance and source:**

| Distance | Runapp | Pfitzinger | Runna | Hansons |
|---|---|---|---|---|
| 5K | 0.56 | −0.04 | 0.00 | — |
| 10K | 0.92 | 0.00 | 0.57 | — |
| Half marathon | 1.28 | −0.02 | 0.67 | 0.00 |
| Marathon | 1.53 | −0.06 | 0.48 | 0.06 |

*Values are median VDOT gain across 1,000 runners. Runapp uses its natural (unconstrained) plan variant. Epoch v0.4.*

Three findings stand out.

First, the median for Pfitzinger is zero or negative at every distance. More than half of runners following those plans gain nothing — or get worse. The plans are well-designed in theory (they rank well in deterministic simulation) but fragile in practice: they depend on near-perfect execution that most runners cannot sustain.

Second, Runapp's advantage grows with distance. The 5K gap is moderate. By the marathon, Runapp's median gain exceeds Runna's by a factor of three and exceeds Pfitzinger by more than 1.5 VDOT points. Longer plans amplify both the benefits of robust design and the costs of fragile design.

Third, the spread matters as much as the center. Runapp's 10th-percentile runner sits at zero across distances — roughly where the *median* runner sits under Pfitzinger — while Pfitzinger's 10th-percentile runner consistently loses fitness. The worst-case scenario under Runapp is roughly the median scenario under competitors. The persisted table behind these figures, with percentiles and injury probabilities per cell, is in the Simulation Data report under NDA.

**Optimization asymmetry applies.** Runapp's plans are designed using the simulator's physiological model; competitors' plans are not. This structural advantage is disclosed and discussed in section 6.

### 5.2 — Mixed-field scenario: a virtual 10K race

The flagship comparison tests each plan in isolation. But real runners choose from a crowded market. What does the distribution of outcomes look like across the full spectrum of available training approaches?

We simulated a virtual 10K race field with 11 protocols spanning the complete delivery-form taxonomy: one adaptive app with real-time feedback (Runapp), one semi-adaptive app-based plan, three wearable-native plans, two app-static plans, three book-based plans, and a control group training without any structured plan. Each protocol was simulated with one thousand runners drawn from the same population, and the field was re-run at ten thousand runners per protocol with the same ranking. All protocols were given equal cohort sizes; the field is not weighted by market share.

**Results by delivery class (median VDOT gain; QDOT_raw, the risk-adjusted gain over the whole plan in VDOT points, before division by plan length and normalization):**

| Delivery class | Protocols | Median gain range | QDOT_raw range | Injury range |
|---|---|---|---|---|
| Adaptive app (real-time feedback) | 1 | 0.92 | 0.41 | 21.9% |
| Semi-adaptive app | 1 | 0.57 | 0.27 | 22.9% |
| Wearable-native | 3 | 0.29–0.50 | 0.18–0.25 | 13–20% |
| App-static | 2 | 0.17–0.22 | 0.11–0.16 | 7–14% |
| Book-static | 3 | −0.06–0.00 | 0.01–0.08 | 12–23% |
| No structured plan | 1 | −0.13 | −0.10 | 4.3% |

Three findings emerge that the flagship comparison does not show.

First, the ordering follows the delivery class at its boundaries: every app-delivered plan outperforms every book-based plan, and every structured plan outperforms no plan. Inside a class the plan still matters — the three wearable-native plans span 0.29 to 0.50, three times the gap to either neighbouring class — but no book-based plan reaches the weakest app-delivered one. This suggests that the delivery mechanism — how the plan reaches the runner and supports execution — matters alongside the plan's physiological design.

Second, book-based plans have a median gain at or below zero. The plans are well-designed in theory (their deterministic performance is competitive) but their static delivery means that compliance degrades over weeks without feedback or adaptation. The 90th-percentile runner on a book-based plan still gains meaningfully, showing that the plans work for highly disciplined runners — but the median runner is not highly disciplined.

Third, running without any structured plan produces negative outcomes. The control group's median gain is −0.13, meaning the typical unstructured runner slightly regresses over a 12-week period. This establishes a meaningful baseline: a structured plan must demonstrably outperform this to justify its existence. All structured plans do — but the margin varies from substantial (Runapp: +1.05 above baseline) to marginal (the weakest book-based plan: +0.07 above baseline).

The mixed-field scenario shows an effect that cannot be seen from the 2×2 decomposition alone: under realistic adherence, plan design and delivery form compound. The 2×2 analysis (section 5.5) finds no interaction at full execution — the plan carries the advantage on its own. The mixed field adds session skipping, and there the delivery class determines how much of a plan's designed quality actually reaches the runner.

### 5.3 — Consumer scenario: constrained runners

Not every runner can train five days a week for unlimited time. The consumer scenario tests plans under recreational constraints: three sessions per week, maximum 60 minutes per session.

The comparison is deterministic (single modeled runner at VDOT 45, every session executed) and has one comparator: a book-based program run under the same constraint. It is not a field-wide ranking — the constrained field-wide ranking is the second step of the three-step experiment described in the QDOT white paper, and it is a cohort measurement on a different scale.

Under these constraints, Runapp's fitness gain at the half marathon is 2.2 times the book-based program's, and at the marathon 6.2 times — the book-based program's marathon gain nearly vanishes when its sessions are capped. At the shorter distances the pattern reverses: at 10K the two build comparable fitness, with Runapp at lower injury cost; at 5K the book-based program builds about a fifth more fitness and Runapp's edge is the lower injury cost. This is consistent with the expectation that plan design matters more when the plan is longer and has more room for differentiated periodization — and it is at the long distances that the cap-aware architecture, not the session composition, is doing the work.

### 5.4 — What the 60-minute cap costs

A 60-minute session cap is a realistic constraint for many runners. We measured its cost across all distances and training frequencies by comparing each plan with and without the cap.

At 5K, the cap costs nothing — sessions are already short. At 10K, the cap reduces gain by 5–9% depending on training frequency. At the half marathon, the cost rises to 9–13%. At the marathon, it reaches 10–15%. The cost tends to fall with training frequency — more sessions means each is shorter and fewer get truncated — with one exception at the marathon, where the four-session variant is an outlier in the underlying data.

This data helps runners make informed trade-offs. A runner training for a half marathon who can only commit 60 minutes per session knows they are leaving 9–13% of their potential gain on the table, more at three or four sessions a week than at five — a meaningful but not devastating constraint.

### 5.5 — Decomposing the advantage: plan design versus execution support

The headline result — Runapp outperforms competitors — invites a natural question: is the advantage coming from better plan design, better execution support (the real-time feedback that improves zone compliance), or both?

We isolated these effects using a 2×2 factorial design at 10K. Each cell combines one source's plan with one source's compliance profile:

| | Runapp compliance | Competitor compliance |
|---|---|---|
| **Runapp plan** | 1.47 | 1.45 |
| **Competitor plan** | 1.33 | 1.31 |

*Values in modeled VDOT gain, epoch v0.4, deterministic single-runner mode at 10K with every session executed as prescribed (the competitor is a book-based program). Because the runs are deterministic, the compliance dimension here is the platform's intensity-targeting profile only — session skipping is not in play.*

The total advantage is 0.16 VDOT. Swapping only the plan design while holding the compliance profile constant moves the result by 0.14 — seven-eighths of the total. Swapping only the compliance profile while holding the plan constant moves it by 0.02 — one-eighth. There is no interaction term: the two effects add up exactly to the total.

That is a cleaner result than an interaction story would have been. At full execution, the advantage is in the plan itself — session composition, volume distribution, phase structure — and it is the same advantage regardless of how precisely the sessions are executed. The execution support adds a small, plan-independent increment on top.

We verified the small size of the compliance-profile effect by giving five competitor plans Runapp's intensity-targeting profile. Their gains improved by 1.5–3.1%. The ranking did not change. Superior intensity targeting alone does not close the gap; the plan does.

Where the two effects *do* compound is under realistic adherence, when sessions are skipped rather than merely executed imprecisely. That effect shows up in the mixed-field results and the cohort-mode flagship comparisons — not in this deterministic table.

### 5.6 — Stability across fitness levels

Training plan quality should not be an artifact of the reference runner's fitness level. We tested the 10K plans at five entry fitness levels — VDOT 35 to 55, spanning the beginner-to-elite tiers of the gain model — in deterministic mode. The key finding: Runapp's advantage over the best competitor remains between 11% and 12% (10.6% at VDOT 55), and the ranking of the four plans tested is the same at all five. The absolute gains scale with fitness (fitter runners gain less, in absolute terms), but the relative picture is invariant. The sweep is tabulated in the Simulation Data report under NDA.

---

## 6 — The circularity question

A natural objection: Runapp built the simulator, and Runapp's plans win. Isn't this circular?

The concern is legitimate and we address it directly.

**The simulator does not know about Runapp.** The physiological model, injury model, and compliance model contain no Runapp-specific logic. They implement published exercise-science frameworks calibrated against external data. Any training plan — from any source — can be evaluated.

**The compliance model's advantages are directional, not arbitrary — and not measured on Runapp users.** The intensity-adherence parameters reflect the observation that real-time heart-rate feedback improves intensity accuracy; Runapp uses such feedback, most competitors' plans are executed without it. The direction has literature support. The magnitudes are engineering defaults, and one of the six values carries no evidence identifier at all — both facts are recorded in the caveat registers. The decomposition analysis shows the whole profile accounts for one-eighth of the gap.

**External validation anchors the model.** The simulator's adaptation model is validated against six published intervention studies spanning 16 protocol arms and five different research groups. Five of six study rankings are correctly reproduced. The injury model is calibrated against published epidemiological data. These external anchors constrain the model's degrees of freedom.

**The decisive argument is the optimization asymmetry.** Runapp's plans are designed using the simulator's physiological model. Competitors' plans are not — they were designed independently using traditional coaching methodologies. This means Runapp's plans are, by construction, optimized against the model that evaluates them. If the model is a reasonable approximation of reality, this optimization should produce genuine advantages. If the model is wrong, the advantages are artifacts.

The optimization asymmetry is a feature, not a bug — it is the entire point of building a simulator. But it means that the simulator's results should be interpreted as "given this model of physiology, Runapp's plans are optimal" rather than "Runapp's plans are objectively the best." The distinction between these claims can only be resolved by empirical validation — which is why we are publishing the model for scrutiny.

---

## 7 — Limitations

We document known limitations explicitly, because an instrument's credibility depends on honest accounting of what it cannot do.

**No prospective validation against real runners.** All results are simulated. The external validation (six published studies) tests the adaptation model's ranking accuracy, not its absolute predictions. Simulated VDOT gains systematically understate measured VO₂max changes. QDOT's strength is ranking, not prediction of absolute magnitudes.

**Many parameters are engineering defaults.** The adherence gap between app-delivered and static plans is directionally supported by research on digital exercise interventions and compliance monitoring, but the specific magnitudes are engineering assumptions, not fitted values. The same is true for several injury-model parameters.

**The compliance model uses platform-level averages.** Individual runners' compliance varies far more than the platform average captures. A disciplined runner following any plan will outperform a careless runner following Runapp. The simulator reports population-level statistics, not individual guarantees.

**The injury model is cumulative, not mechanistic.** It captures epidemiological patterns (acute load spikes, volume exposure, recovery spacing) but does not model specific injury mechanisms. This limits its ability to distinguish between injury types or predict which injury a runner might sustain.

**Certain training modalities are not modeled.** Strength training, heat acclimation, altitude exposure, and cross-training are not represented. Plans that derive significant benefit from these modalities are undervalued by the simulator.

**The optimization asymmetry cuts both ways.** If the model contains systematic biases — for example, if it overvalues easy-volume distribution or undervalues threshold-heavy approaches — those biases would artificially inflate Runapp's advantage. The external panel validation constrains but does not eliminate this risk.

Full known-limitation registers are maintained separately: the QDOT Caveat Register (instrument limitations) and the Simulator Caveats (model limitations), both available under NDA. The two registers have different owners of risk — the instrument versus the model — but share the same classification system.

---

## 8 — What comes next

The simulator is a measurement instrument in its first generation. Three development directions are underway.

**Empirical validation.** The simulator generates testable predictions that can be compared against real-world training data. As Runapp's user base grows, anonymized training outcomes can be compared against simulated predictions — closing the gap between modeled and measured results.

**Extended modalities.** Adding athlete-mode capabilities (warmup modeling, plyometric training, heat response) expands the range of training approaches the simulator can evaluate.

**Publication.** This white paper is a positioning document. The formal mathematical system, including the complete equations, calibration methodology, and validation results, is documented in the Mathematical Specification and available for review under NDA. We welcome scrutiny — an instrument that cannot survive external examination is not an instrument worth building.

---

## 9 — Map

**In this repository**
- The overview of how Runapp validates its plans: [README](../README.md).
- The quality metric computed from the simulator's output: [QDOT: A Sharpe Ratio for Training Plans](qdot.md).
- The studies behind the simulator's models and calibration: [Evidence Register: Simulator](../reference/simulator-evidence-register.md).
- Under NDA, shown here as title and abstract only: the Mathematical Specification, the Simulator Caveats and the two Simulation Data reports ([nda/](../nda/)).

**The other parts**
- What Runapp is — the training engine, the escalation mechanism, adaptation and motivation: [runapp-platform](https://github.com/jonasmaandiwallin/runapp-platform).
- How it was built — Governed Agentic Engineering: [governed-agentic-engineering](https://github.com/jonasmaandiwallin/governed-agentic-engineering).
