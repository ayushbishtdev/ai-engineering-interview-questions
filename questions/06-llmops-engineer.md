# LLMOps Engineer: 30 interview questions with model answers

Thirty scenarios on deployment, monitoring, cost and latency control, reliability, self-hosting and incident response. Write your own answer first, then open the model answer to compare structure and reasoning.

Level mix: 2 Foundation, 19 Practitioner, 9 Advanced. Each question lists what the interviewer is testing, a model answer, red-flag answers to avoid, and the follow-up to expect.

## Contents

1. [How do you deploy and version LLM applications safely?](#q1) (Deployment, Practitioner)
2. [What do you monitor in production LLM systems?](#q2) (Monitoring, Practitioner)
3. [How do you control LLM costs at scale?](#q3) (Cost Control, Practitioner)
4. [How do you reduce latency for a chat application?](#q4) (Latency, Practitioner)
5. [How do you handle provider outages and rate limits?](#q5) (Reliability, Advanced)
6. [When would you self-host an open model instead of using an API?](#q6) (Self-hosting, Practitioner)
7. [Quality dropped and no code changed. What do you investigate?](#q7) (Quality Drift, Advanced)
8. [A prompt change caused a spike of bad outputs at 2am. How do you respond?](#q8) (Incident, Practitioner)
9. [Why use a prompt registry, and what should it support?](#q9) (Prompt Registry, Practitioner)
10. [What does CI/CD look like for an LLM application?](#q10) (CI/CD, Practitioner)
11. [What does a model gateway provide?](#q11) (Model Gateway, Practitioner)
12. [What should LLM tracing capture?](#q12) (Tracing, Practitioner)
13. [When is semantic caching a good idea?](#q13) (Semantic Caching, Advanced)
14. [How do you autoscale GPU inference?](#q14) (GPU Autoscaling, Advanced)
15. [How can you make self-hosted inference cheaper and faster?](#q15) (Inference Optimisation, Advanced)
16. [How do you isolate tenants in a shared LLM platform?](#q16) (Multi-tenancy, Advanced)
17. [How do you manage API keys and secrets for LLM services?](#q17) (Secrets, Foundation)
18. [How do you balance detailed logging with privacy?](#q18) (Logging & Privacy, Practitioner)
19. [How do you keep a RAG index fresh?](#q19) (Index Refresh, Practitioner)
20. [How do feature flags help with LLM releases?](#q20) (Feature Flags, Practitioner)
21. [How do you define SLOs for an LLM service?](#q21) (SLOs, Practitioner)
22. [How do you attribute LLM costs to teams and features?](#q22) (Cost Attribution, Practitioner)
23. [How do you manage fine-tuned models across their lifecycle?](#q23) (Model Registry, Advanced)
24. [What belongs in an on-call runbook for an LLM service?](#q24) (Runbooks, Foundation)
25. [How do you make staging environments realistic for LLM apps?](#q25) (Staging, Practitioner)
26. [How would you detect that an LLM application has started producing lower-quality answers before customers complain?](#q26) (Observability, Advanced)
27. [Your traffic doubles during a marketing campaign and you hit provider rate limits. What do you do in the moment and afterwards?](#q27) (Rate Limits, Practitioner)
28. [How do you roll out a new model version when you cannot fully predict how it will behave?](#q28) (Deployment, Practitioner)
29. [How do you handle user data that ends up in prompts, logs and traces in your LLM platform?](#q29) (Data Governance, Practitioner)
30. [Tell me about an outage or incident you handled on an ML or LLM system. What did you change afterwards?](#q30) (Behavioural, Advanced)

<a id="q1"></a>

### 1. How do you deploy and version LLM applications safely?

**Competency:** Deployment | **Level:** Practitioner

**What it tests:** Whether you version prompts, models and configs together.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I version prompts, model identifiers and configuration together as one release unit, stored in source control, and infrastructure is defined as code. Changes move through environments with eval gates, then reach production through a canary or shadow release with a small share of traffic. Rollback must be instant and tested, ideally a config switch, not a rebuild. Every release records which prompt, model and settings were live, so any behaviour can be traced to a version. Deploying straight to production is how silent quality regressions happen.

**Red-flag answers**

- Versions code but not prompts and models
- Deploys straight to production
- Has no rollback path

**Expect this follow-up:** How do you deploy a prompt change without redeploying the app?

</details>

<a id="q2"></a>

### 2. What do you monitor in production LLM systems?

**Competency:** Monitoring | **Level:** Practitioner

**What it tests:** Whether you monitor quality and cost, not just uptime.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I monitor the operational basics: latency percentiles, error rates, throughput, token usage and cost. On top of that I watch quality signals: a sampled evaluation of outputs, guardrail hits, refusal rates, user feedback and drift in the types of inputs arriving. Each has agreed thresholds and alerts that reach the right on-call person. Dashboards show trends by feature and model version. The gap in many teams is quality monitoring, since a service can be perfectly healthy technically while producing poor answers.

**Red-flag answers**

- Monitors uptime only
- Doesn't sample quality
- Sets alerts with no thresholds

**Expect this follow-up:** Everything is green but users complain. What is missing?

</details>

<a id="q3"></a>

### 3. How do you control LLM costs at scale?

**Competency:** Cost Control | **Level:** Practitioner

**What it tests:** Whether you control cost without cutting quality.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I attack cost from several angles. Caching removes repeated work, prompt trimming and history caps reduce tokens, routing sends easy requests to smaller models, and batching handles non-urgent work at lower prices. I set budgets and rate limits per team and feature, and track cost per successful task, since a cheap failing request is waste. Regular reviews of the top spenders find surprises early. Every optimisation is checked against the eval set so savings do not silently cost quality.

**Red-flag answers**

- Cuts quality to save cost
- Tracks no cost per task
- Sets no per-team budgets

**Expect this follow-up:** Which cost lever do you pull first, and why?

</details>

<a id="q4"></a>

### 4. How do you reduce latency for a chat application?

**Competency:** Latency | **Level:** Practitioner

**What it tests:** Whether you reduce latency with measured techniques.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I measure where time goes first, then act on the biggest part. Streaming makes responses feel faster, and prompt caching and shorter context cut processing time. I run independent steps, such as retrieval and classification, in parallel, use smaller or faster models for simple requests, and deploy close to users. Output length often dominates, so I constrain it. I set a latency budget for each step and track p95 and p99, because the slow tail is what users remember.

**Red-flag answers**

- Only switches to a smaller model
- Ignores streaming and caching
- Measures average latency

**Expect this follow-up:** p95 is bad but the average is fine. What do you check?

</details>

<a id="q5"></a>

### 5. How do you handle provider outages and rate limits?

**Competency:** Reliability | **Level:** Advanced

**What it tests:** Whether you design for provider outages and limits.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I design for failure from the start. Every call has timeouts and retries with exponential backoff and jitter, and circuit breakers stop hammering a failing provider. Behind a model abstraction I keep a fallback provider or model, and queue non-urgent work. When everything fails, the system degrades gracefully, for example by showing a cached answer or a non-AI path. I respect rate limits with client-side throttling, and I rehearse failover regularly, because untested failover tends not to work when needed.

**Red-flag answers**

- Uses a single provider with no fallback
- Retries with no backoff
- Never rehearses failover

**Expect this follow-up:** The fallback model behaves differently. How do you manage that?

</details>

<a id="q6"></a>

### 6. When would you self-host an open model instead of using an API?

**Competency:** Self-hosting | **Level:** Practitioner

**What it tests:** Whether you weigh self-hosting on total cost.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I consider self-hosting when data must stay within our control, when volume is high and steady enough to keep GPUs busy, when I need customisation such as fine-tuning, or when latency needs cannot be met by an API. I compare the full cost, including GPUs, engineering time, on-call, upgrades and idle capacity, against API pricing. At low or spiky volume, APIs are usually cheaper and simpler. I also weigh model quality, since the best hosted models may outperform open ones for my task.

**Red-flag answers**

- Assumes self-hosting is always cheaper
- Ignores GPU and on-call costs
- Has no volume estimate

**Expect this follow-up:** At what volume does self-hosting break even?

</details>

<a id="q7"></a>

### 7. Quality dropped and no code changed. What do you investigate?

**Competency:** Quality Drift | **Level:** Advanced

**What it tests:** Whether you diagnose drift when no code changed.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Since no code changed, I look outside our repository. The provider may have updated the model behind an alias, the mix of user inputs may have shifted, the retrieval index may be stale or a data pipeline may have broken. Seasonal or event-driven effects also matter. I compare current results with the eval set and traces from before the drop, segment by input type and time, and check provider change logs and index freshness. To prevent recurrence, I pin model versions and monitor quality continuously.

**Red-flag answers**

- Says nothing changed so it can't be us
- Ignores provider updates
- Has no eval set to compare against

**Expect this follow-up:** How would you confirm the provider changed the model?

</details>

<a id="q8"></a>

### 8. A prompt change caused a spike of bad outputs at 2am. How do you respond?

**Competency:** Incident | **Level:** Practitioner

**What it tests:** Whether you roll back first and learn afterwards.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

First I stop the harm: roll back to the last known good version, then confirm recovery in the metrics. I communicate status to stakeholders and keep a timeline. Once stable, I capture the failing examples, find the cause and add those examples to the eval suite so the release gate would catch them next time. I tighten the release process, for example with canary stages or required eval passes for prompt changes. The follow-up is a blameless review focused on how the system allowed the change through.

**Red-flag answers**

- Debugs live before rolling back
- Skips the blameless review
- Doesn't turn failures into tests

**Expect this follow-up:** What release gate would have caught this?

</details>

<a id="q9"></a>

### 9. Why use a prompt registry, and what should it support?

**Competency:** Prompt Registry | **Level:** Practitioner

**What it tests:** Whether prompts get ownership, versions and audit.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A prompt registry treats prompts as managed assets. It gives each prompt versions, owners, environments, diffs and linked eval results, and supports instant rollback. Where appropriate it decouples prompt changes from application releases, so a fix does not require a full deployment, while access controls, review and audit history keep this safe. It also helps non-engineers such as product or domain experts propose changes through a controlled process. Without it, prompts get edited in place and nobody knows what was running when.

**Red-flag answers**

- Keeps prompts scattered across code
- Has no owners or audit history
- Has no environment separation

**Expect this follow-up:** Who should be allowed to change a production prompt?

</details>

<a id="q10"></a>

### 10. What does CI/CD look like for an LLM application?

**Competency:** CI/CD | **Level:** Practitioner

**What it tests:** Whether evals gate releases in your pipeline.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

It looks like conventional CI/CD with an extra layer. Code goes through linting and unit tests, then the eval suite runs on prompt, model and retrieval changes, with safety checks. Deployment is staged, with canary monitoring of quality and cost, and automatic rollback if thresholds are breached. The evals play the role of tests, and they gate each release. Because LLM outputs vary, I use statistical thresholds and confidence intervals instead of exact matches, and I keep the pipeline fast enough that developers do not bypass it.

**Red-flag answers**

- Skips evals in the pipeline
- Tests only the code
- Has no automatic rollback

**Expect this follow-up:** What fails the build in your pipeline?

</details>

<a id="q11"></a>

### 11. What does a model gateway provide?

**Competency:** Model Gateway | **Level:** Practitioner

**What it tests:** Whether you centralise access, routing and policy.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A model gateway gives applications a single interface to multiple providers and models. It centralises authentication, rate limits, routing, retries, caching, logging, cost tracking and policy enforcement, so those features are not re-implemented in every service. It reduces lock-in because switching providers becomes a configuration change, and it gives security and finance a single point of visibility. The trade-off is another critical component to keep reliable and low-latency, so I treat it as production infrastructure with its own SLOs.

**Red-flag answers**

- Calls providers directly from each app
- Has no central logging
- Enforces no policy

**Expect this follow-up:** What would you put in the gateway first?

</details>

<a id="q12"></a>

### 12. What should LLM tracing capture?

**Competency:** Tracing | **Level:** Practitioner

**What it tests:** Whether traces make production bugs debuggable.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Each trace should capture the prompt and its version, the retrieved context, the model and parameters, tool calls and results, latency, token counts and cost, and any user feedback, all linked by a trace ID. This makes debugging possible, since I can reconstruct exactly what the model saw. It also lets me build evaluation sets from real production data and analyse cost by feature. I handle privacy through redaction and retention limits, and sample where volume is very high.

**Red-flag answers**

- Logs only final responses
- Uses no trace IDs
- Stores raw personal data

**Expect this follow-up:** How do you debug one bad conversation from production?

</details>

<a id="q13"></a>

### 13. When is semantic caching a good idea?

**Competency:** Semantic Caching | **Level:** Advanced

**What it tests:** Whether you cache safely and avoid wrong shared answers.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Semantic caching suits high-volume, repetitive questions where near-duplicates should get the same answer, such as FAQ-style support. I set the similarity threshold carefully and test it, because a threshold that is too loose returns wrong answers confidently. I avoid caching personalised, time-sensitive or sensitive responses, scope the cache by tenant and permissions, and expire entries. I measure the hit rate and the quality of cached answers to confirm the saving is worth the risk.

**Red-flag answers**

- Caches every response
- Sets loose similarity thresholds
- Caches personalised answers

**Expect this follow-up:** A cached answer is wrong for a different user. How did that happen?

</details>

<a id="q14"></a>

### 14. How do you autoscale GPU inference?

**Competency:** GPU Autoscaling | **Level:** Advanced

**What it tests:** Whether you scale GPUs on the right signals.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I scale on signals that reflect real load, such as queue depth, request latency and GPU utilisation, not just CPU. GPUs take minutes to start and models take time to load, so I keep some warm capacity and scale ahead of predictable peaks. Batching and mixed instance types improve utilisation, and I set cost ceilings to avoid runaway spend. I load-test with realistic prompt and output lengths to find true limits, since token counts vary widely and throughput depends on them.

**Red-flag answers**

- Scales on CPU only
- Ignores cold starts
- Sets no cost ceiling

**Expect this follow-up:** Traffic spikes at 9am daily. How do you handle cold starts?

</details>

<a id="q15"></a>

### 15. How can you make self-hosted inference cheaper and faster?

**Competency:** Inference Optimisation | **Level:** Advanced

**What it tests:** Whether you optimise inference while validating quality.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

The main levers are quantisation to reduce memory and speed up inference, continuous batching to raise throughput, KV-cache reuse for shared prefixes, and an optimised serving engine such as vLLM. I right-size hardware, and consider smaller or distilled models where quality allows. Speculative decoding can cut latency for some workloads. Each change is validated against the eval set, because optimisations can degrade quality in subtle ways. I measure cost per thousand tokens and latency, not just raw speed.

**Red-flag answers**

- Buys bigger GPUs first
- Doesn't validate quality after quantisation
- Ignores batching

**Expect this follow-up:** How do you check quality didn't drop after quantising?

</details>

<a id="q16"></a>

### 16. How do you isolate tenants in a shared LLM platform?

**Competency:** Multi-tenancy | **Level:** Advanced

**What it tests:** Whether tenants are isolated and that is tested.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I isolate tenants at every layer: separate data stores or indexes, or strict filtering enforced in the retrieval layer, per-tenant keys, quotas and rate limits, and separate logs. Caches must not be shared across tenants, and prompts must never include another tenant's data. I test isolation explicitly with cross-tenant probes, including prompt-injection attempts to extract other tenants' data. A noisy-neighbour problem is also possible, so fair-use limits protect performance for everyone.

**Red-flag answers**

- Shares indexes and caches across tenants
- Sets no per-tenant quotas
- Never tests isolation

**Expect this follow-up:** How do you prove one tenant can't see another's data?

</details>

<a id="q17"></a>

### 17. How do you manage API keys and secrets for LLM services?

**Competency:** Secrets | **Level:** Foundation

**What it tests:** Whether you handle keys and secrets safely.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

API keys live in a secrets manager, never in code, prompts or logs. They are scoped by service and environment, rotated regularly, and issued with the minimum permissions. I monitor usage for anomalies such as sudden spikes, which can indicate a leak, and set spending limits on keys. Developers get separate keys from production. Where possible I use short-lived credentials or workload identity, and have a tested procedure for revoking and replacing a compromised key quickly.

**Red-flag answers**

- Keeps keys in code or config files
- Never rotates them
- Puts secrets in prompts or logs

**Expect this follow-up:** A key leaks in a log. What do you do?

</details>

<a id="q18"></a>

### 18. How do you balance detailed logging with privacy?

**Competency:** Logging & Privacy | **Level:** Practitioner

**What it tests:** Whether you balance debuggability with privacy.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I log what is needed for debugging and evaluation, and no more. Sensitive fields are redacted or hashed at the point of logging, retention is short, and access is restricted and audited. A separate, consented or sanitised sample set can be kept for review and evals. Privacy requirements from legal and the data protection team decide what may be stored and for how long. The trade-off is real: less logging makes debugging harder, so I invest in good redaction rather than turning logs off.

**Red-flag answers**

- Logs everything forever
- Logs nothing to protect privacy
- Sets no access restrictions

**Expect this follow-up:** Debugging needs full prompts. How do you allow that safely?

</details>

<a id="q19"></a>

### 19. How do you keep a RAG index fresh?

**Competency:** Index Refresh | **Level:** Practitioner

**What it tests:** Whether you keep retrieval indexes fresh and clean.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I trigger incremental ingestion when sources change, and schedule periodic full checks for anything missed. Deleted or updated documents must be removed or re-embedded so stale answers disappear. I version indexes so I can roll back a bad refresh, and I monitor freshness, ingestion failures and index size. After each refresh I run a set of retrieval tests to confirm quality did not drop. Stale data is a quiet failure, so I alert on lag between the source and the index.

**Red-flag answers**

- Re-indexes everything manually
- Ignores deleted documents
- Doesn't monitor freshness

**Expect this follow-up:** A document is deleted at the source. How does it leave the index?

</details>

<a id="q20"></a>

### 20. How do feature flags help with LLM releases?

**Competency:** Feature Flags | **Level:** Practitioner

**What it tests:** Whether you decouple deployment from release.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Feature flags let me separate deployment from release. I can expose a new prompt or model to a small share of traffic or specific segments, compare metrics with the control, and switch it off instantly if something goes wrong without redeploying. They also support experiments and gradual rollout by tenant. I keep flags well managed, with owners and expiry dates, so they do not accumulate into untested combinations of settings.

**Red-flag answers**

- Releases to everyone at once
- Has no way to switch off instantly
- Ties release to deployment

**Expect this follow-up:** How would you run a 5% rollout of a new model?

</details>

<a id="q21"></a>

### 21. How do you define SLOs for an LLM service?

**Competency:** SLOs | **Level:** Practitioner

**What it tests:** Whether SLOs include quality, not only availability.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I define SLOs that reflect the user's experience: availability, latency percentiles, error rate and quality indicators from sampled evals. Each has an objective and an error budget that guides how much risk we can take with releases. Because quality is harder to measure than uptime, I make the quality SLO explicit and track it. I review SLOs after incidents and adjust them when they do not match what users care about. Alerts are based on budget burn, not on every blip.

**Red-flag answers**

- Sets availability targets only
- Adds no quality indicators
- Has no error budgets

**Expect this follow-up:** How do you turn a quality dip into an SLO breach?

</details>

<a id="q22"></a>

### 22. How do you attribute LLM costs to teams and features?

**Competency:** Cost Attribution | **Level:** Practitioner

**What it tests:** Whether costs are attributable by team and feature.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I tag every request with team, feature and environment through the gateway, then aggregate token and infrastructure costs in dashboards. Each team gets a budget with alerts, and anomalies are reviewed weekly. Shared costs, such as a common index or platform overhead, are allocated using a documented rule. Making cost visible changes behaviour: teams notice wasteful prompts when they can see the bill. I also report cost per successful outcome, so cheap-but-failing features do not look efficient.

**Red-flag answers**

- Tracks total spend only
- Uses no tags by team or feature
- Reviews costs annually

**Expect this follow-up:** One feature's cost spikes. How fast can you find it?

</details>

<a id="q23"></a>

### 23. How do you manage fine-tuned models across their lifecycle?

**Competency:** Model Registry | **Level:** Advanced

**What it tests:** Whether models trace back to data, code and evals.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I use a model registry that records each model's lineage: training data version, code, hyperparameters and evaluation results. Models move through stages, such as staging and production, with approvals and automatic checks, and I can reproduce any model from its record. Rollback to a previous version is straightforward. Every deployed model traces to its evidence, which supports audit and debugging. I also track dependencies on base models, so a base-model deprecation triggers a plan.

**Red-flag answers**

- Stores models with no lineage
- Cannot reproduce training
- Requires no approvals

**Expect this follow-up:** An auditor asks how model v3 was produced. What do you show?

</details>

<a id="q24"></a>

### 24. What belongs in an on-call runbook for an LLM service?

**Competency:** Runbooks | **Level:** Foundation

**What it tests:** Whether on-call runbooks are concrete and maintained.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

It lists the symptoms and the dashboards to check, how to confirm provider status, and step-by-step actions for rollback and failover. It covers known failure modes and their fixes, escalation contacts, and templates for communicating with users and stakeholders. It is written to be usable at 3am by someone who did not build the system. I update it after every incident and test it in game days, because an out-of-date runbook is worse than none.

**Red-flag answers**

- Writes runbooks with generic steps
- Leaves out rollback and failover steps
- Never updates them after incidents

**Expect this follow-up:** What is on the first page of your runbook?

</details>

<a id="q25"></a>

### 25. How do you make staging environments realistic for LLM apps?

**Competency:** Staging | **Level:** Practitioner

**What it tests:** Whether staging exposes real-world problems.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I make staging as close to production as practical: the same configuration, the same model versions, representative traffic patterns and real provider rate limits. Data is sanitised or synthetic but realistic in shape and difficulty. I run the eval suite there and load-test at expected volumes. Mocked model responses hide exactly the problems I need to find, such as latency, rate limiting and unexpected outputs, so I use real calls with cost controls. A staging environment that behaves differently gives false confidence.

**Red-flag answers**

- Uses mocked responses only
- Uses unrealistic traffic and data
- Skips real provider limits

**Expect this follow-up:** What issue only shows up in realistic staging?

</details>

<a id="q26"></a>

### 26. How would you detect that an LLM application has started producing lower-quality answers before customers complain?

**Competency:** Observability | **Level:** Advanced

**What it tests:** Whether you monitor quality proactively, not only uptime.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I combine several signals. An LLM judge or rule-based checks score a sample of live traffic against rubrics, and a small share is reviewed by humans to keep the judge honest. I watch proxy signals such as edit rates, retries, abandonment and thumbs-down, and I track drift in input topics, output length and refusal rates. Alerts fire on shifts beyond normal variation. Detection is only useful if flagged cases feed the eval set and an owner investigates.

**Red-flag answers**

- Monitors only uptime and latency
- Waits for customer complaints
- Uses a judge that was never validated

**Expect this follow-up:** The judge score is stable but complaints rise. What do you check?

</details>

<a id="q27"></a>

### 27. Your traffic doubles during a marketing campaign and you hit provider rate limits. What do you do in the moment and afterwards?

**Competency:** Rate Limits | **Level:** Practitioner

**What it tests:** Whether you can manage capacity and degrade gracefully under load.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

In the moment I shed or queue low-priority work, apply client-side throttling, turn on caching, route eligible traffic to a secondary provider or smaller model, and communicate status. Afterwards I ask what warning we missed: capacity was not requested in advance, there was no load test and there was no priority tiering. I request higher limits, set quotas per feature, add autoscaling queues and rehearse the scenario. Marketing should tell engineering about campaigns in advance.

**Red-flag answers**

- Only asks the provider for more quota
- Has no priority between traffic types
- Never load-tests the peak

**Expect this follow-up:** Which requests would you drop first, and how would you decide?

</details>

<a id="q28"></a>

### 28. How do you roll out a new model version when you cannot fully predict how it will behave?

**Competency:** Deployment | **Level:** Practitioner

**What it tests:** Whether you use staged exposure and comparison, not blind switches.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I run the eval suite first, including regression and safety tests, then shadow the new model on live traffic without showing its outputs so I can compare results, cost and latency. Next comes a canary at a few percent, watching quality, guardrail hits and user signals, and then a gradual ramp with flags for instant rollback. Prompts may need adjusting for behavioural differences. I keep the old model available until the new one has proven itself over a full traffic cycle.

**Red-flag answers**

- Switches all traffic at once
- Relies only on public benchmarks
- Removes the old model immediately

**Expect this follow-up:** The canary looks fine on average but worse for one customer. What now?

</details>

<a id="q29"></a>

### 29. How do you handle user data that ends up in prompts, logs and traces in your LLM platform?

**Competency:** Data Governance | **Level:** Practitioner

**What it tests:** Whether you treat observability data as sensitive data.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I classify what may appear in prompts and traces, then apply redaction at the point of capture, encryption, short retention and role-based access. Debug access is audited. Data that must be kept for evaluation is sampled, minimised and, where required, consented. I honour deletion requests across logs, caches and indexes. I make sure third-party observability tools are covered by the same data terms. Traces are enormously useful, but they are also a copy of user data that needs protecting.

**Red-flag answers**

- Logs full prompts forever
- Gives all engineers access to traces
- Forgets caches when handling deletion

**Expect this follow-up:** A user requests deletion. Where might their data still exist in your platform?

</details>

<a id="q30"></a>

### 30. Tell me about an outage or incident you handled on an ML or LLM system. What did you change afterwards?

**Competency:** Behavioural | **Level:** Advanced

**What it tests:** Whether you respond calmly and turn incidents into lasting improvements.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A strong answer gives a concrete incident with its impact and timeline: how it was detected, what I did to stabilise it and how I communicated. Then the root cause, often a combination of factors instead of one mistake, and the fixes: better alerts, release gates, runbooks or capacity planning. I would describe the blameless review and one specific change that measurably reduced the risk of a repeat. I would be honest about what I would do differently.

**Red-flag answers**

- Blames one person
- Cannot describe any lasting change
- Focuses only on the heroics

**Expect this follow-up:** How did you know your fix worked?

</details>

---

Prefer to practise with a write-first answer box? The same scenarios are in the [LLMOps Engineer interview simulator](https://aidevdayindia.org/interview-questions/llmops-engineer-interview-questions.html). Spotted a wrong or outdated answer? [Open a correction issue](https://github.com/ayushbishtdev/ai-engineering-interview-questions/issues/new?template=correction.md).
