# AI Evaluation Engineer: 30 interview questions with model answers

Thirty scenarios on eval design, LLM-as-judge, regression testing, human review and safety evaluation. Write your own answer first, then open the model answer to compare structure and reasoning.

Level mix: 4 Foundation, 16 Practitioner, 10 Advanced. Each question lists what the interviewer is testing, a model answer, red-flag answers to avoid, and the follow-up to expect.

## Contents

1. [How do you build an eval set for a new LLM feature?](#q1) (Eval Design, Practitioner)
2. [What are the risks of using an LLM as a judge, and how do you mitigate them?](#q2) (LLM-as-Judge, Advanced)
3. [How do you choose metrics for a summarisation or Q&A system?](#q3) (Metrics, Practitioner)
4. [How do you stop prompt or model changes from silently breaking quality?](#q4) (Regression, Practitioner)
5. [How do you design a reliable human annotation process?](#q5) (Human Review, Practitioner)
6. [How do offline evals and online metrics work together?](#q6) (Online vs Offline, Practitioner)
7. [How would you evaluate a model for harmful or biased outputs?](#q7) (Safety Evals, Advanced)
8. [A vendor claims state-of-the-art benchmark scores. Do you trust them?](#q8) (Benchmarks, Foundation)
9. [How do you keep a golden dataset useful over time?](#q9) (Golden Datasets, Practitioner)
10. [When is synthetic data appropriate for evals?](#q10) (Synthetic Data, Practitioner)
11. [How do you evaluate a RAG system?](#q11) (RAG Evals, Practitioner)
12. [How do you evaluate multi-step agent trajectories?](#q12) (Agent Evals, Advanced)
13. [LLM eval scores fluctuate between runs. How do you draw reliable conclusions?](#q13) (Statistical Rigour, Advanced)
14. [When do you use pairwise comparison instead of absolute scoring?](#q14) (Scoring Methods, Practitioner)
15. [What makes a good evaluation rubric?](#q15) (Rubric Design, Foundation)
16. [Your eval suite is slow and expensive. How do you fix it?](#q16) (Eval Cost, Practitioner)
17. [How do you detect and avoid benchmark contamination?](#q17) (Contamination, Advanced)
18. [How do you evaluate quality across languages?](#q18) (Multilingual Evals, Practitioner)
19. [How do you evaluate open-ended tasks with no single right answer?](#q19) (No Ground Truth, Advanced)
20. [How do you do error analysis on failing cases?](#q20) (Error Analysis, Practitioner)
21. [How do you report eval results to executives?](#q21) (Reporting, Foundation)
22. [How do you structure a red-teaming exercise?](#q22) (Red Teaming, Advanced)
23. [How do you check whether a model's confidence can be trusted?](#q23) (Calibration, Advanced)
24. [How do you A/B test an LLM feature?](#q24) (A/B Testing, Practitioner)
25. [How do you build an eval-driven culture in a team?](#q25) (Eval Culture, Practitioner)
26. [Your LLM judge and your human reviewers disagree on 30% of cases. What do you do?](#q26) (Judge Design, Advanced)
27. [How do you monitor quality in production when you have no ground-truth labels?](#q27) (Production Monitoring, Practitioner)
28. [How do you decide how large your eval set needs to be?](#q28) (Eval Data, Practitioner)
29. [What would you look for when choosing an evaluation framework or platform?](#q29) (Tooling, Foundation)
30. [Tell me about a time an evaluation result changed a decision the team had already made.](#q30) (Behavioural, Advanced)

<a id="q1"></a>

### 1. How do you build an eval set for a new LLM feature?

**Competency:** Eval Design | **Level:** Practitioner

**What it tests:** Whether your eval set covers real, edge and adversarial cases.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I collect real inputs from logs, support tickets and domain experts, then add synthetic cases to cover rare, edge and adversarial situations. Each item gets an expert-labelled answer or a rubric, and the set is versioned like code. I tag items by scenario so I can report results by segment. A held-out portion stays untouched so prompts are not tuned to the tests. The set is never finished: production failures flow back in, and I review coverage regularly against how users actually use the feature.

**Red-flag answers**

- Uses only easy or synthetic examples
- Keeps no held-out set
- Has no labelled answers or rubrics

**Expect this follow-up:** How do you know your eval set covers real usage?

</details>

<a id="q2"></a>

### 2. What are the risks of using an LLM as a judge, and how do you mitigate them?

**Competency:** LLM-as-Judge | **Level:** Advanced

**What it tests:** Whether you calibrate judges against humans and known biases.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

LLM judges show position bias, length bias and a preference for their own style, and they can be inconsistent between runs. I mitigate by writing clear rubrics with score definitions and examples, randomising answer order, and using a judge from a different model family than the one being graded. Most importantly I calibrate against human labels: I measure agreement on a sample, and I keep auditing samples over time because judge behaviour drifts when models update. A judge I have not validated against humans is an opinion, not a metric.

**Red-flag answers**

- Trusts the judge without calibration
- Ignores position and length bias
- Uses the same model to generate and judge

**Expect this follow-up:** Judge and human agree only 65% of the time. What do you do?

</details>

<a id="q3"></a>

### 3. How do you choose metrics for a summarisation or Q&A system?

**Competency:** Metrics | **Level:** Practitioner

**What it tests:** Whether metrics map to the failures that matter.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start from the failure that matters for the product. For summarisation that might be factual errors and missed key points; for Q&A, wrong or unsupported answers. I define metrics for each dimension, such as factuality, completeness, relevance and tone, and combine automatic checks, rubric-based judging and human review for the harder calls. Results are reported by segment, because an average can hide a group of users who are badly served. I retire metrics that no longer predict user satisfaction.

**Red-flag answers**

- Reports one average metric
- Uses BLEU or ROUGE alone
- Ignores factuality

**Expect this follow-up:** Summaries score well but users say they miss key points. What's wrong?

</details>

<a id="q4"></a>

### 4. How do you stop prompt or model changes from silently breaking quality?

**Competency:** Regression | **Level:** Practitioner

**What it tests:** Whether evals gate releases in CI with real thresholds.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I put the eval suite in CI so every prompt, model or retrieval change is scored automatically against the baseline. Each critical metric and segment has a threshold, and the comparison uses confidence intervals so noise is not mistaken for a change. A change that regresses a critical case blocks the release, with an explicit override that needs an owner's sign-off. I also monitor production, because some regressions only appear on real traffic. Silent breakage happens when nobody is measuring, so I make measurement automatic.

**Red-flag answers**

- Tests manually before release
- Sets no thresholds or baselines
- Ignores segment-level regressions

**Expect this follow-up:** The overall score rose but one critical segment dropped. Do you ship?

</details>

<a id="q5"></a>

### 5. How do you design a reliable human annotation process?

**Competency:** Human Review | **Level:** Practitioner

**What it tests:** Whether annotation is reliable and agreement is measured.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I write guidelines with clear definitions and worked examples, train annotators and run a pilot round before scaling. A subset of items is labelled by several raters so I can measure inter-rater agreement, using a statistic that corrects for chance. Disagreements are reviewed together, and they usually reveal ambiguous rubric wording that I then fix. I monitor annotator quality over time with hidden gold items, and I keep the guidelines versioned. Low agreement means the task definition is unclear, not that raters are careless.

**Red-flag answers**

- Skips guidelines and training
- Uses a single annotator
- Never measures agreement

**Expect this follow-up:** Raters keep disagreeing on one criterion. What do you fix?

</details>

<a id="q6"></a>

### 6. How do offline evals and online metrics work together?

**Competency:** Online vs Offline | **Level:** Practitioner

**What it tests:** Whether offline scores are validated against real outcomes.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Offline evals are cheap, fast and repeatable, so they gate releases. Online metrics such as acceptance rate, edits, retries, complaints and task completion show how the feature behaves with real users. The two must connect: I check whether offline scores actually predict online outcomes, and if they do not, I fix the offline eval. Production failures and disagreements are fed back as new offline cases. Each side covers the other's blind spot: offline misses real usage, and online is slow and noisy.

**Red-flag answers**

- Relies on offline scores alone
- Ignores online signals
- Never checks that offline predicts online

**Expect this follow-up:** Offline scores improved but users are less satisfied. Why?

</details>

<a id="q7"></a>

### 7. How would you evaluate a model for harmful or biased outputs?

**Competency:** Safety Evals | **Level:** Advanced

**What it tests:** Whether you test harm and group gaps systematically.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I define harm categories and user groups relevant to the product, build test prompts for each, and mix expert-written and automated adversarial attacks. I measure violation and refusal rates, including over-refusal of legitimate requests, and compare performance across demographic groups and languages to find gaps. After mitigations I re-test to confirm they worked without creating new problems. Results feed explicit release criteria with thresholds and owners. A one-time safety review is not enough, because models and prompts change.

**Red-flag answers**

- Tests only obvious harmful prompts
- Ignores group-level gaps
- Doesn't re-test after fixes

**Expect this follow-up:** How do you decide the residual risk is acceptable?

</details>

<a id="q8"></a>

### 8. A vendor claims state-of-the-art benchmark scores. Do you trust them?

**Competency:** Benchmarks | **Level:** Foundation

**What it tests:** Whether you distrust claims that skip your own task.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Not on their own. Public benchmarks can be contaminated by training data, saturate quickly, and often measure something different from my task. A vendor's number also comes from their prompts and settings, not mine. I run the candidate model on my own eval set with my prompts, and compare quality alongside cost, latency, context limits and data terms. The benchmark can help build a shortlist, but the decision rests on evidence from my data. If the vendor will not let me test, that is itself informative.

**Red-flag answers**

- Accepts the claim as fact
- Ignores contamination
- Doesn't test cost and latency

**Expect this follow-up:** The model wins on the vendor's benchmark and loses on yours. What do you report?

</details>

<a id="q9"></a>

### 9. How do you keep a golden dataset useful over time?

**Competency:** Golden Datasets | **Level:** Practitioner

**What it tests:** Whether datasets evolve with production failures.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A golden dataset decays if it is frozen. I version it, add new failures from production, retire cases that no longer reflect how the product is used, and review labels periodically since standards and facts change. I track coverage across use cases and user segments so gaps are visible. I keep a protected held-out slice to avoid overfitting. Each change to the dataset is logged so score changes can be explained by a code change or a dataset change, and not confused.

**Red-flag answers**

- Freezes the dataset
- Never adds production failures
- Doesn't review labels

**Expect this follow-up:** How often would you refresh it, and what triggers a change?

</details>

<a id="q10"></a>

### 10. When is synthetic data appropriate for evals?

**Competency:** Synthetic Data | **Level:** Practitioner

**What it tests:** Whether you use synthetic data without fooling yourself.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Synthetic data is useful for expanding coverage of rare or adversarial cases and for bootstrapping before real traffic exists. I validate samples by hand, mix them with real data and label them so results can be split. I avoid using the same model to both generate and grade the data, because that inflates scores. Synthetic items tend to be cleaner and more predictable than real ones, so I never rely on them alone to judge readiness. As real data arrives it takes over.

**Red-flag answers**

- Uses synthetic data only
- Lets the same model generate and grade
- Doesn't validate samples by hand

**Expect this follow-up:** Where could synthetic data mislead you?

</details>

<a id="q11"></a>

### 11. How do you evaluate a RAG system?

**Competency:** RAG Evals | **Level:** Practitioner

**What it tests:** Whether you evaluate retrieval and generation separately.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I evaluate retrieval and generation separately. For retrieval I measure recall, precision and ranking quality against labelled relevant passages. For generation I measure faithfulness to the retrieved sources, answer relevance and completeness, and I test unanswerable questions to check the system says so. Separating the two shows whether to fix search or the prompt. A wrong answer can come from missing context or from misusing good context, and the fix is different. I also track citation accuracy where the product shows sources.

**Red-flag answers**

- Evaluates only final answers
- Doesn't separate retrieval from generation
- Ignores faithfulness to sources

**Expect this follow-up:** Recall is high but answers are wrong. Where do you look next?

</details>

<a id="q12"></a>

### 12. How do you evaluate multi-step agent trajectories?

**Competency:** Agent Evals | **Level:** Advanced

**What it tests:** Whether you score trajectories, not just outcomes.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I judge the outcome and the path. Outcome checks ask whether the task was completed correctly. Path checks look at tool choices, unnecessary or repeated steps, policy or safety violations, recovery from errors, cost and latency. I use sandboxed environments with mocked or resettable tools so runs are repeatable, and I run each scenario several times because behaviour varies. Trajectory-level scoring can use rubrics or judges calibrated against humans. Only checking the final message misses agents that get the right answer by risky means.

**Red-flag answers**

- Judges only the final outcome
- Ignores unnecessary steps and unsafe actions
- Runs on live systems

**Expect this follow-up:** Two agents succeed, one in 5 steps and one in 40. How do you compare them?

</details>

<a id="q13"></a>

### 13. LLM eval scores fluctuate between runs. How do you draw reliable conclusions?

**Competency:** Statistical Rigour | **Level:** Advanced

**What it tests:** Whether you draw conclusions with proper statistics.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Because outputs vary, I use enough samples for the effect size I care about and repeat runs to estimate noise. I report confidence intervals, control randomness where I can with fixed seeds and settings, and use paired comparisons, since the same items run under both versions reduce variance. I avoid concluding anything from small differences, and I check by segment, correcting for the number of comparisons I make. If a change is within the noise, I say so, and I either collect more data or treat it as no difference.

**Red-flag answers**

- Concludes from small score differences
- Runs each case once
- Reports no confidence intervals

**Expect this follow-up:** How many runs would you do to trust a 2-point gain?

</details>

<a id="q14"></a>

### 14. When do you use pairwise comparison instead of absolute scoring?

**Competency:** Scoring Methods | **Level:** Practitioner

**What it tests:** Whether you match the scoring method to the decision.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Pairwise comparison asks which of two answers is better, and people and judges are more consistent at that than at assigning absolute scores, especially for subjective qualities like helpfulness or tone. It is the right tool for comparing two versions. Absolute rubrics suit pass or fail thresholds, safety criteria and tracking a metric over time. I often use both: pairwise for choosing between candidates and rubric scores for gating and trends. I randomise order in pairwise tests to remove position bias.

**Red-flag answers**

- Uses absolute scores for everything
- Doesn't know when pairwise helps
- Ignores rater consistency

**Expect this follow-up:** Which method would you use to track quality over six months, and why?

</details>

<a id="q15"></a>

### 15. What makes a good evaluation rubric?

**Competency:** Rubric Design | **Level:** Foundation

**What it tests:** Whether criteria are specific, observable and separable.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A good rubric has specific, observable criteria, clear definitions for each score level with examples, and separates dimensions such as accuracy, completeness and tone instead of blending them into one number. I keep the scale small so raters can distinguish the levels. Then I test it: several raters score the same items, I measure agreement, and I revise wording where they disagree. A vague rubric like 'is it good' produces noisy scores that cannot support decisions.

**Red-flag answers**

- Uses vague criteria like 'good quality'
- Bundles accuracy and tone together
- Never tests with several raters

**Expect this follow-up:** Write one criterion with score definitions for 'helpfulness'.

</details>

<a id="q16"></a>

### 16. Your eval suite is slow and expensive. How do you fix it?

**Competency:** Eval Cost | **Level:** Practitioner

**What it tests:** Whether you tier evals to stay fast and affordable.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I tier the suite. A small, fast smoke set runs on every change, the fuller suite runs nightly or before release, and the most expensive checks, such as human review, run only at milestones. I cache results for unchanged inputs, sample smartly instead of running everything, remove redundant cases and use cheaper judges once I have calibrated them against a stronger one. I track the cost of each eval so I can see where the money goes. The aim is fast feedback for developers without giving up coverage.

**Red-flag answers**

- Runs the full suite on every change
- Cuts cases at random
- Uses cheaper judges without calibration

**Expect this follow-up:** Which tests go in the fast tier, and why?

</details>

<a id="q17"></a>

### 17. How do you detect and avoid benchmark contamination?

**Competency:** Contamination | **Level:** Advanced

**What it tests:** Whether you protect evals from leakage into training.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Contamination means the model saw the test items during training, which inflates scores. I keep private held-out sets that never appear publicly, use fresh or paraphrased items, and check for verbatim overlap with known corpora where I can. I prefer task-specific evals built from my own data over public leaderboards, and I look for suspicious signs such as very high scores on old items but lower ones on new but similar items. I treat any public benchmark result with caution.

**Red-flag answers**

- Trusts public leaderboards
- Keeps no private held-out set
- Doesn't check for overlap

**Expect this follow-up:** How would you suspect a model has seen your test data?

</details>

<a id="q18"></a>

### 18. How do you evaluate quality across languages?

**Competency:** Multilingual Evals | **Level:** Practitioner

**What it tests:** Whether you evaluate each language with native reviewers.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I build test sets per language, written or reviewed by native speakers, using real user text including code-mixed and transliterated input. I compare scores by language and never assume English results transfer. I check for translation artefacts in the data, cultural fit and tone, and I include language-specific failure modes such as wrong script or mixed languages in the reply. Judge models can be weaker in some languages, so I calibrate them against native-speaker ratings before trusting them.

**Red-flag answers**

- Assumes English results transfer
- Uses machine-translated tests only
- Has no native reviewers

**Expect this follow-up:** Scores are lower in Tamil. How do you tell if it's the model or the test?

</details>

<a id="q19"></a>

### 19. How do you evaluate open-ended tasks with no single right answer?

**Competency:** No Ground Truth | **Level:** Advanced

**What it tests:** Whether you can evaluate open-ended output credibly.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

When there is no single right answer, I define what good looks like through rubrics covering properties such as factuality against sources, coverage of key points, clarity and safety. I combine expert review, pairwise preference comparisons and automated property checks, and calibrate any LLM judge against human ratings, tracking agreement over time. I accept that scores are noisy and report distributions, not a single number. The goal is not certainty but decisions that are better informed than opinion.

**Red-flag answers**

- Insists on one right answer
- Relies on exact match
- Never checks the judge against humans

**Expect this follow-up:** How do you evaluate a creative-writing assistant?

</details>

<a id="q20"></a>

### 20. How do you do error analysis on failing cases?

**Competency:** Error Analysis | **Level:** Practitioner

**What it tests:** Whether you turn failures into a prioritised taxonomy.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I sample failures, read them carefully and group them into a taxonomy such as retrieval miss, misread instruction, hallucination, formatting or tool error. Then I count frequency and severity for each category and trace root causes. This gives a prioritised fix list: the biggest and most severe category first. I review the taxonomy as the product changes, and I keep examples of each category so the team shares one language. Error analysis is usually the highest-value hour in an eval process.

**Red-flag answers**

- Reads a few failures anecdotally
- Has no failure taxonomy
- Doesn't rank by frequency and severity

**Expect this follow-up:** You have 200 failures. How do you start?

</details>

<a id="q21"></a>

### 21. How do you report eval results to executives?

**Competency:** Reporting | **Level:** Foundation

**What it tests:** Whether results become a decision, not a score dump.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Executives need a decision, not a data dump. I give a one-page view: headline metrics against agreed thresholds, the trend over time, the top failure categories with examples, the remaining risk, and a clear recommendation to ship, hold or fix. I explain what the numbers mean in business terms and state the uncertainty honestly. Detail is available in an appendix for those who want it. If the recommendation is not obvious from the first paragraph, the report is too complicated.

**Red-flag answers**

- Sends raw score dumps
- Gives no thresholds or recommendation
- Hides failure categories

**Expect this follow-up:** What one sentence would you say to an executive about release readiness?

</details>

<a id="q22"></a>

### 22. How do you structure a red-teaming exercise?

**Competency:** Red Teaming | **Level:** Advanced

**What it tests:** Whether red teaming is structured and feeds release gates.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start by defining harm categories and threat models relevant to the product, including realistic attackers and misuse. I combine expert human red-teamers, who are creative, with automated attack generation, which gives scale. Every attempt is recorded with its outcome so I can report success rates. Findings are triaged, fixed and retested, and successful attacks are added to the eval suite as permanent regression tests. The exercise feeds release gates and is repeated when the model, prompt or tools change.

**Red-flag answers**

- Runs a one-off jailbreak session
- Has no threat model or harm categories
- Lets findings skip the release gates

**Expect this follow-up:** How do you turn red-team findings into permanent tests?

</details>

<a id="q23"></a>

### 23. How do you check whether a model's confidence can be trusted?

**Competency:** Calibration | **Level:** Advanced

**What it tests:** Whether you test if confidence tracks accuracy.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I compare the model's confidence, whether stated or derived from token probabilities or self-consistency, with actual accuracy. Calibration plots and error rates by confidence band show whether a 90% confident answer is right about 90% of the time. If confidence is well calibrated, I can use it for routing, abstention and human escalation. If not, I recalibrate or use other signals, such as retrieval agreement. Verbalised confidence from LLMs is often overconfident, so I never assume it is reliable without checking.

**Red-flag answers**

- Takes model-stated confidence at face value
- Uses no calibration plots
- Doesn't use confidence for routing

**Expect this follow-up:** The model says 95% confident but is right 70% of the time. What do you do?

</details>

<a id="q24"></a>

### 24. How do you A/B test an LLM feature?

**Competency:** A/B Testing | **Level:** Practitioner

**What it tests:** Whether you run experiments with guardrail metrics.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I define a primary metric and guardrail metrics such as cost, latency and safety before starting. Users are randomly assigned, the test runs long enough to reach significance and cover weekly patterns, and I watch for novelty effects that fade. I also read a sample of actual outputs from both arms, because a metric like engagement can improve while quality falls. I decide in advance what result would make me ship, hold or stop, so I do not rationalise afterwards.

**Red-flag answers**

- Ends the test early on a good day
- Has no guardrail metrics
- Ignores cost and novelty effects

**Expect this follow-up:** The variant wins on clicks but complaints rise. What do you do?

</details>

<a id="q25"></a>

### 25. How do you build an eval-driven culture in a team?

**Competency:** Eval Culture | **Level:** Practitioner

**What it tests:** Whether evals become habit, not a launch event.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I make evals easy to run so nobody has an excuse to skip them: one command, fast feedback, clear output. They run in CI, appear on team dashboards and are part of the definition of done. Every production bug becomes a test case so the same failure does not return. I celebrate catches, where an eval prevented a bad release, and I share failure examples openly. Culture changes when people see evals saving them time and embarrassment, not when they are mandated.

**Red-flag answers**

- Runs evals only before big launches
- Makes evals hard to run
- Doesn't turn production bugs into tests

**Expect this follow-up:** How would you make evals part of the definition of done?

</details>

<a id="q26"></a>

### 26. Your LLM judge and your human reviewers disagree on 30% of cases. What do you do?

**Competency:** Judge Design | **Level:** Advanced

**What it tests:** Whether you diagnose disagreement rather than simply trusting one side.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I would not assume either side is right. I sample the disagreements and read them, looking for patterns: the judge favouring longer answers, humans and the judge reading the rubric differently, or genuinely ambiguous items. If the rubric is unclear, I fix it and re-label. If the judge has a systematic bias, I adjust the prompt, add examples or change the judge model. Then I re-measure agreement on a fresh sample. Until agreement is acceptable, I use the judge only for trends, not for gating releases.

**Red-flag answers**

- Trusts the judge because it is cheaper
- Discards the human labels
- Never reads the disagreeing cases

**Expect this follow-up:** How much agreement would you require before letting the judge gate a release?

</details>

<a id="q27"></a>

### 27. How do you monitor quality in production when you have no ground-truth labels?

**Competency:** Production Monitoring | **Level:** Practitioner

**What it tests:** Whether you use proxy signals, sampling and drift detection sensibly.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I combine several proxy signals: user feedback, edits, retries and abandonment, automated checks for format, grounding and policy, and an LLM judge scoring a sample of traffic. Regular human review of a random sample keeps everything honest. I watch trends and distributions for drift in input types, output length or refusal rates, and alert on changes. Flagged and low-scoring cases feed the eval set. No single proxy is trustworthy alone, but together they catch most problems early.

**Red-flag answers**

- Waits for customers to complain
- Relies on a single proxy metric
- Reviews no real samples

**Expect this follow-up:** Thumbs-down rates are flat but you suspect quality has fallen. How do you check?

</details>

<a id="q28"></a>

### 28. How do you decide how large your eval set needs to be?

**Competency:** Eval Data | **Level:** Practitioner

**What it tests:** Whether you connect sample size to the decision and effect size.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

It depends on the decision. To detect a small improvement with confidence I need many items; to catch big failures a smaller set is enough. I estimate the noise from repeated runs, decide the smallest difference I care about, and calculate the sample size needed. I also need enough items per segment to report on each one. Quality matters as much as quantity: a few hundred well-labelled, representative cases beat thousands of poor ones. I grow the set where uncertainty is highest.

**Red-flag answers**

- Picks a round number arbitrarily
- Ignores per-segment counts
- Values size over label quality

**Expect this follow-up:** Your set has 200 items and two versions differ by 2 points. What do you conclude?

</details>

<a id="q29"></a>

### 29. What would you look for when choosing an evaluation framework or platform?

**Competency:** Tooling | **Level:** Foundation

**What it tests:** Whether you choose tools by workflow fit rather than popularity.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I look at how well it fits our workflow: running in CI, versioning datasets and prompts, supporting custom metrics and judges, tracing production requests and comparing runs side by side. I check data privacy, cost, export options to avoid lock-in, and how easily non-engineers such as reviewers can use it. I prototype on one real feature before committing. Sometimes a small in-house harness is enough, and a heavy platform adds overhead without value.

**Red-flag answers**

- Picks the most popular tool by default
- Ignores data privacy and export
- Never prototypes on a real feature

**Expect this follow-up:** Would you build or buy for a team of five engineers? Why?

</details>

<a id="q30"></a>

### 30. Tell me about a time an evaluation result changed a decision the team had already made.

**Competency:** Behavioural | **Level:** Advanced

**What it tests:** Whether you can influence decisions with evidence and handle pushback.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A strong answer describes a specific case where the eval contradicted expectation, such as a new model that looked better in demos but scored worse on an important segment. I would explain how I checked the result was reliable, presented it clearly with examples and uncertainty, and dealt with disagreement calmly. The outcome might be delaying a launch or choosing a different model. I would also say what I learned about making eval evidence persuasive: concrete examples land better than tables.

**Red-flag answers**

- Cannot give a specific case
- Presents it as personal victory
- Ignores the pushback

**Expect this follow-up:** How did you make sure the result was not just noise?

</details>

---

Prefer to practise with a write-first answer box? The same scenarios are in the [AI Evaluation Engineer interview simulator](https://aidevdayindia.org/interview-questions/ai-evaluation-engineer-interview-questions.html). Spotted a wrong or outdated answer? [Open a correction issue](https://github.com/ayushbishtdev/ai-engineering-interview-questions/issues/new?template=correction.md).
