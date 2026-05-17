# Practice Q&A — Intermediate

Analysis, comparison, and applied reasoning questions. Questions 71 through 140.

## Q71. How does spurious correlation differ from genuine causation, and what methods can distinguish the two?

**Level:** Intermediate

Spurious correlation occurs when two variables appear statistically related due to a third confounding variable or pure chance, without any direct causal link. Genuine causation requires that changes in one variable consistently and mechanically produce changes in another. Methods such as randomized controlled experiments, instrumental variables, and natural experiments help isolate causal effects by removing the influence of confounders. Researchers also use temporal ordering tests and domain knowledge to validate causal claims.

**Real-life applications:**
- Diagnosing whether marketing spend drives sales or both are driven by seasonality
- Separating economic growth from stock market returns in investment analysis
- Identifying whether employee training improves performance or high performers self-select into training
- Distinguishing whether product price reductions cause volume increases or demand shifts cause both

**Key concepts:** `confounding variable`, `spurious correlation`, `causal identification`, `endogeneity`, `randomization`

---

## Q72. Why is randomization considered the gold standard for causal inference?

**Level:** Intermediate

Randomization assigns subjects to treatment and control groups by chance, ensuring that both observed and unobserved confounders are balanced across groups on average. This balance means any subsequent difference in outcomes can be attributed causally to the treatment rather than pre-existing differences. Without randomization, selection bias makes it difficult to isolate the treatment effect from background characteristics. Randomization also allows straightforward statistical inference using standard hypothesis tests.

**Real-life applications:**
- Drug efficacy trials in pharmaceutical companies
- A/B testing new website features for unbiased conversion rate estimates
- Policy pilots that randomly assign subsidies to businesses
- Randomized pricing experiments to understand customer elasticity

**Key concepts:** `randomization`, `selection bias`, `treatment effect`, `control group`, `balance`

---

## Q73. What are the key assumptions required for a valid A/B test in a business context?

**Level:** Intermediate

Valid A/B tests require random assignment of units to treatment and control, independence between units so one user's experience does not affect another's (stable unit treatment value assumption, SUTVA), a pre-specified primary metric, and sufficient statistical power to detect meaningful effects. The test must also run for a sufficient duration to capture weekly cycles and avoid novelty effects. Violations of these assumptions, such as network effects or peeking at results mid-test, inflate false positive rates.

**Real-life applications:**
- E-commerce checkout flow experiments where purchases can be influenced by social proof
- Email campaign tests requiring separate recipient lists
- Mobile app feature tests where family-sharing accounts may violate independence
- Pricing experiments in marketplaces with two-sided network effects

**Key concepts:** `SUTVA`, `statistical power`, `network effects`, `peeking`, `sample size`

---

## Q74. How does multicollinearity affect regression-based causal inference?

**Level:** Intermediate

Multicollinearity occurs when predictor variables are highly correlated with each other, inflating the variance of coefficient estimates and making it difficult to isolate the individual causal effect of each regressor. While it does not bias estimates, it produces wide confidence intervals, reducing precision and making causal conclusions unreliable. Detecting multicollinearity via variance inflation factors (VIF) and addressing it through variable selection, dimensionality reduction, or ridge regression helps improve inferential quality. In causal inference, the core concern is whether the treatment variable is well-identified given the collinear controls.

**Real-life applications:**
- Separating the effect of price and promotional spend when both are correlated in retail data
- Disentangling individual salesperson attributes when tenure and experience move together
- Measuring the impact of training hours versus team support in HR analytics
- Attribution modeling in digital marketing where channels are correlated

**Key concepts:** `multicollinearity`, `variance inflation factor`, `coefficient bias`, `ridge regression`, `identification`

---

## Q75. What is the parallel trends assumption in difference-in-differences, and how would you test it?

**Level:** Intermediate

The parallel trends assumption states that in the absence of treatment, the treated and control groups would have followed the same trajectory over time. It is untestable in the post-treatment period but can be partially validated by examining pre-treatment trends using event study plots or placebo tests. If treated and control groups trend together before the intervention, the assumption becomes more plausible. Researchers also use flexible regression models with group-time fixed effects to detect pre-trend violations.

**Real-life applications:**
- Evaluating the effect of a minimum wage increase using states that did not change wages as controls
- Measuring a loyalty program rollout against stores where the program was not launched
- Assessing the impact of a factory closure on local employment using similar counties as controls
- Studying the effect of a data breach on customer churn with non-breached competitors as the control

**Key concepts:** `parallel trends`, `event study`, `placebo test`, `pre-treatment trends`, `fixed effects`

---

## Q76. How does heterogeneity in treatment effects complicate the interpretation of average treatment effects?

**Level:** Intermediate

When treatment effects vary across individuals or subgroups, a single average treatment effect (ATE) may mask important variation. For example, a new pricing strategy may benefit price-sensitive customers while harming loyal ones. Researchers decompose heterogeneous effects using subgroup analyses, quantile treatment effects, or machine learning approaches like causal forests. Understanding treatment effect heterogeneity is essential for targeting interventions to subgroups where effects are largest.

**Real-life applications:**
- Personalizing marketing campaigns based on which customer segments respond most to discounts
- Identifying which employee groups benefit most from a new training program
- Targeting policy subsidies to businesses where the return on investment is highest
- Tailoring product recommendations to user segments with different engagement patterns

**Key concepts:** `heterogeneous treatment effects`, `subgroup analysis`, `causal forest`, `ATE`, `CATE`

---

## Q77. When should a business analyst prefer instrumental variables over standard regression?

**Level:** Intermediate

Standard regression produces biased estimates when the treatment variable is endogenous, meaning it is correlated with the error term due to omitted variables, measurement error, or reverse causality. Instrumental variables (IV) provide a way to isolate exogenous variation in the treatment by using an instrument that affects treatment but has no direct effect on the outcome. IV is preferred when a valid instrument exists and endogeneity is suspected. A classic example is using draft lottery numbers as an instrument for military service to study earnings effects.

**Real-life applications:**
- Using distance to college as an instrument to study the causal effect of education on wages
- Employing weather shocks as an instrument for supply to estimate demand elasticities
- Using random assignment of case load to judges as an instrument in legal economics
- Leveraging supplier cost shocks as instruments for firm pricing decisions

**Key concepts:** `endogeneity`, `instrument validity`, `exclusion restriction`, `two-stage least squares`, `local average treatment effect`

---

## Q78. What distinguishes a sharp regression discontinuity design from a fuzzy one?

**Level:** Intermediate

In a sharp regression discontinuity (RDD), treatment status changes deterministically from zero to one at a known cutoff threshold. In a fuzzy RDD, crossing the threshold only changes the probability of treatment, not the certainty. A sharp RDD directly estimates the treatment effect at the cutoff, while a fuzzy RDD requires an instrumental variables approach, using the threshold as an instrument for actual treatment. Fuzzy designs arise when compliance with treatment assignment is imperfect.

**Real-life applications:**
- Sharp RDD: scholarship eligibility based on a fixed GPA cutoff
- Fuzzy RDD: insurance enrollment programs where eligibility increases but does not guarantee take-up
- Credit score cutoffs where lenders sometimes override automatic decisions
- Regulatory compliance thresholds where firms partially respond to rules

**Key concepts:** `sharp RDD`, `fuzzy RDD`, `compliance`, `local average treatment effect`, `cutoff threshold`

---

## Q79. How does propensity score matching reduce confounding in observational studies?

**Level:** Intermediate

Propensity score matching estimates the probability of receiving treatment conditional on observed covariates and then matches treated and control units with similar propensity scores. By creating comparable groups, it mimics the balance achieved through randomization among the observed variables. The method assumes that all relevant confounders are observed (no unmeasured confounding), a strong assumption that cannot be directly tested. Matched samples are then used to estimate the average treatment effect on the treated.

**Real-life applications:**
- Comparing health outcomes of smokers and non-smokers after matching on demographics and health history
- Evaluating the effect of job training programs using matched non-participants as controls
- Studying whether early career mobility affects long-term salaries after matching on education and sector
- Assessing the impact of a product upgrade on retention by matching upgraders to similar non-upgraders

**Key concepts:** `propensity score`, `matching`, `confounding`, `overlap`, `average treatment effect on the treated`

---

## Q80. What is a natural experiment, and how does it differ from a controlled experiment?

**Level:** Intermediate

A natural experiment is a real-world event or policy change that creates quasi-random variation in treatment assignment, allowing researchers to estimate causal effects without deliberate randomization. Unlike controlled experiments, the researcher does not control who receives treatment but exploits exogenous variation created by nature, institutions, or policy. Natural experiments are more external-validity-rich than lab experiments but require careful validation that the variation is genuinely exogenous.

**Real-life applications:**
- Using border differences in minimum wage laws to study employment effects
- Exploiting lottery-based immigration visa allocation to study immigrant economic outcomes
- Leveraging random assignment of school quality due to housing lotteries
- Using weather variation as a natural experiment for studying outdoor retail sales

**Key concepts:** `quasi-random variation`, `exogeneity`, `external validity`, `natural experiment`, `policy discontinuity`

---

## Q81. How does mediation analysis help businesses understand the mechanism behind a causal effect?

**Level:** Intermediate

Mediation analysis decomposes the total causal effect of a treatment on an outcome into a direct effect and an indirect effect that operates through an intermediary variable called the mediator. Understanding the mechanism is crucial for designing more targeted interventions. For example, a discount may improve retention partly by increasing satisfaction (mediated path) and partly through direct financial incentives (direct path). The distinction informs whether a business should invest in satisfaction improvements or pricing strategies.

**Real-life applications:**
- Understanding whether a new onboarding flow improves retention through faster activation or through feature discovery
- Decomposing the effect of employee training on productivity into skill improvement and motivation channels
- Identifying whether customer service improvements drive revenue through NPS or repeat purchase
- Analyzing whether ad exposure affects conversion through brand recall or direct response

**Key concepts:** `mediation`, `direct effect`, `indirect effect`, `total effect`, `causal mechanism`

---

## Q82. What role does moderation analysis play in tailoring business strategies?

**Level:** Intermediate

Moderation analysis examines whether the effect of a treatment on an outcome varies across levels of a third variable, the moderator. When significant moderation exists, a one-size-fits-all strategy is suboptimal, and interventions should be tailored to subgroups. For instance, the effect of a discount on purchase probability may be stronger for price-sensitive customers. Moderation is typically tested by including an interaction term between the treatment and the moderator in a regression model.

**Real-life applications:**
- Testing whether a referral incentive program works better for urban than rural customers
- Checking whether employee wellness programs have stronger effects on junior versus senior staff
- Examining whether product bundling increases spend more for high-frequency versus low-frequency buyers
- Identifying whether ad format effectiveness varies by device type

**Key concepts:** `moderation`, `interaction term`, `subgroup effect`, `effect modification`, `conditional average treatment effect`

---

## Q83. How do structural equation models differ from standard regression models in causal analysis?

**Level:** Intermediate

Structural equation models (SEM) simultaneously model multiple causal pathways, including direct and indirect effects, feedback loops, and latent variables. Unlike standard regression, which estimates a single equation, SEM represents a system of equations that reflects the researcher's assumed causal structure. SEM requires explicit specification of a causal diagram and is therefore sensitive to model misspecification. It is widely used in social science and organizational research to test complex theories about how variables causally relate.

**Real-life applications:**
- Modeling how leadership style affects firm performance through employee engagement and innovation
- Testing whether customer satisfaction drives revenue both directly and through word-of-mouth referrals
- Analyzing the interplay between marketing investment, brand equity, and sales
- Studying organizational culture's impact on employee turnover via job satisfaction

**Key concepts:** `structural equation`, `latent variable`, `path analysis`, `model fit`, `causal diagram`

---

## Q84. What is the difference between the intent-to-treat (ITT) and the average treatment effect on the treated (ATT)?

**Level:** Intermediate

The intent-to-treat effect measures the causal effect of being assigned to treatment, regardless of whether subjects actually received it, preserving the benefits of randomization even under non-compliance. The average treatment effect on the treated (ATT) measures the causal effect among those who actually received the treatment. ITT is conservative and policy-relevant when non-compliance is realistic in real-world settings, while ATT is more appropriate when the goal is to evaluate the effect for compliers.

**Real-life applications:**
- Measuring the ITT effect of a health intervention where some participants drop out
- Evaluating the ATT effect of a job training program among those who completed training
- Estimating the policy-relevant effect of a subsidy that only some eligible firms claimed
- Assessing the effect of a new software tool among employees who adopted it versus all who were assigned

**Key concepts:** `intent-to-treat`, `ATT`, `non-compliance`, `complier average causal effect`, `randomization`

---

## Q85. How do you detect and handle omitted variable bias in a causal regression model?

**Level:** Intermediate

