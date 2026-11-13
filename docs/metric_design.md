# Metric Design: Pressure-Adjusted Player Reliability

## 1. Design objective

Create separate batter and bowler ratings that answer:

> How much better or worse did this player perform than a comparable player would be expected to perform in the same demanding match situations, and how certain are we?

The working name is **Pressure-Adjusted Player Reliability (PAPR)**. This is a proposed project metric, not an established cricket statistic.

## 2. Core architecture

1. Reconstruct pre-delivery match state.
2. Estimate pressure from state and resources.
3. Estimate expected performance for a comparable role/context.
4. Calculate observed-minus-expected contribution.
5. Aggregate across opportunities.
6. Apply reliability adjustment and uncertainty.
7. Test rank stability.

## 3. Pressure components

Candidate signals, each scaled to a common interpretable range:
- chase demand: required run rate relative to resource-adjusted expected scoring rate
- resource scarcity: balls and wickets remaining
- wicket stress: recent wicket loss and wickets remaining
- first-innings demand: score relative to a competition/venue/season par curve
- match leverage: change in win probability, only if calibrated

Do not add these blindly. Check correlation, redundancy, and availability. The first release should use a small transparent set of components and publish its formula and sensitivity tests.

## 4. Batter contribution candidates

- pressure runs above expected
- pressure scoring rate above expected
- boundary and rotation contribution relative to expected
- dismissal cost / survival value where state-value estimation supports it
- role and phase adjustments

Avoid summing strike rate, boundaries and runs as if independent: these overlap. Prefer an event-value measure as the primary component, with the others as explanatory diagnostics.

## 5. Bowler contribution candidates

- runs prevented relative to expected for the same phase/state
- dot-ball value relative to expected
- credited wickets and their state-dependent value
- boundary prevention relative to expected
- legal-ball economy and extras

Run-outs are not bowler wickets. Wides/no-balls must be handled correctly in legal-ball and over denominators. Do not credit a bowler for a dismissal type that rules/data attribution do not assign to the bowler.

## 6. Common event-value formulation

If a validated state-value model is available:

**Batter delivery value** = batter runs + expected future runs after the delivery − expected future runs before the delivery.

**Bowling delivery value** = expected future runs before the delivery − (runs conceded + expected future runs after the delivery), with explicit treatment of wicket value and attribution.

These are conceptual definitions. The implementation must account for extras, legal balls, dismissals, innings termination, and the fact that batting and bowling perspectives are opposite sides of the same event. Do not double-count the same run or wicket in a combined score.

If state-value modelling is not adequately supported by the dataset, use role/phase-specific expected runs and wicket baselines as the transparent first version.

## 7. Role-aware expectations

Potential cohorts:
- batting position bands / role groups
- powerplay, middle, death
- first innings vs chase
- pace vs spin and bowling role
- competition / season / venue where data supports it

Cohorts must be large enough. Use partial pooling/shrinkage rather than fragile micro-groups.

## 8. Reliability and uncertainty

Report at least:
- raw mean pressure contribution per opportunity
- total pressure contribution
- number of pressure innings / overs / matches
- shrinkage-adjusted estimate
- interval or uncertainty band
- consistency and sensitivity

A simple empirical-Bayes or hierarchical shrinkage approach is preferred to a hard arbitrary minimum. Bootstrap at innings or match level to preserve within-match dependence.

## 9. Ranking policy

- Rank batters and bowlers separately.
- Show a primary ranking and supporting diagnostic columns.
- Consider role group and competition splits before any cross-role aggregation.
- Include an eligibility rule based on minimum opportunity and uncertainty, specified before looking at final names.
- If evidence is insufficient, label a player "provisional" rather than forcing a precise rank.

## 10. Validation gates

- Compare pressure-only ranking with conventional metrics and role-adjusted baseline.
- Evaluate predictive/calibration properties only if a future outcome target is defined and held out chronologically.
- Test alternative pressure specifications and cohort definitions.
- Use leave-one-season-out checks where possible.
- Report Top-10 overlap and rank correlation across specifications.
- Flag ranking changes caused by low sample, a single match, or one competition.
- Keep a versioned record of all final metric choices.
