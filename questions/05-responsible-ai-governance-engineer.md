# Responsible AI / AI Governance Engineer: 30 interview questions with model answers

Thirty scenarios on risk assessment, regulation, bias testing, transparency, privacy and incident response. Write your own answer first, then open the model answer to compare structure and reasoning.

Level mix: 3 Foundation, 14 Practitioner, 13 Advanced. Each question lists what the interviewer is testing, a model answer, red-flag answers to avoid, and the follow-up to expect.

## Contents

1. [How do you assess the risk of a new AI use case?](#q1) (Risk Assessment, Practitioner)
2. [How do you keep systems aligned with rules like the EU AI Act and India's DPDP Act?](#q2) (Regulation, Advanced)
3. [How do you test an AI system for bias?](#q3) (Bias Testing, Practitioner)
4. [What documentation should accompany a deployed model?](#q4) (Transparency, Foundation)
5. [How do you prevent sensitive data leaking through an LLM application?](#q5) (Privacy, Advanced)
6. [How do you design meaningful human oversight?](#q6) (Human Oversight, Advanced)
7. [An AI system produced a harmful output publicly. What is your response?](#q7) (Incident Response, Advanced)
8. [The business wants to launch despite unresolved fairness findings. What do you do?](#q8) (Pressure, Advanced)
9. [Why keep an inventory of AI systems, and what goes in it?](#q9) (AI Inventory, Foundation)
10. [How do you run an AI impact assessment?](#q10) (Impact Assessment, Practitioner)
11. [How do you approach explainability for different audiences?](#q11) (Explainability, Practitioner)
12. [Fairness metrics can conflict. How do you choose?](#q12) (Fairness Trade-offs, Advanced)
13. [How do you assess data provenance, consent and copyright for training or retrieval?](#q13) (Data Provenance, Advanced)
14. [What do you check before adopting a third-party model or AI vendor?](#q14) (Vendor Due Diligence, Practitioner)
15. [How do you design safety testing before launch?](#q15) (Safety Testing, Practitioner)
16. [How do you turn a responsible-AI policy into guardrails engineers can use?](#q16) (Policy Guardrails, Practitioner)
17. [What should be logged to support AI audits?](#q17) (Audit Trail, Practitioner)
18. [How do you set up an AI governance operating model?](#q18) (Governance Model, Practitioner)
19. [How do you embed governance into the delivery pipeline?](#q19) (Controls in CI, Practitioner)
20. [How would you write a generative-AI acceptable-use policy for employees?](#q20) (Acceptable Use, Foundation)
21. [Employees are using unapproved AI tools. How do you respond?](#q21) (Shadow AI, Practitioner)
22. [What extra safeguards are needed when users may be children or vulnerable?](#q22) (Vulnerable Users, Advanced)
23. [How do you monitor fairness and safety after launch?](#q23) (Post-launch Monitoring, Practitioner)
24. [How do you handle a data deletion request when data may be in a model?](#q24) (Erasure Requests, Advanced)
25. [How do you manage differing regulations across countries?](#q25) (Cross-border, Advanced)
26. [What are the main governance risks specific to generative AI compared with traditional ML?](#q26) (Generative AI Risk, Practitioner)
27. [How does governance change when an AI system can take actions, not only produce text?](#q27) (Agentic AI, Advanced)
28. [A team says documentation slows them down. How do you keep it useful and lightweight?](#q28) (Documentation, Practitioner)
29. [A provider updates its model and outputs change for your regulated use case. How do you govern that?](#q29) (Third-party Models, Advanced)
30. [Tell me about a time you had to say no to a launch or slow one down for governance reasons. How did you handle it?](#q30) (Behavioural, Advanced)

<a id="q1"></a>

### 1. How do you assess the risk of a new AI use case?

**Competency:** Risk Assessment | **Level:** Practitioner

**What it tests:** Whether you tier AI use cases by impact and autonomy.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I classify each use case by its impact on people, the level of autonomy the system has, the sensitivity of the data and whether its effects can be reversed. A meeting summariser is low risk; a tool that screens job candidates affects livelihoods and sits in a high-risk tier. Higher tiers get stronger controls: human oversight, deeper testing, fuller documentation and formal approval gates. I revisit the classification when scope, data or model changes. The goal is proportionate governance, so low-risk work moves quickly and high-risk work gets real scrutiny.

**Red-flag answers**

- Treats all use cases the same
- Ignores reversibility and autonomy
- Applies no tiered controls

**Expect this follow-up:** Classify a résumé-screening tool and an internal meeting summariser, and explain your reasoning.

</details>

<a id="q2"></a>

### 2. How do you keep systems aligned with rules like the EU AI Act and India's DPDP Act?

**Competency:** Regulation | **Level:** Advanced

**What it tests:** Whether compliance is built into the pipeline.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I map each use case to the relevant risk categories under rules like the EU AI Act and India's Digital Personal Data Protection Act, and keep an inventory with the documentation each category needs. Then I build requirements into the design: consent and purpose limits, data minimisation, logging, transparency and rights handling. I work with legal on interpretation and on changes as guidance evolves. Compliance lives in the delivery pipeline and system design, not in a review at the end, because retrofitting controls is slower and costlier.

**Red-flag answers**

- Says compliance is legal's job
- Adds it at the end
- Keeps no inventory or documentation

**Expect this follow-up:** A new regulation lands. How do you find which systems are affected?

</details>

<a id="q3"></a>

### 3. How do you test an AI system for bias?

**Competency:** Bias Testing | **Level:** Practitioner

**What it tests:** Whether you test fairness by group, not overall.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start by defining which groups matter for the use case and which fairness metrics fit the harm at stake. Then I evaluate performance and error rates by group on representative data, including intersections where the sample size allows. When I find gaps, I investigate the cause, which may be data coverage, labels or thresholds, and apply mitigations, then re-test. I document the trade-offs and residual risk, and I repeat the testing after launch because populations and data drift over time.

**Red-flag answers**

- Tests only overall accuracy
- Doesn't define groups or metrics
- Doesn't re-test after mitigation

**Expect this follow-up:** You find a 6-point gap for one group. What next?

</details>

<a id="q4"></a>

### 4. What documentation should accompany a deployed model?

**Competency:** Transparency | **Level:** Foundation

**What it tests:** Whether documentation covers limits and prohibited uses.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

At minimum a model card covering purpose, training and evaluation data summary, performance by segment, known limitations, intended and prohibited uses, and named owners. For the deployed application I add a system card describing how the model is used with retrieval, tools, guardrails and human oversight, since risk comes from the whole system. Documentation should be versioned, kept up to date, and written for readers such as auditors, product teams and affected users, not just engineers.

**Red-flag answers**

- Says a README is enough
- Lists no limitations or prohibited uses
- Gives no evaluation by segment

**Expect this follow-up:** Who reads the model card, and what do they need from it?

</details>

<a id="q5"></a>

### 5. How do you prevent sensitive data leaking through an LLM application?

**Competency:** Privacy | **Level:** Advanced

**What it tests:** Whether you prevent leakage across the whole data path.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I minimise and redact sensitive data before it reaches the model, and enforce access controls at retrieval so users only get documents they are allowed to see. I avoid training on customer data without consent, filter outputs for sensitive patterns, set retention limits and log access. I also test for leakage directly, for example by probing for memorised or cross-user data. Providers are chosen on their data terms. Privacy needs to be an architectural property, because a prompt telling the model to keep secrets is not a control.

**Red-flag answers**

- Relies on the provider's promises
- Ignores access control at retrieval
- Keeps logs indefinitely

**Expect this follow-up:** How do you test for leakage before launch?

</details>

<a id="q6"></a>

### 6. How do you design meaningful human oversight?

**Competency:** Human Oversight | **Level:** Advanced

**What it tests:** Whether oversight can actually change outcomes.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Meaningful oversight means the reviewer has the context, the authority and the time to change the outcome. I design review screens that show the evidence and the model's reasoning, not just a verdict, and I make it easy to reject or edit. I measure override rates and review time to spot rubber-stamping, and rotate or sample to keep attention high. There are clear escalation paths for hard cases. Oversight that cannot change outcomes, or that people are too busy to exercise, is a checkbox, not a safeguard.

**Red-flag answers**

- Adds a human reviewer as a checkbox
- Doesn't measure override rates
- Gives reviewers no time or authority

**Expect this follow-up:** Reviewers approve 99% of outputs. Is oversight working?

</details>

<a id="q7"></a>

### 7. An AI system produced a harmful output publicly. What is your response?

**Competency:** Incident Response | **Level:** Advanced

**What it tests:** Whether you respond openly and fix governance gaps.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I contain it first: disable or restrict the feature, and preserve logs and evidence. Then I find the root cause, whether a model behaviour, a prompt change, retrieved content or a missing guardrail. I communicate openly and promptly with affected people, leadership and regulators where required, without speculation. I fix the cause, add tests so it cannot recur, and run a blameless review that includes governance gaps such as missing approvals or weak monitoring. Speed, honesty and learning matter more than defending the system.

**Red-flag answers**

- Denies or delays
- Skips logs and root cause
- Does no governance review

**Expect this follow-up:** Who do you tell first, and what do you say?

</details>

<a id="q8"></a>

### 8. The business wants to launch despite unresolved fairness findings. What do you do?

**Competency:** Pressure | **Level:** Advanced

**What it tests:** Whether you hold the line on unresolved fairness risk.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I escalate with evidence, not opinion: the findings, the legal and reputational exposure, and the affected groups. I propose practical alternatives, such as a limited release, human review of affected decisions or a fix-by-date commitment. If the business still chooses to proceed, I make sure the risk acceptance is documented and signed by someone with the authority to accept it. For critical harms, such as illegal discrimination, I hold the line and do not sign off. My role is to make the risk visible and owned.

**Red-flag answers**

- Complies quietly
- Refuses without alternatives
- Doesn't document risk acceptance

**Expect this follow-up:** Leadership signs off on the risk. What do you still do?

</details>

<a id="q9"></a>

### 9. Why keep an inventory of AI systems, and what goes in it?

**Competency:** AI Inventory | **Level:** Foundation

**What it tests:** Whether you know why visibility comes first.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

You cannot govern what you cannot see. The inventory lists every AI system with its purpose, owner, model and data sources, risk tier, affected users, controls, approvals and review dates. It supports audits, incident response and regulatory reporting, and it exposes shadow AI that teams adopted without review. To keep it alive, I link it to procurement and deployment workflows so entries are created as part of normal work, and I review it on a schedule.

**Red-flag answers**

- Keeps a spreadsheet nobody updates
- Assigns no owner or risk tier
- Cannot find shadow AI

**Expect this follow-up:** How would you discover AI systems that aren't in the inventory?

</details>

<a id="q10"></a>

### 10. How do you run an AI impact assessment?

**Competency:** Impact Assessment | **Level:** Practitioner

**What it tests:** Whether assessments identify harms per group and get revisited.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I describe the use case, the stakeholders and the data, then identify benefits and harms for each affected group, including people who are not users. I rate likelihood and severity, define mitigations with owners and deadlines, and record residual risk for sign-off. The assessment involves legal, security, product and, where possible, representatives of those affected. It is a living document: I revisit it when the model, data or scope changes, and after incidents.

**Red-flag answers**

- Fills in a form once
- Ignores affected groups
- Never revisits after changes

**Expect this follow-up:** What triggers a reassessment?

</details>

<a id="q11"></a>

### 11. How do you approach explainability for different audiences?

**Competency:** Explainability | **Level:** Practitioner

**What it tests:** Whether explanations fit the audience and are faithful.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I match the explanation to the audience and the risk. Users need plain-language reasons and sources they can check. Auditors need traceable logic, data lineage and decision records. Engineers need technical detail such as feature importance or retrieval traces. I test that explanations are faithful to what the system actually did, since a plausible but invented rationale can mislead. For high-stakes decisions I prefer inherently more interpretable designs, or a human decision supported by evidence.

**Red-flag answers**

- Gives one explanation for all audiences
- Confuses plausible with faithful
- Ignores audit needs

**Expect this follow-up:** How do you check an explanation is faithful?

</details>

<a id="q12"></a>

### 12. Fairness metrics can conflict. How do you choose?

**Competency:** Fairness Trade-offs | **Level:** Advanced

**What it tests:** Whether you choose fairness metrics with context.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Common fairness metrics, such as equal error rates and equal selection rates, can be mathematically incompatible, so I cannot satisfy all of them. I begin with the harm we are trying to prevent and the legal context, then choose the metrics that match. I quantify the trade-offs with accuracy and other business metrics, involve legal, product and affected-group perspectives, and record the decision and its reasoning. The choice is a value judgement, so it needs to be made openly by accountable people and revisited as circumstances change.

**Red-flag answers**

- Picks a metric without context
- Ignores the legal context
- Doesn't quantify trade-offs

**Expect this follow-up:** Two fairness metrics can't both be met. Which do you choose, and why?

</details>

<a id="q13"></a>

### 13. How do you assess data provenance, consent and copyright for training or retrieval?

**Competency:** Data Provenance | **Level:** Advanced

**What it tests:** Whether you check licence, consent and lineage.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I trace where training and retrieval data came from, check the licence terms and the consent basis, and record lineage so I can answer questions later. Restricted, unlicensed or improperly collected content is excluded or removed. For third-party data I require contractual assurances about rights and provenance, and I ask legal to review high-risk sources. I also plan for takedown: if a source must be removed, I need to know where it has been used, in indexes, fine-tuning sets and caches.

**Red-flag answers**

- Ignores licences and consent
- Keeps no lineage records
- Trusts third-party data blindly

**Expect this follow-up:** A source's licence is unclear. What do you do?

</details>

<a id="q14"></a>

### 14. What do you check before adopting a third-party model or AI vendor?

**Competency:** Vendor Due Diligence | **Level:** Practitioner

**What it tests:** Whether you check vendors beyond marketing.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I check how the vendor handles and retains our data and whether they train on it, their security certifications and testing, model and system documentation, evaluation evidence and known limitations. I look at sub-processors, incident history and regional processing. In the contract I look at liability, audit rights, service levels and exit terms, including data return and deletion. I test the vendor's claims on our own data. Vendor risk is our risk, so due diligence has to be evidence-based, not a questionnaire someone else filled in.

**Red-flag answers**

- Relies on the vendor's marketing
- Ignores training on customer data
- Leaves out exit terms

**Expect this follow-up:** The vendor won't share evaluation evidence. Do you proceed?

</details>

<a id="q15"></a>

### 15. How do you design safety testing before launch?

**Competency:** Safety Testing | **Level:** Practitioner

**What it tests:** Whether pre-launch testing has thresholds and sign-off.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I define harm categories relevant to the product, build test sets and red-team scenarios, and set pass thresholds according to the risk tier. Tests cover misuse, jailbreaks, sensitive topics, and failures for particular groups and languages. After mitigations I test again to confirm they work without excessive over-refusal. Residual risk is documented and needs formal sign-off from the owner before release. I keep the tests in the pipeline, since changes to prompts, models or tools can reintroduce old problems.

**Red-flag answers**

- Tests only common cases
- Sets no pass thresholds by risk tier
- Requires no sign-off on residual risk

**Expect this follow-up:** The test fails one critical category. Who can approve a launch?

</details>

<a id="q16"></a>

### 16. How do you turn a responsible-AI policy into guardrails engineers can use?

**Competency:** Policy Guardrails | **Level:** Practitioner

**What it tests:** Whether policy becomes usable engineering controls.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I translate principles such as fairness or privacy into concrete controls engineers can adopt without a legal degree: content filters, PII detection, approval gates, logging and evaluation checks. I package them as shared libraries, templates and pipeline steps, with examples and defaults that make the compliant path the easy path. I run short workshops and office hours. A policy PDF changes little; a control that is built into the tooling changes behaviour, and produces evidence for audits at the same time.

**Red-flag answers**

- Publishes a policy PDF only
- Adds no code or pipeline checks
- Offers principles with no concrete controls

**Expect this follow-up:** Turn 'be fair' into three checks an engineer can run.

</details>

<a id="q17"></a>

### 17. What should be logged to support AI audits?

**Competency:** Audit Trail | **Level:** Practitioner

**What it tests:** Whether logs support audits without over-collecting.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I log the model and prompt versions, inputs and outputs where permitted, retrieved sources, decisions taken, human reviews and overrides, and access records. Logs need to be tamper-resistant and retained for the period required, but they must also respect privacy: I redact or hash sensitive fields and restrict access. I design the schema with auditors in mind so a decision can be reconstructed months later. The tension between traceability and privacy is resolved by being deliberate about what is stored and why.

**Red-flag answers**

- Logs everything including personal data
- Logs too little to audit
- Lets logs be edited

**Expect this follow-up:** How do you keep logs useful without over-collecting?

</details>

<a id="q18"></a>

### 18. How do you set up an AI governance operating model?

**Competency:** Governance Model | **Level:** Practitioner

**What it tests:** Whether governance is tiered and lightweight.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I set up a lightweight council of legal, security, privacy, product and engineering, with clear decision rights. Reviews are tiered by risk: low-risk use cases follow a checklist and proceed quickly, while high-risk ones get deeper assessment and formal approval. Each tier has owners, turnaround times and templates so teams know what to expect. I track metrics such as review time and issues found. Governance that is too slow gets bypassed, and governance that is too light misses real risks.

**Red-flag answers**

- Builds a slow committee
- Applies the same review to all risks
- Sets no owners or SLAs

**Expect this follow-up:** Low-risk teams say governance slows them down. What do you change?

</details>

<a id="q19"></a>

### 19. How do you embed governance into the delivery pipeline?

**Competency:** Controls in CI | **Level:** Practitioner

**What it tests:** Whether governance evidence is automated.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I automate the checks that can be automated: documentation present, evaluation thresholds met, bias tests passed, secrets and PII scans clean, and approved model and vendor lists respected. Higher-risk changes hit an approval gate that requires a human sign-off with a recorded decision. The pipeline generates evidence automatically, which reduces manual audit preparation and makes compliance visible to teams. I keep the checks fast and the failures clear, so developers see them as help rather than obstruction.

**Red-flag answers**

- Reviews every release manually
- Generates no automated evidence
- Ties approvals to nothing about risk

**Expect this follow-up:** Which check would you automate first?

</details>

<a id="q20"></a>

### 20. How would you write a generative-AI acceptable-use policy for employees?

**Competency:** Acceptable Use | **Level:** Foundation

**What it tests:** Whether policy is short, practical and paired with training.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I keep it short and practical. It states which tools and use cases are approved, what data must never be entered, such as customer personal data or confidential source code, and how outputs must be reviewed before use. It covers disclosure to customers, intellectual property, and the consequences of breaches. I pair it with training and real examples, plus a simple route to request new tools. A policy nobody reads or can follow will be ignored, so usability matters.

**Red-flag answers**

- Writes a long legal policy
- Doesn't say what data must never be entered
- Offers no training

**Expect this follow-up:** An employee pastes customer data into a public tool. What now?

</details>

<a id="q21"></a>

### 21. Employees are using unapproved AI tools. How do you respond?

**Competency:** Shadow AI | **Level:** Practitioner

**What it tests:** Whether you address the need behind unapproved tools.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start by understanding why people use unapproved tools, which is usually an unmet need or slow approved options. Then I offer approved alternatives that are actually good, publish clear guidance, and make requests for new tools quick. I use discovery methods such as network and expense data to see the scale of use, and communicate what is at risk without blaming. Blocking without alternatives only pushes usage underground, where I cannot help people use it safely.

**Red-flag answers**

- Bans tools and hopes
- Punishes users
- Doesn't ask why they use them

**Expect this follow-up:** What approved alternative would you offer first?

</details>

<a id="q22"></a>

### 22. What extra safeguards are needed when users may be children or vulnerable?

**Competency:** Vulnerable Users | **Level:** Advanced

**What it tests:** Whether you add safeguards for children and vulnerable users.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I apply stricter content limits, age-appropriate design and tone, and limit the data collected. There are clear escalation paths to humans, especially for signs of distress, and I involve child-safety or clinical experts in design and testing. I test with scenarios specific to these users and language. I review the legal duties that apply, such as age-appropriate design codes and parental consent rules. For these users the default should be caution, and features are enabled only when I can show they are safe.

**Red-flag answers**

- Treats every user the same
- Ignores legal duties
- Skips expert testing

**Expect this follow-up:** How does your escalation path change for a distressed user?

</details>

<a id="q23"></a>

### 23. How do you monitor fairness and safety after launch?

**Competency:** Post-launch Monitoring | **Level:** Practitioner

**What it tests:** Whether monitoring continues by group after launch.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I track quality and error rates by group, harmful-output incidents, user complaints and drift in inputs and outputs, with agreed thresholds and alerts. Sampled outputs are reviewed by people on a regular schedule, and results are reported to the governance forum. When metrics cross a threshold, it triggers investigation, retesting or rollback. I also watch for new use patterns that were not in the original impact assessment. Launch testing is a snapshot, but risk moves as users and data change.

**Red-flag answers**

- Stops monitoring after launch
- Tracks overall metrics only
- Sets no thresholds or rollback triggers

**Expect this follow-up:** What metric shift would make you roll back?

</details>

<a id="q24"></a>

### 24. How do you handle a data deletion request when data may be in a model?

**Competency:** Erasure Requests | **Level:** Advanced

**What it tests:** Whether you handle deletion when data is in a model.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I delete the data from source systems, indexes, caches, backups within policy and logs. Then I assess whether it was used for training. If so, the options depend on the case: retraining, unlearning techniques where they are credible, or suppressing outputs, and I am honest with legal about their limitations. The best approach is prevention, by avoiding training on personal data and using retrieval so deletion is straightforward. I keep records of how each request was handled.

**Red-flag answers**

- Says deleting a row is enough
- Ignores logs and indexes
- Doesn't assess training use

**Expect this follow-up:** The data was used for fine-tuning. What are your options?

</details>

<a id="q25"></a>

### 25. How do you manage differing regulations across countries?

**Competency:** Cross-border | **Level:** Advanced

**What it tests:** Whether you manage differing regulations systematically.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I set a baseline on the strictest common requirements where practical, and map local differences in a control matrix that shows which rules apply to which systems and regions. Where laws conflict, I use regional configurations, such as data residency, feature restrictions or different consent flows. I work with local counsel and track regulatory changes through a named owner. The aim is a manageable core design with controlled variations, not a separate system for every country.

**Red-flag answers**

- Follows one country's rules only
- Builds no control matrix
- Doesn't track regulatory change

**Expect this follow-up:** How do you design for a country with stricter rules than your baseline?

</details>

<a id="q26"></a>

### 26. What are the main governance risks specific to generative AI compared with traditional ML?

**Competency:** Generative AI Risk | **Level:** Practitioner

**What it tests:** Whether you understand what is different about open-ended generative systems.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Generative systems produce open-ended output, so risks include hallucination, harmful or biased content, leakage of sensitive data, prompt injection, copyright exposure and misuse. Unlike a classifier, the range of outputs cannot be fully enumerated, so testing is statistical and never complete. Users also over-trust fluent answers. Governance therefore adds output monitoring, red-teaming, disclosure, content and data controls, and clear human accountability for decisions made with model help. Many controls that suit traditional ML, such as fixed test sets alone, are not enough.

**Red-flag answers**

- Treats it as identical to traditional ML
- Believes testing can prove absence of harm
- Ignores over-trust by users

**Expect this follow-up:** Which of these risks would you prioritise for an internal HR chatbot?

</details>

<a id="q27"></a>

### 27. How does governance change when an AI system can take actions, not only produce text?

**Competency:** Agentic AI | **Level:** Advanced

**What it tests:** Whether you recognise the shift in risk from content to consequences.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

When a system can act, errors have consequences, not just wrong words: money moves, records change and messages are sent. I extend governance to permissions and autonomy: least-privilege access, defined action limits, human approval for high-impact or irreversible steps, full audit logs and the ability to stop the system instantly. Accountability must be clear, with a named owner for what the agent may do. Testing includes adversarial scenarios and failure of tools, and monitoring watches actions, not just outputs.

**Red-flag answers**

- Applies only content-safety controls
- Leaves accountability unassigned
- Grants broad standing permissions

**Expect this follow-up:** Who is accountable when an agent takes a harmful action within its permissions?

</details>

<a id="q28"></a>

### 28. A team says documentation slows them down. How do you keep it useful and lightweight?

**Competency:** Documentation | **Level:** Practitioner

**What it tests:** Whether you make governance efficient and valuable to engineers.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I find out what part is painful and remove waste. I generate as much as possible automatically from pipelines and registries, such as model versions, evaluation results and data sources. Templates ask only for what reviewers actually need, scaled to the risk tier, so low-risk work has a page and high-risk work has more. I show teams how the documents help them, for example onboarding and incident response. If nobody ever reads a document, it should be cut.

**Red-flag answers**

- Demands the same documents for every project
- Ignores the team's actual pain
- Keeps documents nobody reads

**Expect this follow-up:** Which documents would you require for a low-risk internal tool?

</details>

<a id="q29"></a>

### 29. A provider updates its model and outputs change for your regulated use case. How do you govern that?

**Competency:** Third-party Models | **Level:** Advanced

**What it tests:** Whether you manage change in dependencies you do not control.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I pin model versions where possible and track provider change notices. Any update triggers re-running the evaluation suite, including fairness and safety tests, before it reaches production, with a canary rollout and rollback path. The change is recorded in the inventory and, if material, in the risk assessment. Contracts should give notice periods for changes. If the provider will not give enough stability for a regulated use, I limit the use case or choose a different provider.

**Red-flag answers**

- Accepts silent updates
- Re-tests only accuracy
- Has no rollback path

**Expect this follow-up:** The provider gives only a week's notice of deprecation. What do you do?

</details>

<a id="q30"></a>

### 30. Tell me about a time you had to say no to a launch or slow one down for governance reasons. How did you handle it?

**Competency:** Behavioural | **Level:** Advanced

**What it tests:** Whether you can hold a line constructively and keep relationships intact.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A strong answer describes a specific case and the evidence behind my concern. I explain how I framed it as risk to the business, not obstruction, and offered options such as a limited release or extra safeguards. I would say who I involved, how I documented the decision and how I kept the relationship working. The outcome might be a delay with a plan. I would also reflect on what I learned about engaging early so reviews do not feel like surprises.

**Red-flag answers**

- Presents governance as a veto for its own sake
- Offers no alternatives
- Cannot name a real example

**Expect this follow-up:** What would you do if a senior leader overruled you?

</details>

---

Prefer to practise with a write-first answer box? The same scenarios are in the [Responsible AI / AI Governance Engineer interview simulator](https://aidevdayindia.org/interview-questions/responsible-ai-governance-engineer-interview-questions.html). Spotted a wrong or outdated answer? [Open a correction issue](https://github.com/ayushbishtdev/ai-engineering-interview-questions/issues/new?template=correction.md).
