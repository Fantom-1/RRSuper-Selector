# Literature Review: Player Performance and Pressure

This is a working evidence map, not an exhaustive systematic review. Papers are grouped by the idea they contribute. Publication dates and access links should be rechecked before final submission.

## A. Directly relevant cricket research

### 1. Match analysis trends in limited-overs professional cricket: A systematic review of technical and tactical performance (2026)
- Authors: Akash Gangadharan Nair Ramanan et al.
- DOI: https://doi.org/10.1177/17479541261439184
- Link: https://journals.sagepub.com/doi/10.1177/17479541261439184
- Why it matters: Recent systematic review of 47 studies (2007–2024), covering technical and tactical indicators in limited-overs cricket.
- Takeaway: Move beyond static averages to contextual indicators such as phase, pressure, match-ups, game state and win probability. The review also flags a gap between analytical sophistication and practical use.
- Use here: Literature foundation and rationale for context-aware, coach-readable metrics.

### 2. A win-based measure of player productivity in cricket: evidence from the Women's Big Bash League between 2016/17 and 2025/26 (2026)
- DOI: https://doi.org/10.1080/23750472.2026.2747309
- Why it matters: Recent Cricket Win Score (CWS) framework decomposes player productivity and links batting/bowling contribution to team winning percentage.
- Reported validation: Abstract reports comparison with realised wins, Pythagorean expected wins and cricWAR, including strong player-level rank agreement.
- Use here: Important benchmark for testing whether event-level contribution aggregates to meaningful team outcomes. Do not copy its coefficients without inspecting the full method and checking compatibility with our data.

### 3. A pressure index for the team batting second in T20I cricket (2024)
- Authors: Don K. Mallawa Arachchi, Ananda B. Manage, Stephen M. Scariano.
- DOI: https://doi.org/10.3233/JSA-240792
- Link: https://journals.sagepub.com/doi/full/10.3233/JSA-240792
- Why it matters: Defines chase pressure using required rate relative to remaining resources and models pressure evolution.
- Use here: A principled alternative pressure formulation for second innings. Limitation: its stated focus is the chasing team, so it does not by itself solve first-innings pressure.

### 4. Modelling player ratings in One Day International cricket using the Modified Duckworth-Lewis method (published 2023; journal issue 2024)
- DOI: https://doi.org/10.1093/imaman/dpad014
- Link: https://academic.oup.com/imaman/article/35/2/267/7242576
- Why it matters: Uses match-state/resource modelling to value player contributions, accounting for pressure and pitch effects; can compare batting, bowling and all-round contributions.
- Use here: Strong methodological precedent for state-dependent player ratings. Adapt to T20 only after testing the resource model against our competition data.

### 5. A new in-form and role-based Deep Player Performance Index for player evaluation in T20 Cricket (2022)
- Authors: C. Deep Prakash, Sanjay Verma.
- DOI: https://doi.org/10.1016/j.dajour.2022.100025
- Link: https://www.sciencedirect.com/science/article/pii/S2772662222000029
- Why it matters: Proposes a T20 player index using role and current form, with K-Means and Random Forest.
- Use here: Baseline comparator, not the final design. Our challenge needs a pressure-specific, more transparent approach; avoid treating a clustering/classification pipeline as proof of player value.

### 6. Player evaluation in Twenty20 cricket (2015)
- Authors: Jack Davis, Harsha Perera, Tim B. Swartz.
- DOI: https://doi.org/10.3233/JSA-150002
- Link: https://journals.sagepub.com/doi/10.3233/JSA-150002
- Why it matters: Expected run differential relative to a role-specific standard player.
- Use here: Direct support for role-aware expected contribution instead of raw averages.

### 7. Quantifying the pressure on the teams batting or bowling in the second innings of limited overs cricket matches (2016)
- Authors: Dibyojyoti Bhattacharjee, Hermanus H. Lemmer.
- DOI: https://doi.org/10.1177/1747954116667106
- Link: https://journals.sagepub.com/doi/10.1177/1747954116667106
- Why it matters: Methods to quantify second-innings pressure and individual batting/bowling contributions, partnerships and turning points.
- Use here: Historical pressure-analysis comparator.

### 8. Rating players in test match cricket (2014 online; 2015 journal volume)
- Authors: Sohail Akhtar, Philip Scarf, Zahid Rasool.
- DOI: https://doi.org/10.1057/jors.2014.30
- Link: https://link.springer.com/article/10.1057/jors.2014.30
- Why it matters: Models match outcome probabilities and allocates batting, bowling and fielding contribution through state changes.
- Use here: Conceptual precedent for common outcome-based value across different disciplines. Test-cricket assumptions need adaptation.

