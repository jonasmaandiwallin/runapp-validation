---
title: "Evidence Register: QDOT — A Sharpe Ratio for Training Plans"
type: reference
status: current
version: "0.3"
date: "2026-11-02"
author: "Tooling & Architecture"
audience: "External — no IP disclosure. Readable without NDA."
reading_order: 5
package: validation
release: public
framework:
  name: "Governed Agentic Engineering (GAE)"
  originator: "Jonas Maandi Wallin"
editor: "Jonas Maandi Wallin"
contact: "https://www.linkedin.com/in/jonasmaandiwallin"
author_llm:
  - model: null
    model_id: null
    roles: [drafting]
    source: not-established
  - model: "Claude Opus 5.5"
    model_id: "claude-opus-5-5"
    roles: [editing, fact-check]
    source: platform
  - model: "Claude Sonnet 5"
    model_id: null
    roles: [fact-check]
    source: handoff
  - model: "Claude Fable 5.1"
    model_id: "claude-fable-5-1"
    roles: [review]
    source: handoff
ai_disclosure:
  - role: drafting
    status: complete
    scope: "Selection of references, grouping and roles in versions up to 0.2 (2026-09-03), written by the Tooling & Architecture agent. The model of those sessions is not established: no handoff of that date names it."
    evidence: "The document's own text: each entry names its DOI where one exists."
    reason: null
  - role: technical-analysis
    status: not-applicable
    scope: null
    evidence: null
    reason: "The register lists literature; it carries no measurement."
  - role: editing
    status: complete
    scope: "Version 0.3: public frontmatter added and the closing map rewritten for the public repository. Bibliographic data corrected after a check against Crossref and the publishers: DOIs for Busso 1990, Videbæk, Vermeire, Impellizzeri and Marchal; title and journal for Stephens Hemingway and Marchal; subtitle for Kluitenberg; title and author form for Santos; PMID in place of DOI for Nielsen and Damsted; editors, edition and ISBN for Banister; Mølmen replaced by the review the entry describes; Lolli 2019 removed, no work with its title found; after the second check, the title of Gavanda 2025 and the subtitle of Seiler & Kjerland. Roles unchanged."
    evidence: "The two bibliographic checks of 2026-11-02 against Crossref and the publishers; the diff against version 0.2."
    reason: null
  - role: fact-check
    status: complete
    scope: "Every reference read against Crossref or the publisher in two passes: first the DOIs without an evidence-registry entry and the references without a DOI, then every DOI with an entry. Each DOI resolves to the work the register names."
    evidence: "The two bibliographic checks of 2026-11-02, one row per reference with its source and outcome; the corrections are listed under editing."
    reason: null
  - role: review
    status: complete
    scope: "Adversarial review of the release in two rounds; for this register, against NDA content, contradictions with the other files of the release, and frontmatter. The bibliography itself was left to the fact-check."
    evidence: "Round 1 (2026-11-02): no finding in this register. Round 2 (2026-11-02): no blocking or advisory finding."
    reason: null
license: "CC-BY-4.0"
repository: "https://github.com/jonasmaandiwallin/runapp-validation"
path: "reference/qdot-evidence-register.md"
---

# Evidence Register: QDOT

*Scientific literature informing the design, calibration, and validation of the QDOT quality instrument.*

---

## How to read this register

Each entry is tagged with an **evidence role**:

- **Foundation** — establishes the physiological, mathematical, or methodological principle the instrument is built on.
- **Parameter support** — provides empirical data informing a threshold, calibration target, or model component.
- **Validation** — used to test whether the instrument reproduces observed training-response relationships.

This register lists what the research says. It does not disclose how the research was operationalized — which parameter values were derived, which calibration constants were set, or how the findings were transformed into the computational chain. The studies are public. The operationalization is not.

---

## Adaptation modeling