Omitted variable bias occurs when a variable that affects both the treatment and the outcome is excluded from the model, causing the treatment coefficient to absorb its effect. It is detected through economic reasoning, sensitivity analyses (such as Oster's method), or by testing whether adding plausible controls substantially changes the coefficient. Remedies include adding omitted controls if data is available, using fixed effects to control for time-invariant unobservables, or employing IV or RDD to identify causal effects exogenously.

**Real-life applications:**
- Failing to control for store traffic when estimating the effect of shelf placement on sales
- Omitting customer tenure when estimating the effect of a loyalty program on spend
- Excluding macroeconomic conditions when measuring the effect of HR programs on productivity
- Ignoring pre-existing health conditions when estimating the effect of wellness benefits on absenteeism

**Key concepts:** `omitted variable bias`, `confounding`, `sensitivity analysis`, `fixed effects`, `endogeneity`

---

## Q86. What is the local average treatment effect (LATE) and why does it matter for business decisions?

**Level:** Intermediate

The local average treatment effect (LATE) is the causal effect of treatment for compliers — units whose treatment status is changed by the instrument — and is the estimand identified by instrumental variables methods. It is local because it does not represent the effect for all units, only for compliers. Businesses must recognize that LATE may not generalize to the full population, particularly when compliers are a non-representative subgroup. Understanding who compliers are is essential for determining whether IV estimates are policy-relevant.

**Real-life applications:**
- IV estimates of the effect of a new software tool apply only to employees who would change adoption based on a random nudge
- LATE from a price experiment applies to price-sensitive customers who respond to random price variations
- Loan approval effects from credit score cutoffs apply only to marginal applicants near the cutoff
- Training program effects from lottery assignment apply to individuals who would train only if chosen

**Key concepts:** `LATE`, `compliers`, `instrumental variables`, `generalizability`, `policy relevance`

---

## Q87. How does two-stage least squares estimation work in practice?

**Level:** Intermediate

Two-stage least squares (2SLS) is the standard method for implementing instrumental variables estimation. In the first stage, the endogenous treatment variable is regressed on the instrument and any controls, generating predicted values that represent the exogenous variation. In the second stage, the outcome is regressed on these predicted treatment values, effectively purging the endogenous component. Standard errors must be adjusted to reflect the two-stage nature, and weak instruments (with low first-stage F-statistics) inflate standard errors and can lead to unreliable estimates.

**Real-life applications:**
- Estimating the causal effect of advertising spend on revenue using competitor advertising as an instrument
- Estimating price elasticity using cost-shifter instruments in two-stage regressions
- Studying the effect of political connections on firm outcomes using election results as instruments
- Measuring the impact of access to credit on firm growth using loan officer assignment as an instrument

**Key concepts:** `2SLS`, `first stage`, `second stage`, `instrument strength`, `F-statistic`

---

## Q88. What is the difference between internal validity and external validity in causal studies?

**Level:** Intermediate

Internal validity refers to whether the causal inference is correct for the study sample, meaning confounders are properly controlled and the treatment effect is unbiased. External validity refers to whether findings generalize beyond the study sample to other populations, settings, or time periods. Highly controlled experiments often have strong internal validity but limited external validity, while observational studies may have broader external validity but weaker internal validity. Businesses must balance both dimensions when applying research findings to new markets or contexts.

**Real-life applications:**
- A controlled lab experiment on ad effectiveness may not translate to real-world purchasing behavior
- An A/B test run on US users may not generalize to international markets
- Results from early adopters in a product launch may not predict mainstream adoption
- Findings from a pilot program in one city may not replicate when scaled nationally

**Key concepts:** `internal validity`, `external validity`, `generalizability`, `sample representativeness`, `transportability`

---

## Q89. How does fixed effects regression control for unobserved individual heterogeneity?

**Level:** Intermediate

Fixed effects regression absorbs all time-invariant unobserved differences between units by including unit-specific intercepts or equivalently by demeaning variables at the unit level. This removes any confounding due to stable individual characteristics, such as inherent ability or firm culture, that are correlated with both treatment and outcome. The trade-off is that fixed effects cannot identify the causal effect of time-invariant treatments and require sufficient within-unit variation. They are widely used in panel data settings.

**Real-life applications:**
- Controlling for unobserved firm quality when estimating the effect of a management intervention across firms
- Removing individual productivity differences when studying the effect of incentive pay
- Absorbing neighborhood-level differences when estimating the effect of local policy changes
- Controlling for store-specific factors when measuring the effect of promotional campaigns across locations

**Key concepts:** `fixed effects`, `panel data`, `within-unit variation`, `unit-specific intercepts`, `demeaning`

---

## Q90. What is a regression discontinuity design, and under what conditions is it valid?

**Level:** Intermediate

Regression discontinuity design (RDD) exploits a known threshold in an assignment variable to identify causal effects. Units just below and just above the cutoff are treated as locally comparable, so differences in outcomes at the threshold are attributed to treatment. Validity requires that units cannot precisely manipulate their assignment variable value to sort above or below the cutoff, which is tested using density tests such as the McCrary test. The identifying assumption is that all other determinants of the outcome vary smoothly through the cutoff.

**Real-life applications:**
- Estimating the effect of college attendance using GPA-based scholarship eligibility thresholds
- Studying the effect of tax bracket changes using income cutoffs as the running variable
- Measuring the impact of loan approval on business growth using credit score cutoffs
- Evaluating the effect of passing a professional licensing exam on earnings

**Key concepts:** `running variable`, `cutoff`, `continuity assumption`, `manipulation test`, `local randomization`

---

## Q91. How does the choice of bandwidth affect regression discontinuity estimates?

**Level:** Intermediate

The bandwidth in RDD determines the range of observations around the cutoff used in estimation. A narrower bandwidth makes the local comparison more credible because units closer to the cutoff are more similar, but reduces sample size and increases variance. A wider bandwidth increases precision but risks including units where the continuity assumption breaks down. Optimal bandwidth selection methods, such as those developed by Imbens and Kalyanaraman, balance bias and variance. Robustness checks across multiple bandwidths are standard practice.

**Real-life applications:**
- Selecting observation windows near credit score cutoffs for loan effect studies
- Choosing time windows around a policy change threshold for evaluating program impacts
- Narrowing the income range near a tax bracket boundary to study behavioral responses
- Restricting analysis to students just above and below a test score cutoff

**Key concepts:** `bandwidth`, `bias-variance tradeoff`, `local polynomial regression`, `optimal bandwidth`, `robustness`

---

## Q92. Why might a difference-in-differences estimate be biased, and how can the bias be addressed?

**Level:** Intermediate

DiD estimates are biased if the parallel trends assumption is violated, meaning treated and control groups were on diverging trajectories even before treatment. Bias also arises from anticipation effects, where treated units change behavior before the official treatment date, or from spillover effects that contaminate the control group. Researchers address these issues by carefully selecting control groups, using event study specifications to test pre-trends, excluding contaminated controls, and applying synthetic control methods when no suitable control group exists.

**Real-life applications:**
- Bias from firms preemptively adjusting wages before a minimum wage law takes effect
- Control stores being affected by a loyalty program rollout through shared supply chains
- Pre-existing divergence in sales trends between treated and untreated product categories
- Healthcare control regions affected by treated-region publicity about a new intervention

**Key concepts:** `parallel trends violation`, `anticipation effect`, `spillover`, `synthetic control`, `event study`

---

## Q93. What is the synthetic control method, and when is it preferred over standard DiD?

**Level:** Intermediate

The synthetic control method constructs a weighted combination of control units that best matches the pre-treatment trajectory of the treated unit. This "synthetic" control is then used as the counterfactual for what the treated unit would have experienced without treatment. It is preferred over DiD when there is only one treated unit, such as a country or region, and when no single control unit provides a good parallel trend match. The method offers a transparent, data-driven approach to counterfactual construction.

**Real-life applications:**
- Evaluating the economic impact of a major trade policy change on a single country using other countries as donors
- Measuring the effect of a firm's IPO on innovation output using pre-IPO matched firms
- Estimating the revenue impact of a natural disaster on a single city
- Assessing the effect of a state-level tax reform with no comparable comparison state

**Key concepts:** `synthetic control`, `donor pool`, `pre-treatment fit`, `counterfactual`, `single treated unit`

---

## Q94. How do event study designs help evaluate the dynamic effects of an intervention?

**Level:** Intermediate

Event study designs estimate treatment effects at multiple time points before and after an intervention, allowing researchers to test for pre-trends and observe how effects evolve over time. They are implemented by including leads and lags of the treatment indicator in a regression model. Coefficients on leads test for anticipation effects and pre-trend violations, while coefficients on lags reveal whether effects fade or strengthen over time. Dynamic effects are crucial for understanding the long-run implications of business decisions.

**Real-life applications:**
- Tracking how a new product launch affects weekly revenue over 12 weeks post-launch
- Measuring how a layoff announcement affects employee engagement in the months before and after
- Evaluating how a marketing campaign's effect on web traffic evolves across four quarters
- Studying how a merger's impact on prices unfolds over two years post-acquisition

**Key concepts:** `event study`, `leads and lags`, `pre-trend test`, `dynamic effects`, `anticipation`

---

## Q95. What is the role of balance tests in evaluating randomization quality in experiments?

**Level:** Intermediate

Balance tests check whether randomization successfully produced comparable treatment and control groups on observed covariates. They are typically implemented by regressing each baseline covariate on the treatment indicator and testing for statistically significant differences. A well-randomized experiment should show no systematic differences, though some imbalance by chance is expected. When imbalance is found, covariate adjustment or stratified randomization can restore balance and improve precision.

**Real-life applications:**
- Verifying that A/B test groups have similar baseline purchase rates before measuring a new feature's effect
- Checking that participants in a clinical trial have balanced age and health status
- Ensuring that treatment and control stores in a pricing experiment have similar historical sales
- Validating that randomized email recipients have comparable prior engagement rates

**Key concepts:** `balance test`, `covariate balance`, `randomization check`, `regression adjustment`, `stratification`

---

## Q96. How does cluster-robust standard error estimation affect inference in business experiments?

**Level:** Intermediate

When treatment is assigned at a higher level than the unit of observation, such as randomizing at the store level but measuring individual transactions, standard errors must be clustered at the assignment level to account for within-cluster correlation. Failing to cluster inflates false positive rates because standard errors are underestimated. Cluster-robust standard errors are typically larger, resulting in wider confidence intervals and more conservative inference. The number of clusters also matters — too few clusters (fewer than 30–50) reduces the reliability of cluster-robust estimates.

**Real-life applications:**
- Store-level randomized experiments analyzed at the transaction level
- A/B tests where users are assigned by geographic market but metrics are measured per user session
- Employer-level randomized studies measured at the employee level
- Class-level educational interventions analyzed using student-level test scores

**Key concepts:** `cluster-robust standard errors`, `assignment level`, `within-cluster correlation`, `false positive`, `inference`

---

## Q97. What is propensity score weighting, and how does it differ from propensity score matching?

**Level:** Intermediate

Propensity score weighting uses the inverse of the propensity score to re-weight observations so that the covariate distribution of treated and control units appears balanced. Unlike matching, which discards unmatched observations, weighting retains all units, which is more efficient. Inverse probability weighting (IPW) can estimate the average treatment effect (ATE) for the full population, while matching typically estimates the average treatment effect on the treated (ATT). Extreme propensity scores near 0 or 1 can cause instability in weighted estimates.

**Real-life applications:**
- Estimating the effect of a health program using survey data while controlling for demographic confounders
- Reweighting a biased product feedback sample to match the true customer population
- Estimating the ATE of a job training program by reweighting a non-randomized dataset
- Adjusting observational sales data for targeting bias in a promotion analysis

**Key concepts:** `inverse probability weighting`, `ATE`, `ATT`, `propensity score`, `weight trimming`

---

## Q98. How does the exclusion restriction in IV differ from the relevance condition, and why must both hold?

**Level:** Intermediate

The exclusion restriction requires that the instrument affects the outcome only through the treatment and not through any other channel. The relevance condition requires that the instrument has a sufficiently strong effect on the treatment. Both conditions are necessary for valid IV estimation: relevance ensures the instrument provides useful variation in treatment, while the exclusion restriction ensures this variation is exogenous with respect to the outcome. Violation of either condition leads to inconsistent IV estimates.

**Real-life applications:**
- Using rainfall as an instrument for agricultural output requires that rainfall affects income only through crops, not through other channels
- Using distance to a store as an instrument for purchases requires that distance only affects behavior through the shopping trip decision
- Using judge leniency as an instrument for incarceration requires that leniency does not affect recidivism through other judicial actions
- Using lottery winnings as an instrument for wealth requires that lottery participation does not directly affect health outcomes

**Key concepts:** `exclusion restriction`, `instrument relevance`, `exogeneity`, `validity`, `weak instrument`

---

## Q99. What is Rubin's potential outcomes framework and how does it formalize causal reasoning?

**Level:** Intermediate

Rubin's potential outcomes framework formalizes causation by defining for each unit two potential outcomes: the outcome if treated and the outcome if not treated. The causal effect is the difference between these two potential outcomes. The fundamental problem of causal inference is that only one potential outcome is ever observed for any unit, making individual-level causal effects unidentifiable without assumptions. Under randomization or conditional independence, average causal effects become identifiable from observed data.

**Real-life applications:**
- Defining the counterfactual revenue a customer would have generated without a discount
- Formalizing what employee productivity would have been without a new management program
- Reasoning about the sales a store would have achieved if it had not run a promotion
- Estimating what churn rate would have been for a cohort that did not receive a retention email

**Key concepts:** `potential outcomes`, `counterfactual`, `fundamental problem of causal inference`, `average treatment effect`, `SUTVA`

---

## Q100. How does the SUTVA assumption constrain the design of business experiments?

**Level:** Intermediate

The stable unit treatment value assumption (SUTVA) requires that the potential outcome of one unit is unaffected by the treatment of another unit and that there is a single version of treatment. Violations arise in business settings through network effects, marketplace competition, or shared infrastructure. When SUTVA is violated, standard A/B test estimates conflate the treatment effect with spillovers, leading to biased conclusions. Cluster-level randomization, holdout markets, or two-sided experiment designs can mitigate SUTVA violations.

**Real-life applications:**
- Marketplace experiments where pricing changes for some sellers affect demand for untreated sellers
- Social network experiments where treated users influence the behavior of control users
- Supply chain experiments where treated warehouses draw resources from control warehouses
- Ad auction experiments where bids for treated advertisers affect prices for untreated advertisers

**Key concepts:** `SUTVA`, `spillover`, `network effects`, `interference`, `cluster randomization`

---

## Q101. What are the main threats to internal validity in observational causal studies?

**Level:** Intermediate

The main threats to internal validity in observational studies include confounding (omitted variable bias), selection bias (non-random treatment assignment), simultaneity bias (reverse causality), measurement error, and attrition. Each threat can cause the estimated treatment effect to deviate from the true causal effect. Researchers address these threats through careful study design, instrumental variables, difference-in-differences, regression discontinuity, or matching methods. Sensitivity analyses assess how robust findings are to unmeasured confounders.

**Real-life applications:**
- Selection bias when evaluating job training programs because motivated individuals self-select into training
- Reverse causality when profitable firms invest more in marketing, making it hard to isolate marketing's effect
- Attrition bias when churn makes it impossible to observe long-run outcomes for all users
- Measurement error in self-reported survey data used to proxy treatment status

**Key concepts:** `confounding`, `selection bias`, `reverse causality`, `attrition`, `measurement error`

---

## Q102. How does regression adjustment improve precision in randomized experiments?

**Level:** Intermediate

Even in randomized experiments, outcome variance can be high, reducing statistical power. Regression adjustment — including pre-treatment covariates that predict the outcome in the analysis model — absorbs residual variance and shrinks standard errors without introducing bias under randomization. This approach, known as ANCOVA, typically yields more precise estimates than a simple difference-in-means and is particularly valuable when the experiment has limited sample size. Covariates should be pre-specified to prevent fishing.

**Real-life applications:**
- Including baseline sales when analyzing the effect of a promotional campaign
- Controlling for prior engagement metrics in an A/B test of a new product feature
- Adding demographic variables to a clinical trial analysis to reduce outcome variance
- Using prior customer lifetime value as a covariate when testing a new retention offer

**Key concepts:** `ANCOVA`, `covariate adjustment`, `precision`, `pre-specification`, `residual variance`

---

## Q103. What is the complier average causal effect (CACE), and how is it estimated?

**Level:** Intermediate

The complier average causal effect (CACE), also known as the local average treatment effect (LATE), is the causal effect of treatment for the subpopulation of compliers — those who take up treatment when assigned to it and do not when not assigned. It is estimated using instrumental variables, where the instrument is the random assignment indicator and the treatment is actual uptake. CACE is useful when non-compliance is present in randomized experiments and represents the effect for the relevant population that responds to the encouragement.

**Real-life applications:**
- Estimating the effect of completing an online course for those who would only complete it if randomly enrolled
- Measuring the effect of attending a workplace training for employees who comply with random scheduling
- Estimating the revenue effect of a promotional email for customers who open emails only when randomly incentivized
- Evaluating the health impact of a medical treatment for patients who take it only when assigned by lottery

**Key concepts:** `CACE`, `compliers`, `non-compliance`, `encouragement design`, `LATE`

---

## Q104. How do DiD and RDD compare in terms of their identifying assumptions and typical use cases?

**Level:** Intermediate

DiD relies on the parallel trends assumption and uses variation over time across treated and untreated groups, making it well-suited for policy rollouts or phased interventions. RDD relies on the continuity assumption and uses variation around a threshold in an assignment variable, making it well-suited for eligibility cutoffs. DiD requires data before and after the intervention; RDD requires data on units around the cutoff. Both are weaker than randomized experiments but stronger than naive regression when their assumptions hold.

**Real-life applications:**
- DiD for evaluating a staggered regional rollout of a new pricing policy
- RDD for evaluating the effect of a customer loyalty tier upgrade at a spending threshold
- DiD for studying employment effects of minimum wage increases across states
- RDD for studying the effect of passing a standardized licensing exam on career outcomes

**Key concepts:** `DiD`, `RDD`, `parallel trends`, `continuity assumption`, `quasi-experiment`

---

## Q105. How is sensitivity analysis used to assess the robustness of causal findings to unmeasured confounding?

**Level:** Intermediate

Sensitivity analysis quantifies how strong unmeasured confounding would need to be to overturn a causal conclusion. Methods include Rosenbaum bounds (for matched observational studies), Oster's method (for regression studies), and the E-value (for any causal estimate). A high E-value or Rosenbaum bound indicates that confounding would need to be implausibly strong to explain away the result, increasing confidence in the finding. Conversely, low bounds suggest the finding is fragile and should be interpreted cautiously.

**Real-life applications:**
- Assessing whether a causal finding about customer churn survives sensitivity to unmeasured engagement factors
- Evaluating robustness of an employee training effect to unobserved motivation differences
- Testing how robust a health intervention estimate is to unmeasured lifestyle confounders
- Determining how sensitive a pricing effect estimate is to omitted competitive information

**Key concepts:** `sensitivity analysis`, `E-value`, `Rosenbaum bounds`, `unmeasured confounding`, `robustness`

---

## Q106. What is the average treatment effect (ATE) versus the average treatment effect on the treated (ATT), and when does the distinction matter?

**Level:** Intermediate

The ATE is the average causal effect across all units in the population, while the ATT is the average causal effect among only those units that actually received the treatment. The distinction matters when the treated group differs from the overall population, as treatment effects may be heterogeneous. For policy evaluation, the ATT is often more relevant — it tells us the effect among those who received or are likely to receive the program. For policies targeting the full population, the ATE is more relevant.

**Real-life applications:**
- ATT for evaluating a job training program among those who enrolled versus ATE for scaling it to all eligible workers
- ATT for assessing a loyalty program's effect on those who joined versus ATE for all customers
- ATT for measuring a health intervention's effect on participants versus ATE for considering universal rollout
- ATE for estimating the effect of a product feature on all future users versus ATT for early adopters

**Key concepts:** `ATE`, `ATT`, `treatment effect heterogeneity`, `policy relevance`, `population of interest`

---

## Q107. How does the regression kink design extend the regression discontinuity approach?

**Level:** Intermediate

The regression kink design (RKD) exploits a known kink — a change in the slope — in the relationship between an assignment variable and the treatment intensity, rather than a discrete jump in treatment probability. It identifies the causal effect of continuous variation in treatment intensity by comparing the slope of the outcome function just above and below the kink point. RKD is applicable when a policy determines treatment intensity (such as benefit levels) as a function of a running variable.

**Real-life applications:**
- Estimating the effect of unemployment benefit generosity on job search duration using benefit formula kinks
- Studying how tax marginal rates affect reported income using tax schedule kink points
- Evaluating how subsidy amount affects firm investment using funding formula kink points
- Measuring the effect of pension benefit levels on retirement timing using earnings formula kinks

**Key concepts:** `regression kink design`, `kink point`, `treatment intensity`, `slope discontinuity`, `running variable`

---

## Q108. What are the assumptions underlying propensity score matching, and what happens when they are violated?

**Level:** Intermediate

Propensity score matching relies on the conditional independence assumption (CIA), which states that conditional on observed covariates, treatment assignment is independent of potential outcomes. It also requires overlap — every unit must have a positive probability of receiving either treatment. When CIA is violated due to unmeasured confounders, matching estimates are biased. When overlap fails, matched estimates extrapolate beyond the support of the data. Sensitivity analyses and overlap checks are essential validations.

**Real-life applications:**
- CIA violation when unobserved motivation drives both self-selection into job training and labor market outcomes
- Overlap failure when comparing very different customer segments in a loyalty program evaluation
- CIA violation when omitted health behaviors confound the estimated effect of a wellness benefit
- Overlap failure when treated and control firms operate in entirely different markets

**Key concepts:** `conditional independence assumption`, `overlap`, `common support`, `selection on observables`, `bias`

---

## Q109. How does covariate selection affect the validity of propensity score methods?

**Level:** Intermediate

In propensity score methods, covariates should be selected based on their role in the data generating process. Variables that are causally prior to treatment and predict the outcome should be included, while variables that are affected by treatment (post-treatment variables) should be excluded, as including them introduces collider bias. Variables that predict treatment but not the outcome are unnecessary and can hurt overlap. A domain-knowledge-driven, pre-specified covariate selection strategy produces the most defensible propensity score estimates.

**Real-life applications:**
- Including pre-treatment customer demographics but excluding post-treatment satisfaction scores in a retention analysis
- Avoiding the inclusion of intermediate variables when evaluating the effect of a sales training program
- Selecting relevant baseline health indicators while excluding post-enrollment medical events in a health study
- Including industry and size but not post-investment revenue in a loan approval effect study

**Key concepts:** `covariate selection`, `collider bias`, `post-treatment variable`, `pre-treatment covariate`, `propensity score estimation`

---

## Q110. What is the Wald estimator in the context of instrumental variables?

**Level:** Intermediate

The Wald estimator is the simplest form of instrumental variables estimation, applicable when both the instrument and the treatment are binary. It equals the ratio of the reduced form effect (the effect of the instrument on the outcome) to the first stage effect (the effect of the instrument on the treatment). It identifies the LATE for compliers under the relevance and exclusion restriction conditions. In practice, 2SLS generalizes the Wald estimator to settings with continuous instruments or multiple instruments.

**Real-life applications:**
- Using a lottery win as an instrument, the Wald estimator divides the income effect of winning by the employment effect of winning
- Estimating the effect of a mobile app feature by dividing the outcome response to random app assignment by the take-up rate
- Measuring the health effect of a nudge by dividing the health change by the behavioral compliance rate
- Estimating training effects by dividing outcome changes in the lottery-invited group by training completion rates

**Key concepts:** `Wald estimator`, `reduced form`, `first stage`, `LATE`, `binary instrument`

---

## Q111. How does the "first stage" F-statistic inform the quality of an instrumental variable?

**Level:** Intermediate

The first stage F-statistic tests whether the instrument has a sufficiently strong relationship with the treatment variable. A rule-of-thumb threshold of F > 10 (or more conservatively F > 16 per recent recommendations) indicates a strong instrument. Weak instruments with low F-statistics lead to IV estimates that are biased toward OLS, have inflated size (false positive rates), and wide confidence intervals. Weak instrument diagnostics should always be reported alongside IV estimates.

**Real-life applications:**
- Testing whether lottery assignment strongly predicts program enrollment before using it as an IV
- Checking whether weather shocks have a strong first-stage effect on agricultural supply
- Validating that distance to the nearest store is a strong predictor of store visits
- Confirming that judge leniency strongly predicts incarceration before using it as an IV for recidivism

**Key concepts:** `first stage F-statistic`, `weak instrument`, `instrument strength`, `bias`, `relevance condition`

---

## Q112. What is the role of placebo tests in validating causal identification strategies?

**Level:** Intermediate

Placebo tests check whether a causal identification strategy produces spurious results in settings where no effect should exist. For example, testing whether a treatment affects pre-treatment outcomes (which it cannot causally affect) checks for pre-trends. Similarly, applying the same method to an outcome unrelated to the treatment should yield a null result. Placebo tests provide indirect evidence for the validity of identifying assumptions, and significant placebo effects raise concerns about the research design.

**Real-life applications:**
- Testing whether a minimum wage increase affects pre-period employment in a DiD design
- Checking whether an RDD estimate exists for an unaffected outcome variable at the same cutoff
- Testing whether an IV affects outcomes for a placebo sample that did not experience the treatment
- Verifying that a synthetic control matches pre-treatment trends and yields no post-treatment effect for a placebo unit

**Key concepts:** `placebo test`, `pre-treatment outcome`, `falsification`, `identifying assumption`, `null effect`

---

## Q113. How does observational data complicate causal inference compared to experimental data?

**Level:** Intermediate

Observational data are generated by real-world processes where treatment assignment is not random, making treated and control groups systematically different. This non-random assignment creates confounding that biases naive comparisons. Researchers must identify sources of exogenous variation, use quasi-experimental methods, or rely on strong assumptions to make causal claims. Even with careful design, causal conclusions from observational data are generally less credible than those from randomized experiments and require more extensive robustness checks.

**Real-life applications:**
- Confounding when comparing the sales performance of mentored versus unmentored salespeople who self-selected into mentorship
- Selection bias when studying the effect of a premium product tier on retention when high-value customers self-upgrade
- Reverse causality when profitable firms spend more on R&D, making it hard to isolate R&D's effect on profits
- Endogeneity when studying hiring practices using firm-level data where unobservable firm quality drives both hiring and outcomes

**Key concepts:** `selection bias`, `endogeneity`, `confounding`, `quasi-experiment`, `observational study`

---

## Q114. What is a dose-response relationship, and how is it estimated in causal analysis?

**Level:** Intermediate

A dose-response relationship describes how the magnitude of a treatment effect varies with the intensity or dose of the treatment. It is estimated using parametric models that include treatment intensity as a continuous predictor, nonparametric methods, or instrumental variables for continuous treatment. Identifying a dose-response relationship requires careful handling of endogeneity in treatment intensity assignment. Generalizations of propensity score methods to continuous treatments (generalized propensity scores) can also be used.

**Real-life applications:**
- Estimating how email frequency affects unsubscribe rates across a range of sending frequencies
- Measuring how discount depth affects purchase probability across different discount levels
- Studying how training hours affect skill acquisition in corporate learning programs
- Estimating how advertising exposure frequency affects brand recall

**Key concepts:** `dose-response`, `continuous treatment`, `generalized propensity score`, `treatment intensity`, `nonparametric estimation`

---

## Q115. How does the choice of outcome variable affect causal conclusions in business studies?

**Level:** Intermediate

The choice of outcome variable determines what causal question is being answered and whether the answer is practically meaningful. Proximate outcomes (such as clicks) may be easier to measure and more statistically powered but may not translate to the ultimate business objective (such as revenue or customer lifetime value). Measuring multiple outcomes — including those in the causal chain — helps validate mechanisms. Choosing outcomes post-hoc inflates false positive rates and should be avoided through pre-registration.

**Real-life applications:**
- Measuring click-through rates when the true business outcome is revenue in an A/B test
- Choosing customer satisfaction scores as an outcome proxy when retention is the actual business goal
- Pre-specifying revenue per user as the primary outcome before launching a pricing experiment
- Evaluating both short-term conversion and long-term engagement to understand trade-offs

**Key concepts:** `outcome selection`, `surrogate outcome`, `pre-registration`, `multiple testing`, `causal chain`

---

## Q116. What is the purpose of a power calculation in designing business experiments?

**Level:** Intermediate

A power calculation determines the minimum sample size required to detect a meaningful treatment effect with a specified probability (power, typically 80–90%) at a given significance level. Underpowered experiments fail to detect true effects (false negatives), while overpowered experiments waste resources. Key inputs include the expected effect size, baseline outcome variance, significance level, and the number of treatment arms. Power calculations should be conducted before the experiment begins to commit to a sample size and prevent post-hoc adjustments.

**Real-life applications:**
- Determining how many users are needed to detect a 2% conversion rate improvement in an A/B test
- Calculating the number of stores required to detect a 5% sales lift from a promotional campaign
- Sizing a clinical trial to detect a clinically meaningful reduction in a health outcome
- Determining the duration of a pricing experiment needed to achieve statistical power for a small elasticity effect

**Key concepts:** `statistical power`, `minimum detectable effect`, `sample size`, `false negative`, `significance level`

---

## Q117. How does staggered treatment adoption complicate difference-in-differences estimation?

**Level:** Intermediate

In staggered DiD designs, different units receive treatment at different time points, creating variation in treatment timing. Recent econometric research has shown that standard two-way fixed effects DiD estimators use late adopters as implicit controls for early adopters, which is problematic when treatment effects evolve over time. Heterogeneous treatment effects across cohorts and periods can cause the standard estimator to produce negative-weighted averages, leading to biased or even sign-flipped estimates. New estimators by Callaway-Sant'Anna, Sun-Abraham, and de Chaisemartin-D'Haultfoeuille address these issues.

**Real-life applications:**
- Evaluating a phased product feature rollout across markets entering at different times
- Studying the effect of management changes in firms that adopted a new structure at different years
- Measuring the impact of a health program adopted by hospitals in different quarters
- Assessing a policy reform across jurisdictions that enacted it in different legislative sessions

**Key concepts:** `staggered adoption`, `two-way fixed effects`, `heterogeneous treatment effects`, `negative weights`, `Callaway-Sant'Anna`

---

## Q118. What is the role of theory in guiding causal inference in business research?

**Level:** Intermediate

Causal inference requires more than statistical tools — it requires a theoretical model that specifies the data generating process, identifies potential confounders, and justifies the choice of method. A directed acyclic graph (DAG) encodes the researcher's causal assumptions and reveals which variables should be controlled and which should not. Without theory, even sophisticated methods may be applied to the wrong estimand or in the wrong context. Theory and empirics should be co-developed, with statistical results used to test and refine theoretical predictions.

**Real-life applications:**
- Using a DAG to determine whether controlling for customer satisfaction is appropriate when estimating the effect of a pricing change on churn
- Building a theoretical model of advertising response before designing an experiment to test it
- Using economic theory to identify valid instruments for endogenous pricing decisions
- Applying a conceptual model of firm growth to structure SEM relationships

**Key concepts:** `directed acyclic graph`, `causal diagram`, `identifying assumptions`, `theoretical model`, `DAG`

---

## Q119. How does multiple hypothesis testing affect the reliability of causal findings in business experiments?

**Level:** Intermediate

Testing multiple hypotheses simultaneously increases the probability of finding at least one statistically significant result by chance (familywise error rate inflation). For example, testing 20 outcomes at the 5% significance level yields on average one false positive even if no true effects exist. Corrections such as the Bonferroni method, Benjamini-Hochberg procedure, or pre-registration of primary outcomes control false discovery rates. Businesses should pre-specify a primary metric and treat secondary metrics as exploratory.

**Real-life applications:**
- An A/B test with 20 secondary metrics where at least one appears significant by chance
- Testing a new product across five customer segments and reporting only the segment with the largest effect
- Reporting only the favorable subgroup analysis of a randomized policy trial
- Adjusting p-values when evaluating a marketing campaign's effect on multiple brand health metrics

**Key concepts:** `multiple testing`, `familywise error rate`, `Bonferroni correction`, `false discovery rate`, `pre-specification`

---

## Q120. What is the Angrist-Pischke (AP) test for weak instruments, and why does it matter?

**Level:** Intermediate

The Angrist-Pischke F-statistic is a test for the strength of individual instruments in just-identified or over-identified IV models. It measures the contribution of each instrument to the first-stage F-statistic after partialling out the other instruments. When the AP F-statistic is below standard thresholds (e.g., 10–16), the instrument is weak and IV estimates are unreliable. It matters because weak instruments can produce estimates that are more biased than OLS and have severely distorted confidence intervals.

**Real-life applications:**
- Testing whether two instruments for price endogeneity are individually strong before using both in demand estimation
- Validating that multiple geographic instruments for advertising reach each have strong individual first-stage effects
- Checking instrument strength in a supply-demand system estimated with cost and productivity instruments
- Confirming that two weather-based instruments for agricultural output are each sufficiently strong

**Key concepts:** `AP F-statistic`, `instrument strength`, `weak instrument`, `over-identification`, `first stage`

---

## Q121. How can machine learning methods be combined with causal inference to improve business decisions?

**Level:** Intermediate

Machine learning methods improve causal inference by automating high-dimensional covariate selection, constructing flexible nuisance function estimates, and estimating heterogeneous treatment effects. Double machine learning (DML) uses cross-fitting and ML models to estimate treatment effects while controlling for many covariates without overfitting. Causal forests estimate conditional average treatment effects (CATE) across subgroups without specifying the functional form. These methods enable businesses to target interventions to subgroups with the highest expected returns.

**Real-life applications:**
- Using causal forests to identify customer segments where a discount has the largest uplift
- Applying double machine learning to estimate the causal effect of website features while controlling for thousands of user attributes
- Using LASSO to select relevant controls before estimating a causal pricing effect
- Combining gradient boosting with causal inference to personalize pricing interventions

**Key concepts:** `double machine learning`, `causal forest`, `CATE`, `cross-fitting`, `heterogeneous treatment effects`

---

## Q122. What is a directed acyclic graph (DAG) and how is it used to identify confounders in causal analysis?

**Level:** Intermediate

A directed acyclic graph is a graphical representation of causal relationships between variables, with nodes representing variables and directed edges representing direct causal effects. DAGs make causal assumptions explicit and allow researchers to apply graphical rules (such as the backdoor criterion) to identify the minimal set of variables that must be controlled to estimate the effect of one variable on another. Variables not on a backdoor path should not be controlled, and controlling for colliders (common effects) introduces bias.

**Real-life applications:**
- Using a DAG to determine whether store size should be controlled when estimating the effect of staff training on sales
- Applying the backdoor criterion to identify which demographic variables must be adjusted for in a customer lifetime value study
- Using DAGs to avoid controlling for post-treatment variables that are mediators
- Identifying colliders in a study of advertising effects that would induce bias if included in the model

**Key concepts:** `DAG`, `backdoor criterion`, `collider`, `confounder`, `d-separation`

---

## Q123. How does a two-sided market create unique challenges for causal inference in platform businesses?

**Level:** Intermediate

Two-sided platforms connect distinct groups of users whose utilities are interdependent, creating interference where changes for one side of the market affect the other side. An experiment that increases supply on a ride-sharing platform may reduce prices and increase rides for all passengers, contaminating the control group. Standard A/B tests are invalid under this interference. Solutions include switchback experiments (alternating treatment over time), holdout markets, or interleaving designs that estimate platform-level effects.

**Real-life applications:**
- Ride-sharing platforms testing surge pricing algorithms where driver supply changes affect all riders
- Online marketplaces testing seller fee structures where changes affect buyer prices
- Food delivery platforms testing delivery fee changes where driver availability affects all orders
- Job platforms testing employer-facing features where matches affect all job seekers

**Key concepts:** `two-sided market`, `interference`, `switchback experiment`, `marketplace experiment`, `spillover`

---

## Q124. What is the difference between prediction and causal inference, and why does it matter for business decisions?

**Level:** Intermediate

Prediction models estimate the expected value of an outcome given observed features, without requiring any assumptions about causal structure. Causal inference estimates the effect of an intervention on an outcome, requiring assumptions about the data generating process and counterfactuals. Using predictive models to make causal decisions (e.g., targeting customers who are predicted to churn) can lead to poor outcomes if prediction is driven by non-causal correlations. Uplift modeling, which estimates the causal effect of an intervention on a target, is the appropriate tool for intervention decisions.

**Real-life applications:**
- A churn prediction model may score already-churning customers highly, making retention offers wasteful
- A credit default prediction model should not be misused as a causal model for the effect of loan terms
- Targeting high-scoring customers in a direct marketing campaign based on a predictive model that reflects selection
- Using an uplift model instead of a propensity model to target customers with the highest treatment response

**Key concepts:** `prediction`, `causal inference`, `uplift modeling`, `selection bias`, `intervention`

---

## Q125. How is the regression discontinuity design validated through density tests?

**Level:** Intermediate

The McCrary density test checks whether there is a discontinuous jump in the density of the running variable at the cutoff, which would suggest that units are manipulating their assignment variable to fall just above or below the threshold. Bunching just above a tax threshold, for example, indicates strategic behavior that violates the local randomization assumption of RDD. A smooth density through the cutoff supports the assumption that assignment near the threshold is as-good-as-random. Researchers also visually inspect density plots alongside formal tests.

**Real-life applications:**
- Testing for bunching just above a credit score threshold to validate an RDD of loan approval effects
- Checking for manipulation of test scores just above a scholarship eligibility threshold
- Examining whether firms strategically underreport revenues to stay below a regulatory size threshold
- Validating RDD assumptions in a study of GPA-based honor society eligibility

**Key concepts:** `McCrary test`, `density test`, `running variable manipulation`, `bunching`, `local randomization`

---

## Q126. What is the role of pre-analysis plans in improving the credibility of causal research?

**Level:** Intermediate

A pre-analysis plan (PAP) is a document registered before data collection or analysis that specifies the primary outcomes, identification strategy, sample restrictions, and statistical methods. By committing to these choices in advance, researchers prevent data-driven specification searches that inflate false positive rates. PAPs are standard in randomized trials and increasingly used in quasi-experimental research. They enhance credibility by making it transparent what was hypothesized before observing the data versus what was discovered post-hoc.

**Real-life applications:**
- Pre-registering the primary metric and analysis method of an A/B test before launch
- Filing a PAP for a policy evaluation before a minimum wage law takes effect
- Committing to a specific DiD specification before receiving data from a natural experiment
- Registering subgroup analyses before analyzing heterogeneous treatment effects in a clinical trial

**Key concepts:** `pre-analysis plan`, `pre-registration`, `specification search`, `false positive`, `credibility`

---

## Q127. How does endogenous treatment timing complicate difference-in-differences estimation?

**Level:** Intermediate

When units choose when to adopt treatment based on anticipated benefits or outcomes, treatment timing is endogenous, meaning early and late adopters differ in unobservable ways. This violates the parallel trends assumption because treated and control groups are selected on characteristics related to the outcome. Endogenous timing bias can cause DiD to overstate or understate the treatment effect. Researchers address this by identifying exogenous variation in timing, using instrumental variables for timing, or carefully selecting control groups with similar pre-treatment trends.

**Real-life applications:**
- Firms choosing to adopt a new technology earlier because they anticipate it will boost their already-growing revenue
- Healthcare providers that pre-emptively implement a new protocol before a policy deadline based on patient severity
- Retailers opening new stores in markets where demand is already growing, confounding the store opening effect
- Employees who request training when they are already performing poorly, biasing the estimated training effect

**Key concepts:** `endogenous timing`, `parallel trends`, `selection into timing`, `treatment endogeneity`, `DiD bias`

---

## Q128. What is a synthetic difference-in-differences approach, and how does it improve on standard DiD?

**Level:** Intermediate

Synthetic DiD combines elements of difference-in-differences and synthetic control methods. It reweights control units to match the pre-treatment trend of the treated unit (as in synthetic control) and then applies a DiD-style comparison across pre- and post-treatment periods. This approach is robust to violations of exact parallel trends because it adjusts for pre-existing level differences and trend differences. It also provides valid inference with few treated units, overcoming a limitation of standard DiD.

**Real-life applications:**
- Evaluating a regional policy with one treated region and multiple control regions with different pre-treatment trends
- Measuring the effect of a sudden market entry by a large competitor on incumbent firm revenues
- Studying the impact of a corporate scandal on a single firm's stock price using matched competitor firms
- Estimating the effect of a large-scale public infrastructure investment using reweighted comparison cities

**Key concepts:** `synthetic DiD`, `reweighting`, `pre-treatment trend matching`, `synthetic control`, `few treated units`

---

## Q129. How does the concept of external validity apply to A/B tests conducted in digital businesses?

**Level:** Intermediate

External validity in digital A/B tests concerns whether results from the experiment generalize to broader user populations, different time periods, and different product versions. Results from a test on a small percentage of active users may not generalize to all users, especially new users or churned users. Seasonality effects, novelty effects among existing users, and platform-specific behaviors further limit external validity. Replication across multiple time windows, user segments, and markets improves confidence in the generalizability of findings.

**Real-life applications:**
- An A/B test run during the holiday season may not generalize to steady-state behavior
- A feature test on power users may not predict how casual users will respond
- Results from desktop users may not translate to mobile users with different behavior patterns
- A pricing test on the US market may not generalize to price-sensitive international markets

**Key concepts:** `external validity`, `novelty effect`, `seasonality`, `user heterogeneity`, `replication`

---

## Q130. What is regression to the mean, and how does it confound causal evaluation of business interventions?

**Level:** Intermediate

Regression to the mean is the statistical phenomenon where extreme observations on an initial measurement tend to be closer to the population mean on subsequent measurements, regardless of any intervention. If a business targets its worst-performing stores for an intervention, subsequent improvement may partly reflect regression to the mean rather than the causal effect of the treatment. Without a control group, regression to the mean is indistinguishable from a genuine treatment effect. Proper control groups eliminate this confound.

**Real-life applications:**
- Targeted coaching for the lowest-performing sales representatives showing improvement that is partly regression to the mean
- Selecting the worst-performing customer cohorts for a retention intervention and observing improvement
- Evaluating a remedial program for students with the lowest initial test scores
- Assessing a process improvement initiative triggered by unusually high defect rates

**Key concepts:** `regression to the mean`, `selection on extremes`, `control group`, `spurious improvement`, `baseline`

---

## Q131. How does the concept of common support affect the validity of causal estimates from matching methods?

**Level:** Intermediate

Common support (or overlap) requires that for every combination of covariate values, there is a positive probability of being in both the treated and control groups. When treated units have covariate values not represented in the control group, extrapolation is required, making estimates model-dependent and unreliable. Overlap violations are detected by comparing propensity score distributions of treated and control units. Units outside the common support region should be trimmed, and findings should be explicitly qualified as applying to the matched subpopulation.

**Real-life applications:**
- Comparing enterprise customers to SMB customers when the two groups have non-overlapping revenue ranges
- Matching on demographics when treated customers are predominantly young and controls are predominantly old
- Evaluating a training program when trained employees are exclusively from high-education backgrounds with no control counterparts
- Estimating loan approval effects when approved and denied applicants have very different credit score distributions

**Key concepts:** `common support`, `overlap`, `trimming`, `extrapolation`, `propensity score distribution`

---

## Q132. What is the difference between intent-to-treat and per-protocol analysis in business experiments?

**Level:** Intermediate

Intent-to-treat (ITT) analysis includes all participants in their originally assigned groups, regardless of whether they complied with treatment. Per-protocol analysis restricts the sample to participants who fully complied with the assigned treatment. ITT provides a conservative, policy-relevant estimate of the effect of offering a treatment. Per-protocol analysis can be biased if compliance is endogenous (e.g., compliers are different from non-compliers). CACE estimation via instrumental variables provides a non-biased estimate of the effect among compliers.

**Real-life applications:**
- Measuring the ITT effect of offering a free trial versus the per-protocol effect among those who actually used the trial
- Comparing the ITT effect of a mandatory training program versus the effect among employees who completed it
- Estimating the policy-relevant effect of a subsidy offer versus the effect among subsidy recipients
- Evaluating a marketing email campaign on all recipients (ITT) versus those who opened the email (per-protocol)

**Key concepts:** `intent-to-treat`, `per-protocol`, `compliance`, `CACE`, `selection bias`

---

## Q133. How does the use of administrative data improve causal inference in business contexts?

**Level:** Intermediate

Administrative data — records generated as a byproduct of business or government operations — offer large sample sizes, accurate measurement, and long follow-up periods that are unavailable in surveys or experiments. These advantages improve statistical power, reduce measurement error, and allow detection of long-run effects. However, administrative data may not contain all relevant variables for causal identification, may be subject to reporting biases, and may lack external validity for non-administrative populations. Linking administrative data across sources can address some limitations.

**Real-life applications:**
- Using transaction records to estimate the causal effect of a loyalty program with high precision
- Linking employee HR records with payroll data to study the effect of training on compensation
- Using tax records to estimate the causal effect of firm subsidies on long-run employment
- Combining healthcare claims data with prescription records to study the causal effect of a drug on outcomes

**Key concepts:** `administrative data`, `sample size`, `measurement error`, `data linkage`, `long-run effects`

---

## Q134. What is the difference between marginal and average causal effects in policy evaluation?

**Level:** Intermediate

The average causal effect is the mean treatment effect across all treated units, while the marginal causal effect is the effect for the unit at the boundary of the treatment eligibility or decision. Marginal effects are particularly important for cost-benefit analysis of policy expansions, as they determine the effect of treating one more unit. Regression discontinuity designs and marginal treatment effect models estimate effects at the margin, which may differ substantially from the average effect across all treated units.

**Real-life applications:**
- The average effect of a loan on firm growth may be higher than the marginal effect for marginal applicants near the approval cutoff
- The average effect of a training program may exceed the marginal effect for the last worker induced into training
- Expanding a subsidy to less-eligible firms may yield smaller effects than the average effect on highly eligible firms
- Scaling a successful pilot to a larger population may reveal diminishing marginal effects

**Key concepts:** `marginal treatment effect`, `average treatment effect`, `policy expansion`, `regression discontinuity`, `cost-benefit analysis`

---

## Q135. How is covariate balance measured and reported in observational causal studies?

**Level:** Intermediate

Covariate balance is measured by comparing the distribution of observed covariates between treated and control groups before and after matching or weighting. Standardized mean differences (SMDs) are the preferred metric, with values below 0.1 (or sometimes 0.25) indicating adequate balance. Love plots visually display SMDs for all covariates before and after adjustment. Unlike hypothesis tests, SMDs do not depend on sample size, making them more appropriate for assessing practical balance. Both mean and distributional balance should be assessed.

**Real-life applications:**
- Reporting SMDs for customer demographics before and after propensity score matching in a retention study
- Creating Love plots to visualize balance improvements from inverse probability weighting in a health economics study
- Checking balance on both means and higher moments of the propensity score distribution
- Including balance tables in business analytics reports to document the quality of quasi-experimental comparisons

**Key concepts:** `standardized mean difference`, `Love plot`, `covariate balance`, `matching quality`, `balance assessment`

---

## Q136. How does the treatment effect on the compliers relate to the treatment effect on the full population?

**Level:** Intermediate

The LATE (treatment effect on compliers) may differ from the ATE (treatment effect on the full population) when treatment effects are heterogeneous across subgroups. Compliers — those whose treatment status is changed by the instrument — may be a selected subgroup with characteristics that make them more or less responsive to treatment. If compliers are systematically different from non-compliers (never-takers and always-takers), the LATE cannot be extrapolated to the full population without additional assumptions about effect heterogeneity. Understanding who compliers are is essential for policy extrapolation.

**Real-life applications:**
- LATE from a job training lottery applies to individuals who would train only if offered lottery-based enrollment, not self-motivated trainers
- LATE from a price sensitivity instrument applies to price-responsive customers, not brand-loyal ones
- LATE from an insurance mandate applies to individuals who enrolled only due to the mandate, not pre-existing enrollees
- LATE from a nudge applies to nudge-sensitive customers, not those who would have acted regardless

**Key concepts:** `LATE`, `ATE`, `compliers`, `always-takers`, `never-takers`

---

## Q137. What is the relationship between causal diagrams and the identification of estimands in causal inference?

**Level:** Intermediate

Causal diagrams (DAGs) formalize the researcher's assumptions about the causal structure of the data generating process and allow rigorous identification of what can and cannot be estimated from observed data. The backdoor and frontdoor criteria, derived from the DAG structure, determine whether and how the causal effect of interest is identifiable from observational data. By encoding assumptions graphically, DAGs make implicit beliefs explicit and allow critical evaluation of identification strategies. They also reveal when controlling for certain variables (colliders) would induce rather than remove bias.

**Real-life applications:**
- Using a DAG to confirm that controlling for customer segment and tenure is sufficient to identify the causal effect of a loyalty program
- Applying the frontdoor criterion when the direct effect is blocked but the indirect path is identifiable
- Using a DAG to show that controlling for customer satisfaction is inappropriate because it is a mediator
- Identifying a valid adjustment set for estimating the effect of advertising on revenue in a competitive market

**Key concepts:** `DAG`, `backdoor criterion`, `frontdoor criterion`, `identification`, `adjustment set`

---

## Q138. How does sample selection bias arise in business data, and how can it be addressed?

**Level:** Intermediate

Sample selection bias occurs when the observed data is a non-random subset of the population of interest, making results unrepresentative. In business contexts, it arises when analysis is restricted to active users, surviving firms, or completed transactions, excluding churned users, failed firms, or abandoned transactions. This is known as survivorship bias when only successful outcomes are observed. Remedies include Heckman selection correction models, sensitivity analyses that bound the effect under selection, and redesigning data collection to reduce attrition.

**Real-life applications:**
- Analyzing only active customers when estimating the effect of a product change, missing churned customers
- Studying only successful startups when evaluating the effect of VC investment, excluding failed ventures
- Analyzing completed purchases when estimating the effect of a checkout design, excluding cart abandoners
- Studying employees who stay with the firm when measuring the effect of a culture change, excluding those who leave

**Key concepts:** `sample selection bias`, `survivorship bias`, `Heckman correction`, `attrition`, `selection model`

---

## Q139. What are the advantages and limitations of natural experiments compared to randomized controlled trials?

**Level:** Intermediate

Natural experiments offer high external validity because they occur in real-world settings without researcher-induced artificial conditions, and they can study effects that would be unethical or impractical to randomize. However, they rely on finding exogenous variation that is genuinely as-good-as-random, which cannot always be guaranteed, and they may estimate LATE rather than ATE, limiting generalizability. RCTs provide stronger internal validity through guaranteed randomization but may suffer from compliance issues, Hawthorne effects, and limited external validity. Both approaches play complementary roles in causal inference.

**Real-life applications:**
- Natural experiments study the effect of compulsory schooling laws on earnings without ethical concerns about withholding education
- RCTs provide clean estimates of a drug's efficacy under controlled conditions that natural settings cannot replicate
- Natural experiments capture real-world firm responses to regulatory changes that lab experiments cannot mimic
- RCTs allow precise measurement of a new product feature's effect but may induce novelty effects not present at scale

**Key concepts:** `natural experiment`, `RCT`, `internal validity`, `external validity`, `ethical feasibility`

---

## Q140. How should businesses interpret statistically insignificant results from causal studies?

**Level:** Intermediate

A statistically insignificant result does not prove that no effect exists — it only indicates that the evidence is insufficient to reject the null hypothesis at the chosen significance level. The interpretation depends on the study's statistical power: an underpowered study may fail to detect a true effect, while a well-powered study's null result is more informative. Confidence intervals are more informative than p-values alone, as they reveal the range of plausible effect sizes. Businesses should consider whether the confidence interval excludes effects that would be economically meaningful.

**Real-life applications:**
- An underpowered A/B test showing no significant conversion rate difference may reflect inadequate sample size
- A well-powered experiment yielding a null result can confidently conclude that the feature has no meaningful effect
- Reporting confidence intervals to determine whether economically significant effects are ruled out
- Using equivalence testing to formally demonstrate that an effect is below a practical threshold

**Key concepts:** `statistical significance`, `null result`, `statistical power`, `confidence interval`, `equivalence testing`

---

---

## Audited Appendix

# Causal Analysis in Business — Intermediate Q&A Audit (Q71–Q140)
**Course:** Causal Analysis in Business | **Level:** Intermediate | **Worker:** A10
**Scope:** Questions 71–140 | 70 Intermediate Concepts | **Industry Lens:** IT / AI / Product / Consulting

---

## Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|---|---|---|
| **SUTVA** (Stable Unit Treatment Value Assumption) | Each unit's outcome depends only on its own treatment, not on other units' treatments; and treatment is well-defined and consistent. | Violated in two-sided marketplaces (Uber surge pricing affects both riders and drivers simultaneously). Without SUTVA, A/B test estimates are biased and may lead to wrong product decisions. |
| **LATE** (Local Average Treatment Effect) | The average treatment effect for the specific sub-population of compliers — units who take treatment if and only if the instrument assigns them to. | IV estimates LATE, not ATE. In a software feature rollout using a randomized invite as instrument, LATE measures the effect on users who actually adopt when nudged — not all users. Product decisions based on LATE may not generalize to the full user base. |
| **McCrary Density Test** | A statistical test that checks whether there is a discontinuity (jump) in the density of the running variable at the RDD cutoff. | Manipulation of the running variable (e.g., employees gaming a performance score just above a threshold) invalidates RDD. This test detects such gaming before you publish causal conclusions about promotion programs. |
| **Parallel Trends Assumption** | In Difference-in-Differences, the assumption that treatment and control groups would have followed the same outcome trajectory in the absence of treatment. | The most common point of failure for DiD in consulting. If treated firms were already on a steeper growth curve before the policy, DiD over-attributes gains to the treatment. Event study plots are the diagnostic. |
| **Propensity Score** | The probability that a unit receives treatment, conditional on observed covariates. | Used in matching and inverse probability weighting (IPW) to create a pseudo-randomized comparison. In AI model fairness audits, propensity scores help compare similarly-situated users across demographic groups who receive different algorithmic recommendations. |
| **Collider Bias** | Bias introduced when you condition on a variable that is a common effect (collider) of two variables in a DAG, which opens a spurious association between the causes. | Classic trap in product analytics: conditioning on "users who converted" (a collider of ad quality and landing page quality) creates a spurious negative correlation between ad quality and page quality. Leads to wrong optimization priorities. |
| **E-value** | The minimum strength of association (on the risk ratio scale) that an unmeasured confounder would need to have with both treatment and outcome to fully explain away an observed effect. | In consulting due diligence, an observed effect with E-value of 2.0 means an unmeasured confounder needs a 2× association with both variables to nullify the finding. Low E-values signal fragile causal claims. |
| **Synthetic Control** | A weighted combination of control units chosen to match the pre-treatment trajectory of a treated unit, used when there is only one or a few treated units. | Standard in policy evaluation (e.g., effect of GDPR on a single country's data economy). Product teams use it to evaluate the causal impact of a feature launch in a geography where randomization was infeasible. |
| **Callaway-Sant'Anna Estimator** | A heterogeneity-robust DiD estimator for staggered treatment adoption that computes group-time average treatment effects and avoids using already-treated units as controls. | Critical for SaaS product rollouts where features are released to different cohorts at different times. Classical TWFE DiD can produce sign-reversed estimates under effect heterogeneity; Callaway-Sant'Anna avoids this. |
| **Double Machine Learning (DML)** | A method that uses flexible ML models to partial out the effect of controls on both treatment and outcome, then estimates the causal effect in a residual-on-residual regression, with cross-fitting to avoid overfitting bias. | Enables causal estimation with high-dimensional feature sets (hundreds of user behavioral signals). Used by AI product teams when standard regression is underpowered or misspecified due to many potential confounders. |
| **Uplift Modeling** | A predictive modeling approach that directly estimates the individual-level treatment effect (CATE) — the incremental gain from treatment over control for each unit. | Contrasts with standard prediction, which just predicts outcome probability. In retention campaigns, uplift modeling identifies "persuadables" who would churn without intervention but stay with it — avoiding waste on "sure things" and "lost causes." |
| **Rosenbaum Bounds** | A sensitivity analysis in matched observational studies that determines how strong hidden bias (unmeasured confounding) would need to be to overturn a conclusion. | Expressed as gamma (Γ): if Γ = 2, an unmeasured confounder doubling the odds of treatment is needed to invalidate the finding. IT consulting projects must report Γ alongside matched analysis results to signal robustness. |

---

## Frameworks & Mental Models

### 1. IV Validity Checklist

```
┌─────────────────────────────────────────────────────────────────┐
│              INSTRUMENTAL VARIABLE VALIDITY CHECKLIST           │
├──────────────────────┬──────────────────────────────────────────┤
│ Condition            │ Diagnostic                               │
├──────────────────────┼──────────────────────────────────────────┤
│ RELEVANCE            │ First-stage F-stat ≥ 10 (Stock-Yogo)     │
│ (Z → D is strong)   │ Preferred: Effective F ≥ 16 (Lee et al.) │
│                      │ Partial R² of instrument in first stage  │
├──────────────────────┼──────────────────────────────────────────┤
│ EXOGENEITY           │ Not directly testable if exactly ID'd.   │
│ (Z ⊥ U, instrument  │ Use placebo tests: regress Z on pre-     │
│  independent of      │ treatment outcomes. Argue via design.    │
│  confounders)        │ Over-ID: Sargan-Hansen J-test            │
├──────────────────────┼──────────────────────────────────────────┤
│ EXCLUSION            │ Z affects Y ONLY through D.              │
│ (Z → Y only via D)  │ No direct path. Requires subject matter  │
│                      │ expertise. Cannot be tested statistically│
├──────────────────────┼──────────────────────────────────────────┤
│ MONOTONICITY         │ No "defiers" — if Z switches from 0→1,   │
│ (no defiers)         │ units either comply or don't; none do    │
│                      │ opposite. Required for LATE interpretation│
└──────────────────────┴──────────────────────────────────────────┘

          WALD ESTIMATOR (just-identified case):
          
          LATE = (E[Y|Z=1] - E[Y|Z=0]) / (E[D|Z=1] - E[D|Z=0])
               = Reduced Form Effect / First Stage Effect
```

### 2. Difference-in-Differences Assumptions Diagram

```
OUTCOME (Y)
│
│         Treatment Group (Counterfactual — never observed)
│         ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ *
│                                                     /
│                                                    /  ← DiD estimate
│         Treatment Group (Actual)                  /       (ATT)
│         ─────────────────────────────────────────*
│                                    ↑ Treatment
│                                    │
│         Control Group (Actual)     │
│         ─────────────────────────────────────────*
│
├─────────────────────────────────────────────────────→ TIME
         Pre-period                 Post-period

KEY ASSUMPTIONS:
  1. Parallel Trends: Treated and control would trend identically absent treatment
  2. No Anticipation: Treatment group does not adjust before official treatment date
  3. SUTVA: No spillovers between treatment and control groups
  4. Correct Functional Form: Additive (not multiplicative) parallel trends
  
DIAGNOSTICS:
  - Event study plot: test pre-treatment period coefficients ≈ 0
  - Placebo treatment: assign fake pre-treatment dates and verify null effect
  - Callaway-Sant'Anna for staggered adoption
```

### 3. DAG: Backdoor and Frontdoor Criterion

```
BACKDOOR CRITERION EXAMPLE:
(Confounded path must be blocked)

   U (Unobserved Confounder)
   ↙           ↘
  D (Treatment) → M (Mediator) → Y (Outcome)
   ↖                              ↗
    ────────── X (Observed) ──────
    
  Backdoor path: D ← U → Y  (must be blocked)
  Solution: Control for X if X blocks all backdoor paths


FRONTDOOR CRITERION EXAMPLE:
(When backdoor blocking is impossible)

   U (Unobserved)
   ↙            ↘
  D ──────→ M ──────→ Y
  
  D → M: no unmeasured confounders (can be estimated)
  M → Y: no unmeasured confounders (can be estimated)
  Frontdoor estimate = P(M|D) * P(Y|M, D) summed/integrated


COLLIDER BIAS:
  A → C ← B   (C is a collider)
  Conditioning on C opens spurious path A ↔ B
  
  Product Example: Ad Click → Conversion ← Landing Page Quality
  If you filter to "converters only," ad and page quality 
  appear negatively correlated (better ad = worse page, spuriously)
```

### 4. RDD Sharp vs Fuzzy

```
SHARP RDD:
  Treatment probability jumps from 0 to 1 exactly at cutoff c.
  
  P(D=1|X)
  1.0 ────────────────────────────────*──────────────────
                                      |
  0.0 ──────────────────────*─────────
                             c
  Effect = lim[x→c+] E[Y|X=x] - lim[x→c-] E[Y|X=x]
  Estimate: OLS on local bandwidth, polynomial in running variable


FUZZY RDD:
  Treatment probability jumps but not to 0/1. RDD as IV.
  
  P(D=1|X)
  0.8 ──────────────────────────────────────────────────*
                                       |
  0.3 ─────────────────────────────────
  0.0                                  c
  
  Effect = Jump in E[Y|X] at c / Jump in E[D|X] at c
  (Wald estimator; estimates LATE for compliers at cutoff)

BANDWIDTH SELECTION:
  - MSE-optimal (Imbens-Kalyanaraman / Calonico-Cattaneo-Titiunik)
  - Robustness: test with half and double bandwidth
  - McCrary test: verify no density manipulation at cutoff
```

### 5. Mediation vs Moderation Framework

```
MEDIATION (mechanism — HOW does X affect Y?):
  X ──────→ M ──────→ Y
  │                   ↑
  └──────────────────→┘ (direct effect)
  
  Total Effect = Direct Effect + Indirect Effect
  Indirect Effect = a-path * b-path
  Proportion Mediated = Indirect / Total
  Requires: Sequential ignorability assumption


MODERATION (for whom? — WHEN does X affect Y?):
  X ──────────────────→ Y
         ↑
         W (Moderator interacts with X)
  
  Model: Y = β0 + β1*X + β2*W + β3*(X*W) + ε
  Strategy effect: β1 + β3*W  (varies by moderator level)
  
  Product Application: 
  Feature X improves retention (Y) MORE for power users (W=1)
  than casual users (W=0) — moderator W = user engagement tier
```

---

## Formulas, Thresholds & Rules of Thumb

### Instrument Strength
- **F-statistic (first stage) ≥ 10**: Stock-Yogo (1994) conventional weak instrument threshold; below this, IV estimates may have severe bias toward OLS.
- **Effective F ≥ 16**: Lee et al. (2022) updated threshold for 5% size distortion in 2SLS; preferred in recent applied work.
- **Cragg-Donald Wald statistic**: Used for multiple instruments; compare to Stock-Yogo critical values table.
- **Kleibergen-Paap F-stat**: Heteroskedasticity-robust version; use with cluster-robust standard errors.

### Balance Diagnostics
- **Standardized Mean Difference (SMD) < 0.1**: Threshold for acceptable covariate balance after matching/weighting. SMD = (mean_treated - mean_control) / pooled SD.
- **Love Plot**: Visual display of SMD for all covariates before and after matching; must show all covariates crossing the < 0.1 line post-match.
- **Variance Ratio 0.5–2.0**: Supplementary balance check; treatment-to-control ratio of covariate variance within this range signals good balance.

### Regression and Multicollinearity
- **VIF > 10**: High multicollinearity warning; standard errors inflated, coefficients unstable.
- **VIF > 5**: Moderate concern; examine pairwise correlations and consider ridge regression.
- **Ridge regression**: Adds L2 penalty λ‖β‖² to OLS loss; biased but lower variance when multicollinearity is severe.

### Structural Equation Modeling Fit
- **RMSEA < 0.05**: Excellent model fit.
- **RMSEA < 0.08**: Acceptable model fit.
- **CFI > 0.95**: Good comparative fit index.
- **SRMR < 0.08**: Acceptable standardized root mean square residual.
- **Rule of thumb**: Use multiple fit indices; no single index is definitive.

### Sensitivity Analysis
- **E-value formula**: E = RR + √(RR × (RR − 1)), where RR is the observed risk ratio.
- **E-value interpretation**: Larger E-value = finding is more robust to unmeasured confounding.
- **Rosenbaum Bounds Γ > 1.5**: Suggests moderate robustness to hidden bias in matched observational studies.

### Multiple Hypothesis Testing
- **Bonferroni correction**: α_adjusted = α / k, where k = number of tests; conservative.
- **Benjamini-Hochberg FDR**: Controls expected proportion of false discoveries; less conservative than Bonferroni; preferred in exploratory subgroup analyses.
- **Pre-registration**: Specifying primary endpoints and analytical approach before data collection eliminates the need for post-hoc multiplicity corrections on primary outcomes.

### Power and Sample Size
- **Power ≥ 0.80 (80%)**: Conventional threshold; probability of detecting true effect.
- **MDE (Minimum Detectable Effect)**: Smallest effect that can be detected at given power and significance. MDE ∝ 1/√n.
- **Cohen's d = 0.2/0.5/0.8**: Small/medium/large effect size benchmarks.

### DiD and Event Study
- **Pre-treatment event study coefficients ≈ 0**: Necessary (not sufficient) evidence for parallel trends.
- **Staggered adoption**: Use Callaway-Sant'Anna or Sun-Abraham; avoid classical TWFE when treatment timing varies.
- **Placebo test p-value > 0.10**: Pre-period placebo should not reject null; failure suggests confounding.

---

## Do / Don't

### DO

1. **DO draw a DAG before choosing an estimator.** Explicit causal diagrams force you to articulate assumptions, identify backdoor paths, and select appropriate identification strategies rather than defaulting to regression.

2. **DO check instrument relevance with first-stage F-statistic before interpreting 2SLS results.** A weak instrument (F < 10) can make your IV estimate more biased than OLS, not less.

3. **DO run an event study plot before assuming parallel trends holds in DiD.** Pre-treatment period coefficients should be statistically indistinguishable from zero; a trend break pre-treatment invalidates the design.

4. **DO use the McCrary density test in any RDD analysis.** If units can manipulate the running variable to cross the cutoff (employees gaming performance reviews), your causal estimates are invalid.

5. **DO report the E-value for observational causal claims.** It quantifies how robust your finding is to unmeasured confounding and signals intellectual honesty to reviewers and executives.

6. **DO use cluster-robust standard errors when treatment is assigned at the group level.** In SaaS product experiments where randomization is at the company level but outcomes measured at user level, ignoring clustering severely underestimates standard errors.

7. **DO pre-specify your primary outcome, subgroup analyses, and statistical model before running an experiment.** Pre-analysis plans prevent HARKing (Hypothesizing After Results are Known) and protect Type I error rate.

8. **DO distinguish between ITT and ATT in your reporting.** ITT (intent-to-treat) is the conservative policy-relevant estimate; ATT adjusts for non-compliance and is relevant for understanding the treatment mechanism. Report both.

9. **DO use Callaway-Sant'Anna or Sun-Abraham estimators for staggered DiD.** Classical TWFE can have sign-reversed estimates when treatment effects are heterogeneous across cohorts — a catastrophic misdiagnosis in product rollout evaluation.

10. **DO apply the frontdoor criterion when backdoor blocking is impossible.** If the mediating mechanism is fully observed and unconfounded, you can estimate causal effects even with an unmeasured common cause.

### DON'T

1. **DON'T confuse correlation with causation in dashboards presented to leadership.** Controlled A/B tests or explicit identification strategies are required before claiming that Feature X caused the retention lift.

2. **DON'T ignore SUTVA violations in marketplace experiments.** In two-sided platforms (Airbnb, Uber), treating one side spills over to the other; use switchback experiments or market-level randomization, not user-level randomization.

3. **DON'T rely on VIF alone to diagnose harmful multicollinearity.** High VIF inflates standard errors but does not necessarily bias causal estimates if the collinear variable is not the treatment of interest. Diagnose whether the specific treatment coefficient is affected.

4. **DON'T interpret propensity score matching results without a Love Plot.** Presenting matched analysis without a covariate balance table (or Love plot) is analytically incomplete; reviewers cannot assess CIA plausibility.

5. **DON'T run subgroup analyses post-hoc without multiplicity correction.** Data-dredging across demographic cuts inflates Type I error. Pre-specify subgroups or apply Benjamini-Hochberg FDR correction.

6. **DON'T use classical TWFE DiD with staggered rollouts and heterogeneous effects.** Early adopters are used as "controls" for late adopters in TWFE, contaminating the estimate when treatment effects grow over time.

7. **DON'T extrapolate LATE to the full population.** IV estimates apply to compliers only — units who respond to the instrument. If compliers are unusual users (e.g., only those who open promotional emails), the LATE may have limited policy relevance.

8. **DON'T condition on post-treatment variables in a causal regression.** Controlling for a mediator between treatment and outcome blocks the causal channel and creates collider bias; omit all post-treatment variables unless conducting formal mediation analysis.

9. **DON'T use prediction model outputs to make causal inferences.** A high AUC churn prediction model tells you who will churn; it does not tell you what intervention will prevent churn. Use uplift modeling or CATE estimation for causal targeting.

10. **DON'T ignore regression to the mean in before/after analyses.** Units selected because they had extremely bad performance will tend to improve on the next measurement regardless of intervention. Use a control group to net out this effect.

---

## Metric-Driven Scenarios with Anti-Examples

### Scenario 1: SaaS Feature Rollout — Staggered DiD Gone Wrong

**Context:** A B2B SaaS company (think Salesforce scale) rolls out an AI-assisted forecasting feature to enterprise clients in waves: Wave 1 (January) = 50 accounts, Wave 2 (March) = 80 accounts, Wave 3 (June) = 70 accounts. The product analytics team wants to estimate the causal effect of the feature on quarterly revenue per account.

**Anti-Example (Wrong Approach):**
The analyst runs a classical two-way fixed effects (TWFE) regression: Revenue ~ FeatureAdopted + AccountFE + TimeFE. She reports a coefficient of +$12,000/quarter per account with p < 0.01 and declares the feature a success.

**Why It Fails:**
Under staggered rollout, TWFE uses early adopters (Wave 1) as controls for later adopters (Wave 2, 3). If the feature effect compounds over time (accounts in Wave 1 have had the feature longer), the already-treated Wave 1 accounts serve as contaminated controls for Wave 2 and 3. Under effect heterogeneity, TWFE can produce estimates that are wrong in magnitude or even sign. The analyst is comparing Wave 2 accounts at month 3 to Wave 1 accounts who have been using the feature for 3 months — not a valid counterfactual.

**Correct Approach:**
1. Use the **Callaway-Sant'Anna (2021)** estimator, which computes group-time ATTs (e.g., ATT for Wave 2 accounts at time t relative to their adoption) using only not-yet-treated or never-treated accounts as controls.
2. Construct an **event study plot** with pre-treatment periods (relative time -3, -2, -1 quarters) and verify pre-trends are flat.
3. Report **aggregated ATTs** by wave and time horizon.
4. Key metric: Group-Time ATT with 95% CI; check if SMD < 0.1 across pre-treatment account characteristics.

**Decision Signal:** If Wave 1 ATT at 6 months post-adoption is +$15,000 and Wave 2 ATT at 6 months is +$14,000, the effect is credibly stable and the feature should be accelerated to Wave 3.

---

### Scenario 2: AI Recommendation Engine — Prediction vs Causal Confusion

**Context:** A global e-commerce platform (think Amazon third-party marketplace) trains an ML model to predict which users will churn in the next 30 days (AUC = 0.87). The retention team then sends discount coupons to the top 10% predicted churners.

**Anti-Example (Wrong Approach):**
The team observes that among users who received a coupon, 68% retained vs 54% retention among non-coupon users. They conclude the coupon drove a +14pp retention lift and plan to double the budget.

**Why It Fails:**
This is a classic prediction vs. causation confusion compounded by selection bias. The coupon was sent to predicted high-risk churners. The comparison group (non-coupon users) is systematically different — they were predicted to have lower churn risk. The observed difference conflates the causal effect of the coupon with the selection process. Moreover, some high-risk users would have been retained by other touchpoints; sending them coupons wastes margin. There is no estimate of the counterfactual: what would have happened to coupon recipients without the coupon?

**Correct Approach:**
1. **Uplift modeling (CATE estimation):** Train a causal forest on historical A/B test data (where coupons were randomly assigned) to estimate individual-level treatment effects: CATE_i = E[Y_i(1) - Y_i(0) | X_i].
2. Segment users into four quadrants: Persuadables (CATE > 0, predicted to churn), Sure Things (retained regardless), Lost Causes (churn regardless), Sleeping Dogs (coupon hurts retention).
3. Target only Persuadables for coupons.
4. **Key metric:** Qini coefficient (uplift analog of AUC) for model ranking. Validate with a holdout A/B test.
5. Report: Average CATE among Persuadables, incremental retained users per $1,000 spent.

**Decision Signal:** If CATE-targeted campaign costs $0.42 per incremental retained user vs $1.30 for blanket coupon strategy, targeting saves $0.88 per user — a strong case for causal modeling investment.

---

### Scenario 3: IT Consulting Policy Evaluation — IV with Weak Instrument

**Context:** A management consulting team (McKinsey-style) is evaluating whether mandatory cybersecurity training (Treatment D) reduces data breach incidents (Outcome Y) across 200 enterprise clients. Because training adoption is non-random (paranoid firms self-select), they propose to use the distance from the client's HQ to the nearest certified training center as an instrument (Z), arguing that proximity reduces adoption costs.

**Anti-Example (Wrong Approach):**
The team runs 2SLS: first stage F-statistic = 6.4, Kleibergen-Paap F = 5.9. They proceed to report the 2SLS estimate of –0.3 breaches/year as causal, with narrow confidence intervals. The deck goes to client leadership.

**Why It Fails:**
The first-stage F-statistic of 5.9 is far below the weak instrument threshold of 10 (Stock-Yogo) and 16 (Lee et al.). A weak instrument means 2SLS is nearly as biased as OLS toward zero, and the standard errors are unreliable (can be severely underestimated due to weak identification). The confidence intervals reported are invalid. Additionally, the exclusion restriction may be violated: firms near training centers may be in tech hubs with generally better cybersecurity culture (direct effect of Z on Y not through D).

**Correct Approach:**
1. Report first-stage F and Kleibergen-Paap F prominently. With F < 10, **do not use 2SLS.**
2. If set on IV, search for a stronger or different instrument (e.g., regulatory mandate date variation across jurisdictions with staggered roll-out → DiD-IV hybrid).
3. Alternatively, use **propensity score weighting (IPW)** with observed confounders: firm size, industry, prior breach history, IT budget. Check balance with SMD and Love plot.
4. Run **sensitivity analysis**: Rosenbaum Bounds to determine how much hidden bias would overturn the matched estimate; report E-value.
5. **Key thresholds to report:** First-stage F ≥ 16, SMD < 0.1 on all matching covariates, E-value ≥ 2.0 for the final estimate.

**Decision Signal:** If IPW estimate shows –0.25 breaches/year (95% CI: –0.41 to –0.09) with Rosenbaum Γ = 1.8, this is a credible (if observational) finding to present with appropriate caveats.

---

## Practitioner Playbook

### How to Systematically Tackle Intermediate Causal Analysis Questions

This playbook mirrors the analytical sequence followed by elite consulting, product, and AI research teams. Apply it to exam answers, case interviews, and live project design.

---

#### Step 1: Clarify the Causal Question (2 minutes of framing)

- What is the treatment (D)? Is it binary, continuous, or multi-valued?
- What is the outcome (Y)? What is the time horizon?
- What is the estimand? ATE? ATT? LATE? CATE?
- Who is the target population? All users? Compliers? Specific segment?

**Exam tip:** Explicitly state whether you are estimating ATE (population average), ATT (effect on those actually treated), or LATE (effect on compliers). Confusing these is a top error in MBA case interviews.

---

#### Step 2: Draw the DAG

- List treatment, outcome, and all plausible confounders.
- Draw causal arrows; identify backdoor paths.
- Check: Is the backdoor criterion satisfiable with available data?
- Identify any colliders — variables you must NOT condition on.
- Check: Is there a valid instrument? A valid front-door path?

**Red flag:** If you cannot articulate why each arrow in the DAG exists (based on domain knowledge), your causal model is not credible.

---

#### Step 3: Select the Identification Strategy

Use this decision tree:

```
Can we randomize?
├── YES → Design RCT. Check SUTVA, power, pre-specification.
│          Watch for: novelty effects, non-compliance, attrition.
│          Estimate: ITT, ATT (if non-compliance), CACE (LATE via IV on trial).
│
└── NO → Is there a natural experiment or discontinuity?
    ├── YES (RDD) → Sharp or Fuzzy? Check McCrary test, bandwidth robustness.
    ├── YES (DiD) → Check parallel trends, staggered adoption → Callaway-Sant'Anna.
    ├── YES (IV) → Check F-stat ≥ 16, exclusion restriction, monotonicity.
    └── NO → Observational methods:
               Matching (PSM, CEM) + CIA + Love Plot + SMD
               Sensitivity: E-value, Rosenbaum Bounds
               High dimensions: Double ML, LASSO-based selection
```

---

#### Step 4: Execute and Validate

- **Balance check:** SMD < 0.1 on all pre-treatment covariates; Love Plot.
- **Instrument check:** First-stage F ≥ 16; no exclusion violation arguments.
- **Pre-trends check:** Event study plot; pre-period coefficients ≈ 0.
- **Density check:** McCrary test for RDD.
- **Specification test:** Vary bandwidth, functional form, control set — results stable?
- **Multiple testing:** Bonferroni or BH-FDR for subgroup/secondary analyses.

---

#### Step 5: Interpret and Communicate

- State the estimand clearly: "This estimates the ATT for users who adopted the feature, not the ATE for all users."
- Report the E-value: "An unmeasured confounder would need a risk ratio of X to explain away this finding."
- Give the business decision: "At the observed ATT of +$8,000 per account per quarter, the feature pays for its development cost within 2 quarters."
- State limitations and what additional data or design would strengthen confidence.

---

#### Step 6: Handle Heterogeneity

- Run pre-specified subgroup analyses (not post-hoc fishing).
- Use causal forests or DML to estimate CATE across feature space.
- Visualize CATE distribution; identify top-decile treatment responders.
- Check for effect modification: is the treatment more effective for certain firm sizes, geographies, or engagement tiers?

---

## Content Critique & Depth Gaps

### What Intermediate Topics Need More Depth for IIM/HBS MBA Level

#### 1. Asymptotic Theory Behind 2SLS
The Q&A set covers the mechanics of 2SLS and the Wald estimator but does not address the finite sample properties of IV estimators, the Anderson-Rubin confidence interval (which is robust to weak instruments even when the standard Wald CI is not), or limited information maximum likelihood (LIML) as an alternative to 2SLS under weak identification. IIM/HBS-level questions may probe these alternatives.

#### 2. Causal Forests — Algorithm Mechanics
The set mentions causal forests as a method for CATE estimation but does not explain the honesty requirement (splitting samples for tree building vs. leaf estimation), the role of cross-fitting, or how the generalized random forest (GRF) package implements asymptotically valid confidence intervals for CATEs. A working knowledge of these internals is expected in AI product and data science leadership roles.

#### 3. Synthetic DiD (Arkhangelsky et al. 2021)
Synthetic control is mentioned, but synthetic DiD — which combines the matrix completion approach of synthetic control with the parallel trends logic of DiD — is absent. This is increasingly the method of choice for geographic marketing experiments at tech companies (Meta, Google) and is a likely exam/interview topic at the MBA level.

#### 4. Interference and Network Effects
SUTVA violations from network interference are acknowledged via the two-sided market discussion, but the formal literature on cluster-randomized experiments, bipartite experiments, and Bernoulli/Horvitz-Thompson estimators under interference is not covered. This is essential for social platforms (LinkedIn, Twitter/X) where any A/B test faces network spillover.

#### 5. Regression Discontinuity with Multiple Cutoffs
The Q&A covers basic sharp and fuzzy RDD but does not address RDD with multiple cutoffs (e.g., performance bands in HR systems), kink regression discontinuity (RKD — where the slope changes rather than the level), or geographic RDD. These extensions frequently appear in consulting and policy contexts.

#### 6. Sensitivity Analysis Depth
E-value is mentioned but the set does not cover Sensitivity Analysis via Partial R² (Cinelli-Hazlett framework), which is more interpretable and directly connects to the explained variance of a potential confounder. This is the state of the art in observational causal inference for business settings.

#### 7. Pre-Analysis Plans and Registered Reports
The Q&A notes pre-specification but does not walk through what a rigorous pre-analysis plan contains (primary vs. secondary endpoints, sample size justification, exact model specification, subgroup list, stopping rules). IIM case competitions increasingly require PAP-level rigor.

#### 8. Dose-Response / Continuous Treatment
The Q&A mentions dose-response relationships but lacks coverage of generalized propensity scores for continuous treatments, the dose-response function estimation, and how to construct confidence bands. Many real-world treatments are continuous (ad spend, hours of training, dosage).

### What Is Absent from This Q&A Set

- **Difference-in-Discontinuities (DiD + RDD):** Combines RDD with DiD for policies that affect only some groups at the cutoff; used in regulatory impact assessments.
- **Quantile Treatment Effects (QTE):** Average treatment effects obscure distributional impacts. Whether a pricing intervention raises the median or the 90th percentile of revenue matters strategically.
- **Marginal Structural Models (MSMs):** For time-varying treatments with time-varying confounders, standard methods break down; MSMs with stabilized IPW are the solution.
- **Interference in Recommender Systems:** When algorithmic recommendations cause network-level shifts (one user seeing a recommendation changes what others see), standard experimental units are not independent.
- **Long-Run vs. Short-Run Causal Effects:** Novelty effects, learning curves, and equilibrium adjustments mean short-run A/B test results may not predict long-run product value. Techniques: long-run instrumental variables, holdout analysis.

---

## Quick-Recall Card

**Must-Know Intermediate Concepts — Causal Analysis in Business**

**Randomization & Experiments**
- Gold standard because randomization severs all backdoor paths (confounders balanced in expectation).
- A/B test validity requires: SUTVA, pre-specification, sufficient power, absence of novelty effects.
- Novelty effect: inflate short-run treatment estimates; test by looking at effect decay over time.
- Non-compliance: ITT (intent-to-treat) is conservative and policy-relevant; use IV on the trial data (CACE = LATE) for complier-specific effect.

**Difference-in-Differences**
- Parallel trends is the core assumption — not testable definitively, but event study pre-trends provide evidence.
- Staggered adoption breaks classical TWFE — use Callaway-Sant'Anna or Sun-Abraham.
- Anticipation effects: treatment group reacts before treatment date → pre-trends look bad even if assumption holds.

**Instrumental Variables**
- Three pillars: relevance (F ≥ 16), exogeneity (Z ⊥ U), exclusion restriction (Z → Y only via D).
- Wald estimator = Reduced Form / First Stage.
- IV estimates LATE (compliers only), not ATE.
- Weak instruments (F < 10) bias 2SLS toward OLS; use Anderson-Rubin CI for robustness.

**Regression Discontinuity**
- Sharp: P(D|X) jumps 0→1 at cutoff. Fuzzy: partial jump → use as IV.
- McCrary density test: detect running variable manipulation.
- Bandwidth: MSE-optimal (Calonico-Cattaneo-Titiunik); validate with half and double bandwidth.
- Estimates only local effect at cutoff — limited external validity.

**Matching and Weighting**
- Propensity score matching: CIA (conditional independence assumption) required — no unmeasured confounders.
- SMD < 0.1 on all covariates post-match — report Love Plot.
- IPW: inverse probability weighting — can have unstable weights; trim extreme propensity scores.
- CIA is not testable — argue via rich covariate set and domain knowledge.

**Sensitivity Analysis**
- E-value: minimum confounder strength to explain away effect. Report always for observational studies.
- Rosenbaum Bounds Γ: hidden bias required to overturn conclusion. Γ > 2 = robust.
- Cinelli-Hazlett Partial R² framework: more interpretable alternative to E-value.

**Machine Learning for Causal Inference**
- Double ML: partial out controls with ML, estimate causal effect in residual regression. Requires cross-fitting.
- Causal forests: nonparametric CATE estimation; honesty property for valid CIs.
- LASSO: variable selection for control set; use caution — may drop important confounders.
- Do not use prediction model outputs as causal estimates.

**DAGs and Structural Assumptions**
- Backdoor criterion: block all paths from D to Y that have an arrow into D.
- Collider bias: conditioning on a collider opens spurious paths — avoid controlling for post-treatment variables.
- Frontdoor criterion: usable when all of D's effect passes through an unconfounded mediator M.

**Heterogeneous Treatment Effects**
- CATE (Conditional ATE): varies across subgroups — key for targeting and personalization.
- Causal forest or DML: estimate CATE; validate with RATE (Rank-Weighted Average Treatment Effect).
- Pre-specify subgroups; FDR correction for post-hoc subgroup fishing.

**Multiple Testing and Pre-Analysis Plans**
- Bonferroni: α/k; conservative. Benjamini-Hochberg: controls FDR; preferred in exploratory work.
- Pre-analysis plan: pre-specify primary endpoint, model, subgroups, sample size — eliminates post-hoc inflation.
- p-hacking: running analysis until significant result found; mitigated by PAP and pre-registration.

**Mediation and Moderation**
- Mediation (HOW): indirect effect = a-path × b-path; proportion mediated = indirect / total.
- Moderation (FOR WHOM): Y = β1*X + β2*W + β3*(X*W); β3 tests interaction.
- SEM: system of equations encoding both; fit diagnostics: RMSEA < 0.08, CFI > 0.95.

**Key Thresholds at a Glance**
- IV First-Stage F ≥ 16 (Lee et al.) | ≥ 10 (Stock-Yogo)
- VIF > 10: problematic multicollinearity
- SMD < 0.1: acceptable covariate balance
- RMSEA < 0.08, CFI > 0.95: SEM fit
- Power ≥ 0.80 | α = 0.05 (standard)
- Γ > 1.5: moderate Rosenbaum robustness

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Have I ruled out all plausible alternative explanations — confounding, reverse causation, selection bias, and interference — before attributing this observed pattern to the treatment, and can I quantify how sensitive that conclusion is to what I cannot observe?"

---

## Self-Audit Report

<!-- Self-Audit:
WORKER: A10
TARGET FILE: /Users/harshitpanikar/Documents/s_d_1/audit_management_course/causal-analysis-business/14-qa-intermediate.md
SCOPE: Q71–Q140 (70 Intermediate Questions) — Causal Analysis in Business

SECTION COMPLETENESS CHECK:
[PASS] Section 1 — Jargon Buster: 12 terms included (minimum 8 required). All terms drawn from intermediate Q&A topics: SUTVA, LATE, McCrary, Parallel Trends, Propensity Score, Collider Bias, E-value, Synthetic Control, Callaway-Sant'Anna, Double ML, Uplift Modeling, Rosenbaum Bounds.
[PASS] Section 2 — Frameworks & Mental Models: 5 ASCII diagrams included — IV Validity Checklist, DiD Assumptions Diagram, DAG (Backdoor/Frontdoor/Collider), RDD Sharp vs Fuzzy, Mediation vs Moderation.
[PASS] Section 3 — Formulas, Thresholds & Rules of Thumb: All key thresholds present — F ≥ 10/16, SMD < 0.1, E-value formula, Rosenbaum Γ, RMSEA < 0.08, CFI > 0.95, VIF > 10, Bonferroni/BH-FDR, Cohen's d benchmarks, Power ≥ 0.80.
[PASS] Section 4 — Do/Don't: 10 DOs and 10 DON'Ts (exceeds minimum 8 each).
[PASS] Section 5 — Metric-Driven Scenarios with Anti-Examples: 3 scenarios — SaaS staggered DiD, AI recommendation prediction vs causation confusion, IT consulting IV with weak instrument. Each includes anti-example, failure diagnosis, correct approach, and decision signal metrics.
[PASS] Section 6 — Practitioner Playbook: 6-step systematic playbook with decision tree, instrument checklist, balance diagnostics, interpretation guidance, and heterogeneity handling.
[PASS] Section 7 — Content Critique & Depth Gaps: 8 depth gaps identified (2SLS asymptotics, causal forest mechanics, synthetic DiD, interference, multiple-cutoff RDD, Cinelli-Hazlett, PAP rigor, dose-response continuous treatment) + 5 absent topics (DiD+RDD, QTE, MSMs, recommender interference, long-run effects).
[PASS] Section 8 — Quick-Recall Card: 8 thematic recall sections. Final sentence begins exactly "As a PM/Consultant/AI Lead" as required.
[PASS] Section 9 — Self-Audit Report: This HTML comment block.

INDUSTRY LENS VERIFICATION: IT/AI/Product/Consulting lens applied throughout — scenarios use SaaS rollouts, AI recommendation engines, IT consulting engagements; examples reference Salesforce-scale B2B, e-commerce platforms, McKinsey-style consulting. All frameworks grounded in product/consulting application.

ESTIMATED FILE SIZE: ~17 KB (substantially exceeds 13 KB minimum).

IIM/HBS DEPTH ASSESSMENT: Intermediate-to-advanced depth achieved. Covers estimand distinctions (ATE/ATT/LATE/CATE), modern DiD estimators (Callaway-Sant'Anna), weak instrument theory (Lee et al. threshold), sensitivity analysis (E-value, Rosenbaum Γ), ML-for-causal-inference (Double ML, causal forests, uplift), and DAG-based reasoning — all at the level expected for MBA strategy/analytics courses.

CONNECTS TO:
  - 01-foundations-qa.md (basic causal concepts, RCT design fundamentals)
  - 06-iv-advanced.md (instrumental variables deep dive)
  - 08-did-panel.md (difference-in-differences and panel data methods)
  - 10-matching-weighting.md (propensity score and IPW methods)
  - 12-ml-causal.md (machine learning for causal inference)
  - 15-qa-advanced.md (advanced Q&A, Q141–Q210)

AUDIT PASSED: All 9 sections present, all minimums exceeded, all required phrases present.
DATE: 2026-04-18
-->

**Connects to:**
- `01-foundations-qa.md` — Basic causal concepts, RCT design fundamentals
- `06-iv-advanced.md` — Instrumental variables: 2SLS mechanics, weak instrument diagnostics
- `08-did-panel.md` — Difference-in-Differences, panel data, staggered adoption
- `10-matching-weighting.md` — Propensity score matching, IPW, covariate balance
- `12-ml-causal.md` — Double ML, causal forests, LASSO for causal inference
- `15-qa-advanced.md` — Advanced Q&A (Q141–Q210)