### 9. Novel Performance Metrics to Evaluate the Duel Between a Batsman and a Bowler (2020)
- DOI: https://doi.org/10.1177/0258042X20912597
- Link: https://journals.sagepub.com/doi/10.1177/0258042X20912597
- Why it matters: Emphasises balls remaining, wickets, opponent skill and context in batter-bowler evaluation.
- Use here: Match-up analysis as a secondary diagnostic, not a standalone pressure ranking.

## B. Transferable ideas from other sports

### 10. Baseball: Run Expectancy / RE24
- FanGraphs explainer: https://library.fangraphs.com/misc/re24/
- Idea: Estimate expected runs for each base-out state; value an action by how much it changes expected runs, including the runs scored.
- Cricket adaptation: Construct a T20 state-value table from score, balls and wickets remaining. A delivery's run value can be measured as actual runs plus next-state expected runs minus pre-delivery expected runs.
- Caveat: Cricket has different resources, innings structure and two-sided batter/bowler actions; build a cricket-specific state space.

### 11. Baseball: Wins Above Replacement (WAR)
- FanGraphs explainer: https://library.fangraphs.com/misc/war/
- Idea: Express player value relative to a defined replacement-level player, combining multiple contributions.
- Cricket adaptation: Use role-specific replacement/standard baselines to contextualise a player's value. For this challenge, pressure-adjusted value above a role baseline is more directly relevant than importing WAR literally.
- Caveat: Replacement-level definitions and cross-role aggregation are contentious; avoid a single magic number without validation.

### 12. Football: Expected Goals and context adjustment
- Expected goals in football: Improving model performance and demonstrating value (2023): https://pmc.ncbi.nlm.nih.gov/articles/PMC10075453/
- Adjusting expected goals (xG) and shots on target for game context in soccer (2026): https://doi.org/10.1177/22150218261454824
- Idea: Compare outcomes with event-level expectations, and explicitly model how match context changes the opportunity.
- Cricket adaptation: Estimate expected runs/wicket probability from pre-delivery state, batter/bowler/phase context, then value residual contribution.
- Caveat: Expected outcomes are not the same as player skill; ensure calibration and avoid leakage.

### 13. Basketball: Regularized Adjusted Plus-Minus (RAPM)
- Revisiting player contributions in regularized adjusted plus-minus models (2026): https://doi.org/10.1515/jqas-2024-0138
- Idea: Use regularised models to separate player contributions while accounting for teammates/opponents and lineup context.
- Cricket adaptation: Consider opponent and team context as adjustments in a later model, but do not begin with a complex regression if the sample is too sparse.
- Caveat: Team-sport interaction effects and identifiability challenges differ from cricket's delivery-level structure.

### 14. Football: Player action value / threat generation
- Generation of threat: crediting football players for creating dangerous actions in an unbiased way (2025): https://doi.org/10.1515/jqas-2024-0107
- Idea: Value actions by how they change the threat state, including indirect contributions.
- Cricket adaptation: Value a delivery by how it changes scoring opportunity and match leverage, rather than crediting only boundaries and wickets.
- Caveat: Our dataset may not contain enough tracking/field-position information for full action-value models.

## C. Recommended reading order

1. 2026 limited-overs systematic review — map the field.
2. Davis et al. (2015) — role-based expected run differential.
3. Mallawa Arachchi et al. (2024) — chase pressure.
4. Modified Duckworth-Lewis player ratings (2023/2024) — state-dependent value.
5. Bhattacharjee & Lemmer (2016) — pressure and individual contribution.
6. Cricket Win Score (2026) — recent win-linked productivity validation.
7. RE24 and WAR explainers — transferable player-value concepts.
8. Soccer xG and NBA RAPM papers — expected-event value and contextual adjustment.

## D. What we should not do

- Copy a published pressure formula without checking its target format and innings coverage.
- Use the 2022 DPPI as the only baseline when newer contextual methods exist.
- Treat a high-pressure strike rate or economy rate as a complete player rating.
- Train an opaque model and then explain its output with post-hoc feature importance alone.
- claim psychological composure from ball-by-ball outcomes.


## E. Additional high-priority 2025–2026 research

### 15. Impact ranking methodologies in limited-overs cricket: A systematic review of performance metrics (2025)
- DOI: https://doi.org/10.1177/17479541251321477
- Link: https://journals.sagepub.com/doi/abs/10.1177/17479541251321477
- Why it matters: Reviews recent player-impact ranking approaches across batting, bowling and fielding, and critiques the limitations of traditional runs/wickets/averages.
- Use here: Use as a comparison map for ranking families and their assumptions.