| Reference | DOI | Role |
|---|---|---|
| Banister, E.W. "Modeling Elite Athletic Performance." In MacDougall, J.D., Wenger, H.A. & Green, H.J. (eds.), *Physiological Testing of the High-Performance Athlete*, 2nd ed., Human Kinetics, 1991 | — (ISBN 978-0-87322-300-3) | Foundation |
| Busso, T. et al. "A systems model of training responses and its relationship to hormonal responses in elite weight-lifters." *European Journal of Applied Physiology*, 1990 | 10.1007/BF00236693 | Foundation |
| Busso, T. "Variable dose-response relationship between exercise training and performance." *Medicine & Science in Sports & Exercise*, 2003 | 10.1249/01.MSS.0000074465.13621.37 | Foundation |
| Taha, T. & Thomas, S.G. "Systems modelling of the relationship between training and performance." *Sports Medicine*, 2003 | 10.2165/00007256-200333140-00003 | Foundation |
| Hellard, P. et al. "Assessing the limitations of the Banister model in monitoring training." *Journal of Sports Sciences*, 2006 | 10.1080/02640410500244697 | Foundation |
| Vermeire, K. et al. "The fitness-fatigue model: what's in the numbers?" *International Journal of Sports Physiology and Performance*, 2022 | 10.1123/ijspp.2021-0494 | Foundation |
| Stephens Hemingway, B.H. et al. "The effects of measurement error and testing frequency on the fitness-fatigue model applied to resistance training: A simulation approach." *International Journal of Sports Science & Coaching*, 2020 | 10.1177/1747954119887721 | Foundation |
| Marchal, A. et al. "Statistical flaws of the fitness-fatigue sports performance prediction model." *Scientific Reports*, 2025 | 10.1038/s41598-025-88153-7 | Foundation |
| Kontro, H. et al. "The three-dimensional impulse-response model: Modeling the training process in accordance with energy system-specific adaptation." *PLoS ONE*, 2026 | 10.1371/journal.pone.0341721 | Foundation |

## Intensity distribution and zone models

| Reference | DOI | Role |
|---|---|---|
| Seiler, S. & Kjerland, G.Ø. "Quantifying training intensity distribution in elite endurance athletes: is there evidence for an 'optimal' distribution?" *Scandinavian Journal of Medicine & Science in Sports*, 2006 | 10.1111/j.1600-0838.2004.00418.x | Foundation |
| Esteve-Lanao, J. et al. "Impact of training intensity distribution on performance in endurance athletes." *Journal of Strength and Conditioning Research*, 2007 | 10.1519/R-19725.1 | Validation |
| Stöggl, T. & Sperlich, B. "Polarized training has greater impact on key endurance variables than threshold, high intensity, or high volume training." *Frontiers in Physiology*, 2014 | 10.3389/fphys.2014.00033 | Validation |
| Muñoz, I. et al. "Does polarized training improve performance in recreational runners?" *International Journal of Sports Physiology and Performance*, 2014 | 10.1123/ijspp.2012-0350 | Validation |
| Helgerud, J. et al. "Aerobic high-intensity intervals improve VO₂max more than moderate training." *Medicine & Science in Sports & Exercise*, 2007 | 10.1249/mss.0b013e3180304570 | Validation |
| Vesterinen, V. et al. "Predictors of individual adaptation to high-volume or high-intensity endurance training in recreational endurance runners." *Scandinavian Journal of Medicine & Science in Sports*, 2016 | 10.1111/sms.12530 | Validation |
| Carnes, A.J. & Mahoney, S.E. "Polarized versus high-intensity multimodal training in recreational runners." *International Journal of Sports Physiology and Performance*, 2019 | 10.1123/ijspp.2018-0040 | Validation |

## Injury epidemiology and risk modeling

