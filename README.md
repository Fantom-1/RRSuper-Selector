# SupeRR Selector — Pressure Performance Analysis

An explainable, reproducible cricket analytics project for identifying batters and bowlers who deliver reliably under pressure in T20 cricket.

## Objective
Produce two evidence-backed rankings:
- Top 10 batters under pressure
- Top 10 bowlers under pressure

The ranking must distinguish raw output from context-adjusted contribution, account for role and opportunity, quantify uncertainty, and remain understandable to non-technical stakeholders.

## Current status
This repository is the project workspace and methodology foundation. The analysis playbook, literature review, metric design principles, communication standard, and data-handling rules are documented under `docs/`.

**No player ranking is final until the supplied data has been re-audited, the pressure definition has been tested, and the metrics have passed validation and sensitivity checks.**

## Analytical principles
1. Define pressure from match state, not merely the over number.
2. Compare players with appropriate role- and phase-specific baselines.
3. Measure contribution relative to expectation.
4. Separate performance from sample size and uncertainty.
5. Avoid double-counting correlated statistics.
6. Keep batter and bowler scorecards interpretable.
7. Validate rankings across reasonable alternative assumptions.
8. Preserve a traceable path from source delivery to final score.

## Project structure
```
.
├── README.md
├── .gitignore
├── data/
│   └── README.md
└── docs/
    ├── analysis_playbook.md
    ├── literature_review.md
    ├── metric_design.md
    └── stakeholder_communication.md
```

The implementation structure will expand after the data audit and metric specification are frozen.

## Reproducibility
- Record dataset provenance, version, filters, and row counts.
- Keep raw challenge data out of Git unless its licence and challenge terms explicitly permit redistribution.
- Store experiment parameters and seeds.
- Version the pressure definition and ranking methodology.
- Report uncertainty and sensitivity alongside ranks.

## Disclaimer
This project estimates performance from recorded match events. It does not directly measure a player's psychology, temperament, or mental strength. "Under pressure" refers to objectively defined match situations.