### 16. Applications of higher order Markov models and Pressure Index to strategize controlled run chases in Twenty20 cricket (2026)
- Authors: Rhitankar Bandyopadhyay, Dibyojyoti Bhattacharjee.
- DOI: https://doi.org/10.1177/17479541261430809
- Link: https://journals.sagepub.com/doi/10.1177/17479541261430809
- Why it matters: Uses ball-by-ball second-innings states, Pressure Index and higher-order Markov chains over 6,537 T20 matches; the abstract reports open-source data availability through ESPNcricinfo and Cricsheet.
- Use here: Recent T20-specific comparator for pressure trajectories and state transitions. Evaluate whether its pressure-index range and assumptions transfer to our data. It is a chase-strategy paper, not a complete batter/bowler ranking method.

### 17. Modeling the joint influence of key factors on score contribution and ball utilization in limited-overs cricket for ranking player and team batting performance (2026)
- DOI: https://doi.org/10.1177/17479541261451123
- Link: https://journals.sagepub.com/doi/10.1177/17479541261451123
- Why it matters: Uses a joint beta mixed-effects model to represent the relationship between score contribution and ball utilization, including batting position and experience.
- Use here: A useful reminder that runs and ball usage are related outcomes and should not be blindly combined as independent weighted features. It is batting-focused and does not directly solve pressure-adjusted bowling rankings.

### 18. A win-based measure of player productivity in cricket: evidence from the Women's Big Bash League between 2016/17 and 2025/26 (2026)
- Author: Sarthak Mondal.
- DOI: https://doi.org/10.1080/23750472.2026.2747309
- Link: https://www.tandfonline.com/doi/full/10.1080/23750472.2026.2747309
- Why it matters: Proposes Cricket Win Score (CWS), a role-aware decomposition linking batting and bowling productivity to team winning percentage. The paper reports WBBL-only validation across ten seasons and compares with realised wins, Pythagorean expected wins and cricWAR.
- Reported results: Abstract reports team-level correlation 0.852 and player-level Spearman rank correlations 0.912 for batters and 0.973 for bowlers against cricWAR. These are the authors' reported results, not results independently reproduced by this project.
- Use here: A key contemporary benchmark. Read the full equations and limitations before implementing. It is not a pressure-specific metric, and the WBBL-only evidence does not establish validity for men's IPL or our challenge dataset.

### 19. Match analysis trends in limited-overs professional cricket: A systematic review of technical and tactical performance (2026)
- DOI: https://doi.org/10.1177/17479541261439184
- Link: https://journals.sagepub.com/doi/10.1177/17479541261439184
- Why it matters: PRISMA review of 47 studies from 2007–2024. It describes the shift from static aggregates toward contextual indicators including pressure, phases, match-ups, game state and win probability, while identifying limitations in research-practice integration.
- Use here: Anchor our justification for combining technical and tactical measures and translating them into coach-facing outputs.

## F. Professional practice references (not peer-reviewed research)

These are practitioner interviews and industry accounts. They inform workflow design, not statistical validity.

- **Mumbai Indians team analyst L. Varun (2023):** https://www.mumbaiindians.com/news/l-varun-team-analyst-mi-have-been-trendsetters-in-how-data-is-consumed-by-coaches-and-players — describes year-round scouting support, player tracking, auction analysis, and pre-game / in-game / post-game workflows. Emphasises contextual, visual delivery to coaches and players.
- **ASPA: Inside Professional Cricket Analysis (7 October 2026):** https://theaspa.org/news-%26-articles/f/ask-the-analyst-inside-professional-cricket-analysis?blogcategory=Articles — Hampshire analyst Tom Merrill discusses opposition preparation, live coding, video, coach communication and post-match feedback. Explicitly distinguishes deeper internal analysis from simpler player-facing communication.
- **Cricket Ireland interview with analyst Scott Irvine:** https://cricketireland.ie/news/interview-scott-irvine-on-coding-balls-lords-and-thieving-monkeys/ — describes opponent preparation, match-up information, video/statistical support and review.
- **Mumbai Indians scouting report (Indian Express, 2023):** https://indianexpress.com/article/sports/ipl/how-extensive-scouting-and-diligent-scouts-have-made-mumbai-indians-the-superstar-team-they-are-8629243/ — describes multi-season tracking, data plus human scouting, and assessing match readiness and crunch-game performance.

## G. Refined reading order

1. 2026 limited-overs systematic review — establish the field and known limitations.
2. Davis et al. (2015) — role-based expected run differential.
3. Modified Duckworth–Lewis player ratings (2023/2024) — state-dependent valuation and cross-discipline comparison.
4. Mallawa Arachchi et al. (2024) — T20I chase pressure.
5. Bandyopadhyay & Bhattacharjee (2026) — recent T20 pressure trajectories and Markov states.
6. Mondal (2026) — Cricket Win Score and win-based validation.
7. 2025 impact-ranking systematic review — compare ranking families.
8. Chathurangi et al. (2026) — joint score contribution / ball utilization.
9. RE24, WAR, xG and RAPM — transferable ideas, not formulas to import unchanged.