| Reference | DOI | Role |
|---|---|---|
| Videbæk, S. et al. "Incidence of running-related injuries per 1000 h of running in different types of runners: A systematic review and meta-analysis." *Sports Medicine*, 2015 | 10.1007/s40279-015-0333-8 | Parameter support |
| Nielsen, R.Ø. et al. "Classifying running-related injuries based upon etiology, with emphasis on volume and pace." *International Journal of Sports Physical Therapy*, 2013 | — (PMID 23593555) | Foundation |
| Kluitenberg, B. et al. "What are the differences in injury proportions between different populations of runners? A systematic review and meta-analysis." *Sports Medicine*, 2015 | 10.1007/s40279-015-0331-x | Parameter support |
| Malisoux, L. et al. "Can parallel use of different running shoes decrease running-related injury risk?" *Scandinavian Journal of Medicine & Science in Sports*, 2015 | 10.1111/sms.12154 | Foundation |
| Frandsen, J. et al. "How much running is too much? Identifying high-risk running sessions in a 5200-person cohort study." *British Journal of Sports Medicine*, 2025 | 10.1136/bjsports-2024-109380 | Parameter support |
| Bache-Mathiesen, L.K. et al. "Not straightforward: modelling non-linearity in training load and injury research." *BMJ Open Sport & Exercise Medicine*, 2021 | 10.1136/bmjsem-2021-001119 | Foundation |
| Kalkhoven, J.T. et al. "Training Load and Injury: Causal Pathways and Future Directions." *Sports Medicine*, 2021 | 10.1007/s40279-020-01413-6 | Foundation |
| Damsted, C. et al. "Is There Evidence for an Association Between Changes in Training Load and Running-Related Injuries? A Systematic Review." *International Journal of Sports Physical Therapy*, 2018 | — (PMID 30534459) | Foundation |

## Workload ratio and ACWR critique

| Reference | DOI | Role |
|---|---|---|
| Gabbett, T.J. "The training—injury prevention paradox: should athletes be training smarter and harder?" *British Journal of Sports Medicine*, 2016 | 10.1136/bjsports-2015-095788 | Foundation |
| Impellizzeri, F.M. et al. "Acute:Chronic Workload Ratio: Conceptual Issues and Fundamental Pitfalls." *International Journal of Sports Physiology and Performance*, 2020 | 10.1123/ijspp.2019-0864 | Foundation |

## Adherence and compliance

| Reference | DOI | Role |
|---|---|---|
| Santos, A. et al. "Rates of compliance and adherence to high-intensity interval training: a systematic review and meta-analyses." *International Journal of Behavioral Nutrition and Physical Activity*, 2023 | 10.1186/s12966-023-01535-w | Parameter support |
| Gavanda, S. et al. "Optimizing Resistance Training Outcomes: Comparing In-Person Supervision, Online Coaching, and Self-Guided Approaches: A Randomized Controlled Trial." *Journal of Strength and Conditioning Research*, 2025 | 10.1519/JSC.0000000000005216 | Parameter support |
| Ranieri, L.E. et al. "Comparison of Heart Rate- and Race Pace-Based Training Prescriptions on Training Execution Accuracy in Recreational Distance Runners." *International Journal of Sports Physiology and Performance*, 2026 | 10.1123/ijspp.2025-0578 | Foundation |

These studies support the adherence class ordering (supervised > app-guided > static delivery) in *direction* only; none is running-specific by delivery form, and the class magnitudes are engineering defaults. The QDOT white paper states this as one of its three public caveats.

## Risk-adjusted measurement

| Reference | DOI | Role |
|---|---|---|
| Sharpe, W.F. "Mutual Fund Performance." *Journal of Business*, 1966 | 10.1086/294846 | Foundation |

## Multidimensional training models

| Reference | DOI | Role |
|---|---|---|
| Mølmen, K.S., Almquist, N.W. & Skattebo, Ø. "Effects of Exercise Training on Mitochondrial and Capillary Growth in Human Skeletal Muscle: A Systematic Review and Meta-Regression." *Sports Medicine*, 2024 | 10.1007/s40279-024-02120-2 | Foundation |
| Vanrenterghem, J. et al. "Training Load Monitoring in Team Sports: A Novel Framework Separating Physiological and Biomechanical Load-Adaptation Pathways." *Sports Medicine*, 2017 | 10.1007/s40279-017-0714-2 | Foundation |

---

*Part of the validation documentation for Runapp. The instrument this evidence informs: [QDOT: A Sharpe Ratio for Training Plans](../whitepapers/qdot.md). The overview: [README](../README.md). The simulator's own register: [Evidence Register: Simulator](simulator-evidence-register.md).*
