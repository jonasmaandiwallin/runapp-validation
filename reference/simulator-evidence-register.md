---
title: "Evidence Register: The Runapp Training Simulator"
type: reference
status: current
version: "0.3"
date: "2026-11-02"
author: "Tooling & Architecture"
audience: "External — no IP disclosure. Readable without NDA."
reading_order: 4
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
    scope: "Selection of references, grouping, roles and the three notes in versions up to 0.2 (2026-09-03), written by the Tooling & Architecture agent. The model of those sessions is not established: no handoff of that date names it."
    evidence: "The document's own text: each entry names its DOI where one exists."
    reason: null
  - role: technical-analysis
    status: not-applicable
    scope: null
    evidence: null
    reason: "The register lists literature; it carries no measurement."
  - role: editing
    status: complete
    scope: "Version 0.3: public frontmatter added, the pointer to the superseded overview document replaced by the repository's README, and the closing map rewritten for the public repository. Bibliographic data corrected after a check against Crossref and the publishers: DOIs for Busso 1990, Videbæk and Halson; subtitle for Kluitenberg; title and author form for Santos, and the population of the Santos review in the adherence note; PMID for Nielsen; editors, edition and ISBN for Banister and Daniels 2014; publisher for Daniels & Gilbert; date for the Polar release; the 4-year novice/experienced cohort cited as Kemler et al. 2018 and the distributed-lag entry as Bache-Mathiesen et al. 2022, the works the entries describe; Lerebourg 2023, Ferreira 2022 and Feely 2020 removed, no work with their titles found; after the second check, the title of Gavanda 2025 and the subtitles of Seiler & Kjerland and Buist. Roles unchanged."
    evidence: "The two bibliographic checks of 2026-11-02 against Crossref and the publishers; an earlier DOI repair of the distributed-lag entry; the diff against version 0.2."
    reason: null
  - role: fact-check
    status: complete
    scope: "Every reference read against Crossref or the publisher in two passes: first the DOIs without an evidence-registry entry and the references without a DOI, then every DOI with an entry. Each DOI resolves to the work the register names. The Polar press release of 6 June 2018 is no longer online; its title and date come from the release's own address in a search listing, not from an archived copy."
    evidence: "The two bibliographic checks of 2026-11-02, one row per reference with its source and outcome; the corrections are listed under editing."
    reason: null
  - role: review
    status: complete
    scope: "Adversarial review of the release in two rounds; for this register, against NDA content, contradictions with the other files of the release, and frontmatter. The bibliography itself was left to the fact-check."
    evidence: "Round 1 (2026-11-02): no finding in this register. Round 2 (2026-11-02): no blocking or advisory finding."
    reason: null
license: "CC-BY-4.0"
repository: "https://github.com/jonasmaandiwallin/runapp-validation"
path: "reference/simulator-evidence-register.md"
---

# Evidence Register: The Runapp Training Simulator

*Scientific literature informing the design and calibration of the Monte Carlo training simulator.*

---

## How to read this register

Each entry is tagged with an **evidence role**:

- **Foundation** — establishes the physiological or methodological principle the model is built on.
- **Parameter support** — provides empirical data informing a model parameter or calibration target.
- **Validation** — used to test whether the simulator reproduces observed training-response relationships.

This register lists what the research says. It does not disclose how the research was operationalized — which parameter values were derived, which time constants were set, or how the findings were transformed into model equations. The studies are public. The operationalization is not.

---

## Fitness-fatigue modeling

