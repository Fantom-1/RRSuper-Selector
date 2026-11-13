# Professional Cricket Analysis Playbook

## 1. Purpose

Build a defensible process for identifying players who maintain or improve their contribution in demanding T20 match situations. The aim is decision support for selectors, not a black-box prediction or a claim to measure a player's mental state.

## 2. How high-performance analysis is organised

Professional analysis is a decision-support function. Public accounts from franchise and county analysts describe a cycle spanning scouting, opposition preparation, match-up analysis, live coding, post-match review, coach communication, player development, and recruitment/auction support.

We adapt that cycle into five repeatable stages:

1. **Prepare:** audit data, define player roles, establish competition and season context.
2. **Understand the game:** reconstruct each delivery's match state and available resources.
3. **Measure:** compare each player's contribution with a fair expectation for the same role and situation.
4. **Challenge:** test alternative pressure definitions, baselines, sample thresholds, and ranking stability.
5. **Communicate:** provide a score, evidence, uncertainty, and a plain-language explanation.

## 3. Analyst questions

### Batter
- What was the player's role and batting position?
- How many balls and wickets remained when they entered?
- Was the side chasing, setting a target, rebuilding, or accelerating?
- How did the required rate and resources change?
- Did the batter score faster or preserve resources better than a comparable batter?
- Did the contribution improve the team's state, or merely add runs after the contest was nearly decided?
- How many independent pressure innings support the estimate?

### Bowler
- What phase and role did the bowler operate in?
- What was the state of the innings before the spell?
- How many runs would a comparable bowler be expected to concede in this state?
- Did the bowler create dot balls, prevent boundaries, take credited wickets, or restrict the opponent's options?
- Were wickets attributable to the bowler? Run-outs must not be credited as bowler wickets.
- How many pressure overs and distinct matches support the estimate?

## 4. Match-state reconstruction

For every delivery, reconstruct at minimum:
- match, competition, season, innings, batting team, bowling team
- legal-ball number and legal balls remaining
- score and wickets lost before the delivery
- target and runs required, where applicable
- required run rate and current scoring rate
- innings phase (powerplay, middle, death; exact definitions documented)
- striker, non-striker, bowler, batting position
- delivery runs, batter runs, extras, wicket and dismissal type
- bowler type/pace-spin classification where reliable

Use the pre-delivery state to calculate the pressure and expectation for that delivery. Do not use the outcome of the current ball to define the pressure that supposedly preceded it.

## 5. Pressure: a multi-signal concept

Pressure is not synonymous with "death overs". It can arise early when a team loses several wickets, or late when a chase becomes difficult.

Candidate signals:
- **Resource-adjusted chase difficulty:** required runs relative to remaining balls and wickets.
- **Wicket vulnerability:** wickets remaining and recent wicket-loss pattern.
- **Scoring demand:** required rate relative to a phase- and resource-aware expected rate.
- **First-innings demand:** score relative to a competition/venue/season par expectation, with wickets and balls remaining.
- **Leverage:** how consequential the delivery is to the match state.

The first implementation should be a transparent pressure score based on standardised, bounded components. A win-probability model or pressure-index formulation can be evaluated as an alternative, but only if its inputs and calibration are defensible.

Do not call a delivery "high pressure" solely because it occurred in overs 16–20. Use phase as context, not the whole definition.

## 6. Expected-performance baselines

Estimate expected batter and bowler performance from comparable historical situations. Baselines should be stratified or model-adjusted by:
- batting position / role
- innings phase
- pressure band or continuous pressure score
- competition and season
- innings number and chase/set context
- opponent quality where sample size supports it
- pace/spin or bowling type where relevant

Avoid overly narrow groups that create tiny samples. Use hierarchical pooling or shrinkage when a cohort is sparse.

## 7. Contribution, not just outcomes

Preferred conceptual measure: **observed contribution minus expected contribution**.

Possible event-value approaches:
- change in expected runs from the match state before to after the delivery
- change in win probability, if a properly calibrated model is available
- runs above/below a context-specific expected baseline

The event-value model must be validated and must not attribute fielding errors or run-outs incorrectly to the bowler. If the dataset lacks enough state information to estimate a component credibly, omit it rather than inventing it.

## 8. Player-level reliability

Aggregate delivery or innings contributions, then report:
- mean contribution per pressure opportunity
- total contribution
- number of pressure innings/overs/matches
- uncertainty interval
- shrinkage-adjusted estimate
- consistency across matches
- split by role/phase/competition

A player with a very high average over a handful of opportunities should not automatically outrank a player with a strong, repeatable record over many opportunities.

## 9. Validation and challenge tests

At minimum:
- data integrity tests for legal balls, extras, wickets, innings and match joins
- compare pressure definitions (continuous, quantile bands, published index-inspired)
- compare simple role baselines against richer models
- test multiple reasonable pressure thresholds
- leave-one-season-out or chronological validation where feasible
- bootstrap at match or innings level, not individual delivery level alone
- report rank correlation and Top-10 overlap across specifications
- investigate players whose ranks change materially
- check that rankings are not driven by a single innings, opponent, venue or season

Do not tune the methodology solely to produce a preferred list of players.

## 10. Deliverables

1. Data audit and data dictionary.
2. Pressure definition and sensitivity report.
3. Batter scorecard and bowler scorecard.
4. Final Top 10 lists with uncertainty and evidence.
5. Methodology report for technical reviewers.
6. One-page stakeholder explainer with plain-language examples.
7. Reproducible code, parameters, and tests.
