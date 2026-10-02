# AI Solutions Architect: 30 interview questions with model answers

Thirty scenarios on enterprise GenAI architecture, build vs buy, security, multi-model design, scale and stakeholder trade-offs. Write your own answer first, then open the model answer to compare structure and reasoning.

Level mix: 4 Foundation, 17 Practitioner, 9 Advanced. Each question lists what the interviewer is testing, a model answer, red-flag answers to avoid, and the follow-up to expect.

## Contents

1. [How do you design an enterprise architecture for generative AI?](#q1) (Architecture, Practitioner)
2. [How do you decide between build, buy and partner for AI capabilities?](#q2) (Build vs Buy, Practitioner)
3. [How do you advise a client choosing between RAG and fine-tuning?](#q3) (RAG vs Fine-tuning, Foundation)
4. [What are the key security risks in LLM architectures?](#q4) (Security, Advanced)
5. [How do you design for multiple models and vendors?](#q5) (Multi-model, Practitioner)
6. [How do you plan for scale and cost in an AI platform?](#q6) (Scale & Cost, Practitioner)
7. [How do you explain trade-offs to non-technical executives?](#q7) (Stakeholders, Foundation)
8. [A bank wants AI on top of legacy systems under strict compliance. What is your approach?](#q8) (Legacy, Advanced)
9. [What does a production RAG reference architecture include?](#q9) (RAG Reference, Practitioner)
10. [How do you prepare enterprise data for AI use?](#q10) (Data Architecture, Practitioner)
11. [How do you choose between cloud AI services, private cloud and on-premises?](#q11) (Hosting Choices, Practitioner)
12. [How do you design for tight latency requirements?](#q12) (Latency Design, Practitioner)
13. [How do you add AI features to a multi-tenant SaaS product?](#q13) (Multi-tenant SaaS, Advanced)
14. [How do you make an AI system resilient?](#q14) (Resilience, Advanced)
15. [Which integration patterns work well for AI in enterprise systems?](#q15) (Integration Patterns, Practitioner)
16. [What architectural concerns are specific to enterprise agents?](#q16) (Enterprise Agents, Advanced)
17. [How do you estimate total cost of ownership for an AI solution?](#q17) (TCO, Practitioner)
18. [What typically breaks between a PoC and production?](#q18) (PoC to Production, Practitioner)
19. [How do you run a fair vendor evaluation?](#q19) (Vendor Selection, Practitioner)
20. [How should identity and access work in an AI architecture?](#q20) (Identity & Access, Advanced)
21. [How do you migrate an application to a new model safely?](#q21) (Model Migration, Practitioner)
22. [A vendor promises big accuracy gains. How do you validate the claim?](#q22) (Vendor Claims, Foundation)
23. [When does on-device or edge AI make sense?](#q23) (Edge AI, Practitioner)
24. [What kinds of technical debt are unique to AI systems?](#q24) (AI Tech Debt, Practitioner)
25. [How do you choose between a workflow and an agentic architecture for a client?](#q25) (Workflow vs Agent, Practitioner)
26. [How do you design an AI platform so that individual teams can build quickly while central risk requirements are still met?](#q26) (Governance, Advanced)
27. [A client wants to use customer conversations to improve their AI assistant. How do you advise them?](#q27) (Data Privacy, Advanced)
28. [How do you build evaluation into the architecture, not treat it as a later testing phase?](#q28) (Evaluation, Practitioner)
29. [A client asks you to choose their first generative AI use case. How do you decide?](#q29) (Generative AI Strategy, Foundation)
30. [Tell me about an architecture decision you got wrong. What happened and what did you learn?](#q30) (Behavioural, Advanced)

<a id="q1"></a>

### 1. How do you design an enterprise architecture for generative AI?

**Competency:** Architecture | **Level:** Practitioner

**What it tests:** Whether your design layers security, cost and swap-ability.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I build it in layers: data and retrieval, a model gateway, orchestration, guardrails, observability, and identity and access running through all of them. Each layer has a clear owner and interface, so components can change independently. I design for security, cost control and the ability to swap models, because the model market moves quickly. For a pilot I would build the thinnest slice that proves value, with evaluation and logging in from day one, then harden the layers as usage grows.

**Red-flag answers**

- Draws boxes with no security or cost
- Locks into one model
- Assigns no ownership per layer

**Expect this follow-up:** Which layer would you build first for a pilot, and why?

</details>

<a id="q2"></a>

### 2. How do you decide between build, buy and partner for AI capabilities?

**Competency:** Build vs Buy | **Level:** Practitioner

**What it tests:** Whether you decide on differentiation, lock-in and skills.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I buy commodity capabilities, such as generic chat or transcription, build where our data, workflow or user experience creates a real advantage, and partner when speed or specialist skills matter. I compare total cost of ownership, lock-in, security and compliance, and the skills the team really has. Decisions are revisited as the market moves, since something worth building last year may now be a product. I try to make choices reversible by keeping clean interfaces around bought components.

**Red-flag answers**

- Builds everything, or buys everything
- Ignores lock-in and skills
- Never revisits the decision

**Expect this follow-up:** The vendor's price doubles after year one. What is your exit?

</details>

<a id="q3"></a>

### 3. How do you advise a client choosing between RAG and fine-tuning?

**Competency:** RAG vs Fine-tuning | **Level:** Foundation

**What it tests:** Whether you advise on evidence, starting simple.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I explain that they solve different problems. RAG suits knowledge that changes or is proprietary, and it gives citations and easy updates. Fine-tuning suits consistent style, format or behaviour, or making a smaller model perform a narrow task. Usually I recommend starting with good prompting and RAG, measuring with an eval set, and fine-tuning only where the evals show a gap that remains. They can also be combined. The client should leave knowing what evidence would change my recommendation.

**Red-flag answers**

- Says fine-tuning is always better
- Ignores citations and freshness
- Doesn't start with prompting

**Expect this follow-up:** The client insists on fine-tuning. How do you respond?

</details>

<a id="q4"></a>

### 4. What are the key security risks in LLM architectures?

**Competency:** Security | **Level:** Advanced

**What it tests:** Whether you know LLM-specific threats beyond hallucination.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

The main risks are prompt injection, data leakage, agents with excessive permissions, insecure tool calls, supply-chain risk from models and packages, and poisoned or untrusted data. Controls include isolating untrusted content, least-privilege access, propagating user identity, validating tool arguments, input and output filtering, sandboxing, dependency scanning and monitoring. I run threat modelling early and adversarial tests before release. No single control is enough, so I layer defences and assume that some will fail.

**Red-flag answers**

- Mentions only hallucinations
- Ignores agent permissions
- Has no supply-chain thinking

**Expect this follow-up:** Which single control gives the most protection for the least effort?

</details>

<a id="q5"></a>

### 5. How do you design for multiple models and vendors?

**Competency:** Multi-model | **Level:** Practitioner

**What it tests:** Whether you design a gateway that limits lock-in.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I put a gateway in front of the models with a common interface, so applications do not depend on a single vendor. It handles routing rules, central logging, policy enforcement and cost tracking. I choose models per task using my own evals, for example a small fast model for classification and a stronger one for complex reasoning, and switch based on evidence. This reduces lock-in, improves cost and resilience, but adds a component to operate, so it needs its own reliability targets.

**Red-flag answers**

- Integrates each vendor directly
- Has no central logging or policy
- Ignores eval-driven switching

**Expect this follow-up:** How do you switch a model without breaking the application?

</details>

<a id="q6"></a>

### 6. How do you plan for scale and cost in an AI platform?

**Competency:** Scale & Cost | **Level:** Practitioner

**What it tests:** Whether you model tokens, quotas and unit costs.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start with expected users, request volumes and token counts per request, then model the peak and growth scenarios. I choose caching, batching and routing to control cost, set quotas per tenant or team, and plan GPU capacity if self-hosting. Unit economics matter: cost per user or per task must stay below the value produced, or growth loses money. I present the numbers with sensitivity to usage and price changes, and I build monitoring so real costs are compared with the plan.

**Red-flag answers**

- Ignores token volumes
- Sets no quotas
- Estimates cost per call only

**Expect this follow-up:** Usage grows 5x in six months. What breaks first?

</details>

<a id="q7"></a>

### 7. How do you explain trade-offs to non-technical executives?

**Competency:** Stakeholders | **Level:** Foundation

**What it tests:** Whether you explain trade-offs in business terms.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I frame options in the terms executives use: value, cost, risk and time. I give a clear recommendation, explain what happens under each choice, and avoid jargon. An analogy or a small live demo often communicates faster than a diagram. I am honest about uncertainty and say what would change my advice. I keep it to what they must decide. Executives trust architects who make the trade-offs plain, not those who hide them in detail.

**Red-flag answers**

- Uses jargon with executives
- Presents options with no recommendation
- Hides uncertainty

**Expect this follow-up:** The CFO asks 'why can't it be 100% accurate?' What do you say?

</details>

<a id="q8"></a>

### 8. A bank wants AI on top of legacy systems under strict compliance. What is your approach?

**Competency:** Legacy | **Level:** Advanced

**What it tests:** Whether you propose safe, incremental AI in regulated settings.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I begin with a low-risk, high-value use case, such as internal document search, not a customer-facing decision. Legacy data is exposed through secure APIs, not copied around, and it stays in approved regions. I add audit logging, access controls and human review for anything consequential, then pilot before scaling. Compliance, risk and security join from day one, so their requirements shape the design and approval does not surprise the project at the end. Trust is built one controlled step at a time.

**Red-flag answers**

- Proposes a big-bang rebuild
- Ignores compliance and audit
- Moves data outside approved regions

**Expect this follow-up:** Which use case would you start with at the bank, and why?

</details>

<a id="q9"></a>

### 9. What does a production RAG reference architecture include?

**Competency:** RAG Reference | **Level:** Practitioner

**What it tests:** Whether you know every layer of production RAG.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

It includes ingestion and parsing of source documents, chunking and embedding, a vector or hybrid index, retrieval with reranking, prompt assembly, generation, and guardrails on input and output. Access control is enforced at retrieval time so users only see permitted content. Around it sit evaluation, monitoring and tracing, and a pipeline for keeping the index fresh. I also include feedback capture. The reference architecture is a starting point that I adapt to the data, users and risk of the client.

**Red-flag answers**

- Lists only a vector database and an LLM
- Leaves out evaluation and monitoring
- Ignores access control at retrieval

**Expect this follow-up:** A user retrieves a document they shouldn't see. Where did the design fail?

</details>

<a id="q10"></a>

### 10. How do you prepare enterprise data for AI use?

**Competency:** Data Architecture | **Level:** Practitioner

**What it tests:** Whether you treat data governance as the real bottleneck.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I begin by cataloguing sources and identifying owners, then assess quality and fix the biggest problems. Access controls and lineage are applied so that AI systems respect existing permissions. I standardise formats where it matters, and build pipelines that keep the data fresh and detect breakage. Poor data governance is usually the real bottleneck, not the model, so I set expectations early that data work is a major part of the project and often needs its own budget.

**Red-flag answers**

- Says data is the client's problem
- Ignores ownership, quality and lineage
- Has no plan for freshness

**Expect this follow-up:** Data is scattered across ten systems. Where do you start?

</details>

<a id="q11"></a>

### 11. How do you choose between cloud AI services, private cloud and on-premises?

**Competency:** Hosting Choices | **Level:** Practitioner

**What it tests:** Whether hosting choices follow sensitivity, regulation and skills.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I weigh data sensitivity, regulation, latency, cost, available skills and which models each option offers. Managed cloud services are fastest to adopt and often give access to the strongest models. Private cloud or on-premises gives more control but requires capacity, skills and operations. Many clients end up hybrid: managed services for most workloads and private hosting for the most sensitive ones. I make the decision workload by workload, with a clear rationale the client's risk team can review.

**Red-flag answers**

- Always recommends public cloud
- Ignores regulation and skills
- Offers no hybrid option

**Expect this follow-up:** Which workloads would you keep private, and why?

</details>

<a id="q12"></a>

### 12. How do you design for tight latency requirements?

**Competency:** Latency Design | **Level:** Practitioner

**What it tests:** Whether you budget latency per step and measure p95.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I set a latency budget for the whole interaction and allocate it to each step. Then I reduce the biggest contributors: smaller or distilled models, streaming, prompt caching, parallel retrieval, fewer hops, and deployment close to users. I check whether every step is truly needed. I measure p95 and p99 under realistic load, not on a quiet demo system. If the requirement cannot be met with an LLM in the path, I discuss alternatives such as precomputed answers or a non-AI fast path.

**Red-flag answers**

- Only picks a faster model
- Sets no per-step latency budget
- Measures average, not p95

**Expect this follow-up:** Latency is 6s and the target is 2s. Where do you cut first?

</details>

<a id="q13"></a>

### 13. How do you add AI features to a multi-tenant SaaS product?

**Competency:** Multi-tenant SaaS | **Level:** Advanced

**What it tests:** Whether tenant isolation holds at every layer.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I isolate tenant data at every layer, from storage and indexes to caches and logs, and enforce that isolation in code and tests. Quotas and fair-use limits protect against noisy neighbours, and cost is metered per tenant so pricing reflects usage. Tenants may need configuration options such as models, data residency or content settings. I make sure prompts, memory and caches can never carry one tenant's data into another's request, and I test that with adversarial probes.

**Red-flag answers**

- Shares prompts and caches across tenants
- Has no per-tenant metering
- Ignores fair use

**Expect this follow-up:** How would you test that tenant data never leaks?

</details>

<a id="q14"></a>

### 14. How do you make an AI system resilient?

**Competency:** Resilience | **Level:** Advanced

**What it tests:** Whether the system degrades gracefully when providers fail.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I define recovery objectives first, then design to meet them. Techniques include multi-region or multi-provider fallbacks, timeouts, retries with backoff, circuit breakers, queues for asynchronous work, and graceful degradation to a non-AI path. Dependencies such as the vector store and the gateway are covered as well as the model. I test failover regularly through game days. A resilience plan that has never been exercised is a hope, not a design.

**Red-flag answers**

- Uses a single provider and region
- Has no fallback or graceful degradation
- Never tests failover

**Expect this follow-up:** The provider is down for an hour. What do users see?

</details>

<a id="q15"></a>

### 15. Which integration patterns work well for AI in enterprise systems?

**Competency:** Integration Patterns | **Level:** Practitioner

**What it tests:** Whether you choose loose, appropriate integration patterns.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

For synchronous requests I expose AI services through APIs. For long or bursty work I use events and queues, with webhooks for callbacks. Adapters wrap legacy systems so the AI service does not depend on their quirks. I keep the AI components loosely coupled behind stable contracts so models, prompts and vendors can change without rewriting the integrations. I also think about idempotency and error handling, since AI calls are slower and less predictable than typical service calls.

**Red-flag answers**

- Tightly couples AI to the core system
- Uses synchronous calls for everything
- Ignores adapters for legacy systems

**Expect this follow-up:** When would you use events instead of an API call?

</details>

<a id="q16"></a>

### 16. What architectural concerns are specific to enterprise agents?

**Competency:** Enterprise Agents | **Level:** Advanced

**What it tests:** Whether governance is designed into agent architecture.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

The concerns are identity and delegated permissions, so the agent acts with a specific user's rights and no more; a registry of approved tools; approval flows for high-impact actions; audit logs; cost and step limits; state management for long tasks; and observability to reconstruct decisions. Governance and security must be designed in from the start, because retrofitting them onto an agent that already has broad access is much harder. I also plan how agents will be tested and rolled back.

**Red-flag answers**

- Treats agents like chatbots
- Ignores identity and delegated permissions
- Has no audit logs or cost limits

**Expect this follow-up:** How do you stop an agent acting beyond the user's permissions?

</details>

<a id="q17"></a>

### 17. How do you estimate total cost of ownership for an AI solution?

**Competency:** TCO | **Level:** Practitioner

**What it tests:** Whether you count all costs, not just the model.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I include model and infrastructure costs, data preparation and pipelines, integration effort, evaluation, monitoring, security and compliance work, and the staffing needed to run and improve the solution. Then I model growth scenarios and show sensitivity to usage and to model price changes, which can move quickly. I distinguish one-off from recurring costs. Comparing the TCO with the expected value, and showing the assumptions, allows the client to challenge the numbers and trust the conclusion.

**Red-flag answers**

- Counts only model costs
- Ignores data, integration and support
- Shows no sensitivity to usage

**Expect this follow-up:** Which cost line do clients usually underestimate?

</details>

<a id="q18"></a>

### 18. What typically breaks between a PoC and production?

**Competency:** PoC to Production | **Level:** Practitioner

**What it tests:** Whether you plan production readiness from the PoC.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Data is messier than the demo data, edge cases multiply, latency and cost look different at scale, security reviews surface new requirements, integrations take longer than planned, and there are no evals or monitoring to tell whether it works. Ownership and support are often undefined too. I plan a production-readiness checklist at the start of the PoC and include an estimate of the remaining work in the PoC results, so the sponsor sees the true path to production.

**Red-flag answers**

- Says the PoC just needs scaling
- Ignores evals and monitoring
- Discovers security reviews late

**Expect this follow-up:** What would be on your production-readiness checklist?

</details>

<a id="q19"></a>

### 19. How do you run a fair vendor evaluation?

**Competency:** Vendor Selection | **Level:** Practitioner

**What it tests:** Whether you run fair, evidence-based vendor evaluation.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I define requirements and weighted criteria up front, agreed with stakeholders, so the outcome does not depend on the loudest voice. Candidates are tested on our data using a shared eval set, and I review security posture, data terms and contract conditions. I check references and total cost, and score everyone transparently against the same criteria. I keep the process documented so it can be defended, and I ask about exit terms, since leaving a vendor is part of choosing one.

**Red-flag answers**

- Chooses on demos or price
- Uses no shared eval set
- Skips contract and security review

**Expect this follow-up:** Two vendors score equally. How do you decide?

</details>

<a id="q20"></a>

### 20. How should identity and access work in an AI architecture?

**Competency:** Identity & Access | **Level:** Advanced

**What it tests:** Whether the model never gets more access than the user.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

The user's identity should be propagated end to end so every layer knows who is asking. Permissions are enforced at retrieval and at tool level, based on that identity, so the model can only reach what the user is allowed to. Services use least-privilege credentials, and access is logged. The model never gets more access than the user has. A common failure is a service account with broad access behind a chatbot, which lets any user see everything.

**Red-flag answers**

- Gives the model service-level access
- Doesn't propagate user identity
- Enforces permissions only in the UI

**Expect this follow-up:** How do you enforce document-level permissions in RAG?

</details>

<a id="q21"></a>

### 21. How do you migrate an application to a new model safely?

**Competency:** Model Migration | **Level:** Practitioner

**What it tests:** Whether you migrate models safely with evals and rollback.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I run the evaluation suite on the new model and compare quality, cost and latency. Prompts are adapted for behavioural differences, then I use shadow traffic or a canary to test on real requests. I monitor closely during the ramp and keep rollback ready. I plan for differences in style, refusals and format, and I inform stakeholders in case the changes are visible. Starting early turns a forced migration into a routine one.

**Red-flag answers**

- Swaps the model with no evals
- Ignores behavioural differences
- Has no rollback

**Expect this follow-up:** How would you shadow-test a new model?

</details>

<a id="q22"></a>

### 22. A vendor promises big accuracy gains. How do you validate the claim?

**Competency:** Vendor Claims | **Level:** Foundation

**What it tests:** Whether you validate claims on your own data.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I ask for a trial on our own data and metrics, not the vendor's demo set. I look for benchmark mismatch and cherry-picking, ask about failure modes and where the system does poorly, and validate cost and latency under realistic load. I check whether results hold across our segments. I ask for references from similar customers. If the vendor resists a fair test, that is important information. The claim is a hypothesis until it is proven on my data.

**Red-flag answers**

- Accepts vendor benchmarks
- Runs no trial on client data
- Ignores failure modes and load

**Expect this follow-up:** The vendor won't allow a trial on your data. What do you do?

</details>

<a id="q23"></a>

### 23. When does on-device or edge AI make sense?

**Competency:** Edge AI | **Level:** Practitioner

**What it tests:** Whether you know when on-device AI genuinely fits.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Edge or on-device AI makes sense for privacy, offline use, very low latency or limited bandwidth. The trade-offs are smaller models, tight device constraints on memory and power, and harder updates and monitoring. I test quality on the actual target hardware, not only on servers, and plan how models will be updated and how failures will be observed. Often a hybrid works: simple tasks on the device and complex ones in the cloud.

**Red-flag answers**

- Says edge AI is always cheaper
- Ignores device constraints
- Doesn't test on target hardware

**Expect this follow-up:** How do you update models on devices in the field?

</details>

<a id="q24"></a>

### 24. What kinds of technical debt are unique to AI systems?

**Competency:** AI Tech Debt | **Level:** Practitioner

**What it tests:** Whether you recognise debt unique to AI systems.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

AI systems accumulate debt in ways that are easy to miss: prompts changed without version control, dependencies on specific model versions, stale data pipelines, missing evals, glue code around unreliable components and hidden feedback loops where the system's outputs influence its future inputs. I address it with versioning, tests, clear ownership and scheduled reviews. Because models change underneath us, debt grows even when nobody touches the code. I also track which items are actually slowing delivery and pay those down first.

**Red-flag answers**

- Says AI has no unique debt
- Leaves prompts and models untracked
- Has no evals or ownership

**Expect this follow-up:** Which debt would hurt you most a year from now?

</details>

<a id="q25"></a>

### 25. How do you choose between a workflow and an agentic architecture for a client?

**Competency:** Workflow vs Agent | **Level:** Practitioner

**What it tests:** Whether you start deterministic and justify autonomy.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start with the most deterministic design that meets the need. Workflows suit predictable processes: they are cheaper, faster and easier to test and audit. Agents fit open-ended tasks where the path varies. I justify added autonomy with evals showing it improves outcomes, and with a risk analysis covering what could go wrong and how it is contained. Many good designs are workflows with a small agentic step. I explain this to clients in terms of control, cost and risk.

**Red-flag answers**

- Recommends agents by default
- Doesn't justify autonomy with evals
- Ignores risk analysis

**Expect this follow-up:** The client wants an agent for a fixed process. How do you respond?

</details>

<a id="q26"></a>

### 26. How do you design an AI platform so that individual teams can build quickly while central risk requirements are still met?

**Competency:** Governance | **Level:** Advanced

**What it tests:** Whether you balance autonomy with control through platform design.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I provide a paved road: a shared platform with approved models behind a gateway, built-in guardrails, logging, evaluation templates and identity, so teams get compliance by default. Central policy is expressed as automated checks in the pipeline and tiered reviews by risk, so low-risk work needs almost no ceremony. Teams can step off the paved road, but with extra review. I measure adoption and time-to-launch, because a platform teams avoid has failed.

**Red-flag answers**

- Requires manual approval for everything
- Builds a platform teams find slow
- Leaves each team to solve security alone

**Expect this follow-up:** A team wants a model outside the approved list. How do you decide?

</details>

<a id="q27"></a>

### 27. A client wants to use customer conversations to improve their AI assistant. How do you advise them?

**Competency:** Data Privacy | **Level:** Advanced

**What it tests:** Whether you weigh value against consent, privacy and risk.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I clarify the legal basis and consent: what customers were told and agreed to. I recommend minimising and anonymising the data, excluding sensitive categories, and setting retention limits. I would compare options such as improving prompts and retrieval from insights, versus training on raw data, which has a higher risk. I involve legal and the data protection officer, and provide opt-out. Often the value can be gained from aggregated analysis, without training on personal conversations.

**Red-flag answers**

- Uses all data because it is available
- Ignores consent and retention
- Skips legal review

**Expect this follow-up:** A customer asks for their conversations to be removed from the training set. What must the architecture support?

</details>

<a id="q28"></a>

### 28. How do you build evaluation into the architecture, not treat it as a later testing phase?

**Competency:** Evaluation | **Level:** Practitioner

**What it tests:** Whether you design for measurement from day one.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I treat evaluation as a first-class component. The architecture captures traces with the information needed to replay and score requests, stores versioned eval datasets, and runs the suite in the delivery pipeline as a release gate. Production sampling feeds a review workflow and adds new cases. Metrics are exposed on dashboards alongside cost and latency. Designing for it early is far cheaper than retrofitting, and without it the client cannot tell whether changes are improvements.

**Red-flag answers**

- Leaves testing until the end
- Stores no traces to replay
- Has no route from production failures to the eval set

**Expect this follow-up:** What would you cut if the budget were halved, and what would you keep?

</details>

<a id="q29"></a>

### 29. A client asks you to choose their first generative AI use case. How do you decide?

**Competency:** Generative AI Strategy | **Level:** Foundation

**What it tests:** Whether you select for value, feasibility and risk, not novelty.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I list candidate use cases and score them on business value, feasibility (data availability, technical difficulty), risk and time to a measurable result. I favour a use case with a clear owner, accessible data and users who will adopt it, where mistakes are tolerable and reviewable. Internal knowledge search or drafting support are common starting points. I define success metrics and a scope small enough to complete in weeks, and I use the result to build credibility for larger work.

**Red-flag answers**

- Picks the most impressive demo
- Chooses a high-risk customer-facing case first
- Defines no success metric

**Expect this follow-up:** The CEO wants the most ambitious use case first. How do you respond?

</details>

<a id="q30"></a>

### 30. Tell me about an architecture decision you got wrong. What happened and what did you learn?

**Competency:** Behavioural | **Level:** Advanced

**What it tests:** Whether you show honest reflection and improved judgement.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A strong answer names a real decision, such as locking into one vendor or under-investing in evaluation, and says what led to it: time pressure, missing information or overconfidence. I would describe the consequences, how I recognised the problem and what we did to correct it. Then the lesson and how it changed my practice, for example writing down the assumptions behind decisions and defining review triggers. I would take responsibility without excuses.

**Red-flag answers**

- Claims never to have been wrong
- Blames the client or the team
- Cannot say what changed in their practice

**Expect this follow-up:** How do you now decide which decisions are easy to reverse and which are not?

</details>

---

Prefer to practise with a write-first answer box? The same scenarios are in the [AI Solutions Architect interview simulator](https://aidevdayindia.org/interview-questions/ai-solutions-architect-interview-questions.html). Spotted a wrong or outdated answer? [Open a correction issue](https://github.com/ayushbishtdev/ai-engineering-interview-questions/issues/new?template=correction.md).