| Reference | DOI | Role |
|---|---|---|
| Banister, E.W. "Modeling Elite Athletic Performance." In MacDougall, J.D., Wenger, H.A. & Green, H.J. (eds.), *Physiological Testing of the High-Performance Athlete*, 2nd ed., Human Kinetics, 1991 | — (ISBN 978-0-87322-300-3) | Foundation |
| Calvert, T.W. et al. "A systems model of the effects of training on physical performance." *IEEE Transactions on Systems, Man, and Cybernetics*, 1976 | 10.1109/TSMC.1976.5409179 | Foundation |
| Busso, T. et al. "A systems model of training responses and its relationship to hormonal responses in elite weight-lifters." *European Journal of Applied Physiology*, 1990 | 10.1007/BF00236693 | Foundation |
| Busso, T. "Variable dose-response relationship between exercise training and performance." *Medicine & Science in Sports & Exercise*, 2003 | 10.1249/01.MSS.0000074465.13621.37 | Foundation |
| Taha, T. & Thomas, S.G. "Systems modelling of the relationship between training and performance." *Sports Medicine*, 2003 | 10.2165/00007256-200333140-00003 | Foundation |
| Hellard, P. et al. "Assessing the limitations of the Banister model in monitoring training." *Journal of Sports Sciences*, 2006 | 10.1080/02640410500244697 | Foundation |
| Halson, S.L. et al. "Time course of performance changes and fatigue markers during intensified training in trained cyclists." *Journal of Applied Physiology*, 2002 | 10.1152/japplphysiol.01164.2001 | Parameter support |
| Kontro, H. et al. "The three-dimensional impulse-response model: Modeling the training process in accordance with energy system-specific adaptation." *PLoS ONE*, 2026 | 10.1371/journal.pone.0341721 | Foundation |

## VO₂max and performance prediction

| Reference | DOI | Role |
|---|---|---|
| Daniels, J. & Gilbert, J. "Oxygen Power: Performance Tables for Distance Runners." Tempe, AZ: Oxygen Power, 1979 | — | Foundation |
| Daniels, J. "Daniels' Running Formula." 3rd ed., Human Kinetics, 2014 | — (ISBN 978-1-4504-3183-5) | Foundation |
| Helgerud, J. et al. "Aerobic high-intensity intervals improve VO₂max more than moderate training." *Medicine & Science in Sports & Exercise*, 2007 | 10.1249/mss.0b013e3180304570 | Validation |

## Running injury epidemiology

| Reference | DOI | Role |
|---|---|---|
| Videbæk, S. et al. "Incidence of running-related injuries per 1000 h of running in different types of runners: A systematic review and meta-analysis." *Sports Medicine*, 2015 | 10.1007/s40279-015-0333-8 | Parameter support |
| Kluitenberg, B. et al. "What are the differences in injury proportions between different populations of runners? A systematic review and meta-analysis." *Sports Medicine*, 2015 | 10.1007/s40279-015-0331-x | Parameter support |
| Buist, I. et al. "No Effect of a Graded Training Program on the Number of Running-Related Injuries in Novice Runners: A Randomized Controlled Trial." *American Journal of Sports Medicine*, 2008 | 10.1177/0363546507307505 | Parameter support |
| Kemler, E. et al. "Differences in injury risk and characteristics of injuries between novice and experienced runners over a 4-year period." *The Physician and Sportsmedicine*, 2018 | 10.1080/00913847.2018.1507410 | Parameter support |
| Frandsen, J. et al. "How much running is too much? Identifying high-risk running sessions in a 5200-person cohort study." *British Journal of Sports Medicine*, 2025 | 10.1136/bjsports-2024-109380 | Parameter support |
| Nielsen, R.Ø. et al. "Classifying running-related injuries based upon etiology, with emphasis on volume and pace." *International Journal of Sports Physical Therapy*, 2013 | — (PMID 23593555) | Foundation |
| Malisoux, L. et al. "Can parallel use of different running shoes decrease running-related injury risk?" *Scandinavian Journal of Medicine & Science in Sports*, 2015 | 10.1111/sms.12154 | Foundation |

## Training load and dose-response

| Reference | DOI | Role |
|---|---|---|
| Foster, C. et al. "A new approach to monitoring exercise training." *Journal of Strength and Conditioning Research*, 2001 | 10.1519/1533-4287(2001)015<0109:ANATME>2.0.CO;2 | Foundation |
| Bache-Mathiesen, L.K. et al. "Not straightforward: modelling non-linearity in training load and injury research." *BMJ Open Sport & Exercise Medicine*, 2021 | 10.1136/bmjsem-2021-001119 | Foundation |
| Bache-Mathiesen, L.K. et al. "Assessing the cumulative effect of long-term training load on the risk of injury in team sports." *BMJ Open Sport & Exercise Medicine*, 2022 | 10.1136/bmjsem-2022-001342 | Foundation |

## Adherence and compliance

| Reference | DOI | Role |
|---|---|---|
| Polar Electro Oy. "Polar Data Reveals Training 'Harder' Isn't Always Smarter." Press release, 6 June 2018 | — | Parameter support |
| Ranieri, L.E. et al. "Comparison of Heart Rate- and Race Pace-Based Training Prescriptions on Training Execution Accuracy in Recreational Distance Runners." *International Journal of Sports Physiology and Performance*, 2026 | 10.1123/ijspp.2025-0578 | Foundation |
| Santos, A. et al. "Rates of compliance and adherence to high-intensity interval training: a systematic review and meta-analyses." *International Journal of Behavioral Nutrition and Physical Activity*, 2023 | 10.1186/s12966-023-01535-w | Parameter support |
| Gavanda, S. et al. "Optimizing Resistance Training Outcomes: Comparing In-Person Supervision, Online Coaching, and Self-Guided Approaches: A Randomized Controlled Trial." *Journal of Strength and Conditioning Research*, 2025 | 10.1519/JSC.0000000000005216 | Parameter support |

The adherence class distributions are supported by these studies in *direction* (supervised > app-guided > static delivery) but not in magnitude: Santos et al. pool HIIT interventions in insufficiently active adults and adults with a medical condition, and Gavanda et al. report a resistance-training context (n = 79). No running-specific adherence study by delivery form exists. The class magnitudes are therefore engineering defaults with directional support — see the Simulator white paper and the README of this repository, which state this the same way.

## Individual heterogeneity in injury risk

| Reference | DOI | Role |
|---|---|---|
| Macis, A. "The role of the frailty in the evaluation of injury risk factors for National Basketball Association players." *Computational Statistics*, 2025 | 10.1007/s00180-024-01556-4 | Parameter support |
| Hespanhol Junior, L.C., Costa, L.O.P. & Lopes, A.D. "Previous injuries and some training characteristics predict running-related injuries in recreational runners: a prospective cohort study." *Journal of Physiotherapy*, 2013 | 10.1016/S1836-9553(13)70203-0 | Parameter support |

Macis provides the empirical anchor for modeling between-individual variation in injury susceptibility as a Gamma-distributed frailty term. The population is professional basketball, not recreational running; the study supports the *form*. Hespanhol Junior et al. — a 12-week prospective cohort of 191 recreational runners with a full injury-count distribution (0/1/2/3/4 injuries per runner) — corroborates the magnitude at order-of-magnitude level in the target population (QDOT Caveat Register A1).

## Intensity distribution

| Reference | DOI | Role |
|---|---|---|
| Seiler, S. & Kjerland, G.Ø. "Quantifying training intensity distribution in elite endurance athletes: is there evidence for an 'optimal' distribution?" *Scandinavian Journal of Medicine & Science in Sports*, 2006 | 10.1111/j.1600-0838.2004.00418.x | Foundation |
| Stöggl, T. & Sperlich, B. "Polarized training has greater impact on key endurance variables than threshold, high intensity, or high volume training." *Frontiers in Physiology*, 2014 | 10.3389/fphys.2014.00033 | Validation |
| Esteve-Lanao, J. et al. "Impact of training intensity distribution on performance in endurance athletes." *Journal of Strength and Conditioning Research*, 2007 | 10.1519/R-19725.1 | Validation |
| Muñoz, I. et al. "Does polarized training improve performance in recreational runners?" *International Journal of Sports Physiology and Performance*, 2014 | 10.1123/ijspp.2012-0350 | Validation |
| Carnes, A.J. & Mahoney, S.E. "Polarized versus high-intensity multimodal training in recreational runners." *International Journal of Sports Physiology and Performance*, 2019 | 10.1123/ijspp.2018-0040 | Validation |
| Vesterinen, V. et al. "Predictors of individual adaptation to high-volume or high-intensity endurance training in recreational endurance runners." *Scandinavian Journal of Medicine & Science in Sports*, 2016 | 10.1111/sms.12530 | Validation |

## Wearable sensor accuracy

| Reference | DOI | Role |
|---|---|---|
| Bent, B. et al. "Investigating sources of inaccuracy in wearable optical heart rate sensors." *npj Digital Medicine*, 2020 | 10.1038/s41746-020-0226-6 | Foundation |

---

*Part of the validation documentation for Runapp. The framework this evidence informs: [The Runapp Training Simulator](../whitepapers/simulator.md). The overview: [README](../README.md). QDOT's own register: [Evidence Register: QDOT](qdot-evidence-register.md).*
