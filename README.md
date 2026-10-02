# AI Engineering Interview Questions: 210 Scenarios Across 7 Roles

A set of 210 scenario-based interview questions for AI engineering roles: AI Engineer, Agentic AI Engineer, AI Evaluation Engineer, Forward Deployed Engineer, Responsible AI / AI Governance Engineer, LLMOps Engineer and AI Solutions Architect. Every question comes with what the interviewer is testing, a model answer, the red-flag answers that lose points, and the follow-up to expect. It is written for engineers preparing for these roles, mostly at Practitioner level (118 of 210), with 27 Foundation and 65 Advanced questions. Last updated: October 2026. Reviewed quarterly; numbers, regulations and tool names that change get fixed through issues and pull requests.

## What's in this repo

- [`questions/`](questions/): all 210 questions as Markdown, one file per role, with collapsible model answers so you can write first and reveal later
- [`data/ai-engineering-interview-questions.csv`](data/ai-engineering-interview-questions.csv): the same 210 questions as one flat file for spreadsheets, flashcards and scripts (columns in [`data/README.md`](data/README.md))
- [`CHEATSHEET.md`](CHEATSHEET.md): one-page role map, the Foundation starter list, recurring themes and the behavioural question for each role
- [`CHECKLIST.md`](CHECKLIST.md): every red-flag answer and follow-up as tick boxes, for mock-interview self-checks
- Role summaries below, each with one full worked sample question

## Roles at a glance

| Role | Questions | Foundation | Practitioner | Advanced | Full question set |
|---|---|---|---|---|---|
| AI Engineer (Prompt & Context Engineering) | 30 | 6 | 18 | 6 | [questions/01-ai-engineer.md](questions/01-ai-engineer.md) |
| Agentic AI Engineer | 30 | 3 | 16 | 11 | [questions/02-agentic-ai-engineer.md](questions/02-agentic-ai-engineer.md) |
| AI Evaluation Engineer | 30 | 4 | 16 | 10 | [questions/03-ai-evaluation-engineer.md](questions/03-ai-evaluation-engineer.md) |
| Forward Deployed Engineer | 30 | 5 | 18 | 7 | [questions/04-forward-deployed-engineer.md](questions/04-forward-deployed-engineer.md) |
| Responsible AI / AI Governance Engineer | 30 | 3 | 14 | 13 | [questions/05-responsible-ai-governance-engineer.md](questions/05-responsible-ai-governance-engineer.md) |
| LLMOps Engineer | 30 | 2 | 19 | 9 | [questions/06-llmops-engineer.md](questions/06-llmops-engineer.md) |
| AI Solutions Architect | 30 | 4 | 17 | 9 | [questions/07-ai-solutions-architect.md](questions/07-ai-solutions-architect.md) |
| **Total** | **210** | **27** | **118** | **65** | |

## How to use this

Write your own answer first, aloud or typed, before opening the model answer. Compare the structure of your reasoning with the model answer rather than copying its wording, then rehearse the listed follow-up, since that second question is where most candidates come apart. The same questions are available as an [interactive AI engineering interview simulator](https://aidevdayindia.org/interview-questions/ai-interview-prep.html) if you prefer a write-first answer box over Markdown.

## AI Engineer (Prompt & Context Engineering)

Covers the day-to-day work of building LLM features: prompt structure and versioning, context engineering, RAG debugging, hallucination control, structured output, model selection, cost, latency, caching, prompt injection and PII handling. Strong answers share one habit: change one thing at a time, gate it behind a fixed eval set, and measure instead of assuming (track a hallucination rate rather than trusting a stricter prompt). Most questions are Practitioner level, and the set includes handling Indian languages and preparing for a provider deprecating your model. The set has 30 questions: 6 Foundation, 18 Practitioner and 6 Advanced.

**Competencies covered:** Prompt Engineering, Context Engineering, RAG, Hallucinations, Structured Output, Model Selection, Long Context, Cost, Few-shot Prompting, Prompt Injection, Chunking, Embeddings, Hybrid Search, Function Calling, Prompt Evaluation, Caching, Fine-tuning, Multilingual, Streaming UX, Determinism, PII Handling, Conversation Memory, Ambiguous Requirements, Debugging, Model Deprecation, Latency, Retrieval, Evaluation Data, plus one behavioural question.

**Sample scenario (Practitioner): How do you reduce hallucinations in a customer-facing assistant?**

<details>
<summary>Model answer, red flags and follow-up</summary>

I ground answers in retrieved sources and require citations, so every claim can be checked. I explicitly allow 'I don't know' and reward it in evals, because a model that must always answer will invent. I constrain output format, add a verification step for high-risk claims, and route low-confidence or high-stakes cases to a human. Then I measure: a labelled eval set gives me a hallucination rate I can track across releases. A stricter prompt helps a little, but only measurement tells me whether the assistant is actually safer.

**Red-flag answers:** Says a stricter prompt solves it; Never allows 'I don't know'; Tracks no hallucination rate on an eval set.

**Expect this follow-up:** How do you decide when to route to a human?

</details>

All 30 questions with answers: [questions/01-ai-engineer.md](questions/01-ai-engineer.md)

**Full breakdown:** [AI Engineer (Prompt & Context Engineering) interview simulator with all 30 scenarios and a write-first answer box](https://aidevdayindia.org/interview-questions/ai-engineer-interview-questions.html)

## Agentic AI Engineer

Covers when to use an agent instead of a fixed workflow, tool design, MCP, guardrails, memory, loops, multi-agent systems, planning, human approval, tool-output injection, agent evals, cost control, resumability and code sandboxing. The recurring answer is to start with the simplest design that works and add autonomy only where it pays off, measured by task success against cost and latency. This is one of the more Advanced-heavy sets, with safety and delegated-access scenarios throughout. The set has 30 questions: 3 Foundation, 16 Practitioner and 11 Advanced.

**Competencies covered:** Agent Design, Tool Design, MCP, Guardrails, Memory, Failure Loops, Multi-agent, Observability, Planning, Human Approval, Tool Injection, Agent Evals, Cost Control, State & Resume, Tool Errors, Frameworks, Long Tasks, Delegated Access, Code Sandbox, Context Growth, A2A, Reliability Metrics, Non-determinism, Clarification, Rollout, Prompt Design, Evaluation, Security, Trade-offs, plus one behavioural question.

**Sample scenario (Practitioner): When should you use an agent instead of a fixed workflow?**

<details>
<summary>Model answer, red flags and follow-up</summary>

I use an agent when the steps cannot be known in advance and the task needs dynamic tool choices, such as investigating an unfamiliar bug. If the path is predictable, a fixed workflow with model calls at specific steps is cheaper, faster and far easier to test and audit. I start with the simplest design that works and add autonomy only where it clearly pays off, measured by task success against cost and latency. Many good systems are workflows with one small agentic step inside, which keeps most of the behaviour predictable.

**Red-flag answers:** Says agents are always better than workflows; Cannot explain when a fixed workflow is cheaper and easier to test; Adds autonomy everywhere from day one.

**Expect this follow-up:** Give a task where you would deliberately choose a workflow over an agent.

</details>

All 30 questions with answers: [questions/02-agentic-ai-engineer.md](questions/02-agentic-ai-engineer.md)

**Full breakdown:** [Agentic AI Engineer interview simulator with all 30 scenarios and a write-first answer box](https://aidevdayindia.org/interview-questions/agentic-ai-engineer-interview-questions.html)

## AI Evaluation Engineer

Covers building eval sets, LLM-as-judge risks, metric choice, regression testing, human annotation, offline versus online evaluation, safety and bias evals, benchmark contamination, synthetic data, RAG and agent evals, statistical rigour, red teaming and A/B testing. The consistent principle is that no benchmark, vendor claim or judge model is trusted until it has been checked against your own task and human labels. It also covers reporting results to executives and building an eval-driven team culture. The set has 30 questions: 4 Foundation, 16 Practitioner and 10 Advanced.

**Competencies covered:** Eval Design, LLM-as-Judge, Metrics, Regression, Human Review, Online vs Offline, Safety Evals, Benchmarks, Golden Datasets, Synthetic Data, RAG Evals, Agent Evals, Statistical Rigour, Scoring Methods, Rubric Design, Eval Cost, Contamination, Multilingual Evals, No Ground Truth, Error Analysis, Reporting, Red Teaming, Calibration, A/B Testing, Eval Culture, Judge Design, Production Monitoring, Eval Data, Tooling, plus one behavioural question.

**Sample scenario (Foundation): A vendor claims state-of-the-art benchmark scores. Do you trust them?**

<details>
<summary>Model answer, red flags and follow-up</summary>

Not on their own. Public benchmarks can be contaminated by training data, saturate quickly, and often measure something different from my task. A vendor's number also comes from their prompts and settings, not mine. I run the candidate model on my own eval set with my prompts, and compare quality alongside cost, latency, context limits and data terms. The benchmark can help build a shortlist, but the decision rests on evidence from my data. If the vendor will not let me test, that is itself informative.

**Red-flag answers:** Accepts the claim as fact; Ignores contamination; Doesn't test cost and latency.

**Expect this follow-up:** The model wins on the vendor's benchmark and loses on yours. What do you report?

</details>

All 30 questions with answers: [questions/03-ai-evaluation-engineer.md](questions/03-ai-evaluation-engineer.md)

**Full breakdown:** [AI Evaluation Engineer interview simulator with all 30 scenarios and a write-first answer box](https://aidevdayindia.org/interview-questions/ai-evaluation-engineer-interview-questions.html)

## Forward Deployed Engineer

Covers scoping vague customer requests, messy and legacy data, building trust, security reviews, taking a demo to production, scope creep, sponsor changes, adoption, handover, showing ROI, failed pilots, working with sales and data residency. The role is defined by customer outcomes: judgement about what to build, what to skip and what to tell the customer honestly, plus feeding learnings back into the product. Most questions are situations rather than definitions, so answers are judged on how you reason with the customer in the room. The set has 30 questions: 5 Foundation, 18 Practitioner and 7 Advanced.

**Competencies covered:** Role, Scoping, Messy Data, Trust, Product Feedback, Security Review, Production, Scope Creep, Discovery, Demos, Sponsor Change, Adoption, Legacy Integration, Accuracy Expectations, Handover, Value Story, Failed Pilot, Prioritisation, Working with Sales, Stakeholder Conflict, Internal Escalation, Training, Data Residency, Prototype Debt, Bad News, Technical Judgement, Communication, Delivery, Security, plus one behavioural question.

**Sample scenario (Foundation): What does a forward deployed engineer do that a regular engineer doesn't?**

<details>
<summary>Model answer, red flags and follow-up</summary>

A forward deployed engineer works inside the customer's environment to turn messy, real needs into working solutions quickly. That means scoping problems with the people who live with them, integrating with the customer's systems, deploying, supporting adoption and feeding what they learn back to the product team. Customer outcomes matter as much as code quality, and much of the job is judgement about what to build, what to skip and what to tell the customer honestly. A regular engineer usually works from a defined spec; an FDE often has to help create it.

**Red-flag answers:** Describes it as regular engineering with travel; Ignores customer outcomes; Doesn't mention feeding learnings back to product.

**Expect this follow-up:** Give an example of a customer learning that changed a product.

</details>

All 30 questions with answers: [questions/04-forward-deployed-engineer.md](questions/04-forward-deployed-engineer.md)

**Full breakdown:** [Forward Deployed Engineer interview simulator with all 30 scenarios and a write-first answer box](https://aidevdayindia.org/interview-questions/forward-deployed-engineer-interview-questions.html)

## Responsible AI / AI Governance Engineer

Covers risk and impact assessment, alignment with rules such as the EU AI Act and India's DPDP Act, bias testing, conflicting fairness metrics, documentation, human oversight, incident response, vendor due diligence, audit logging, shadow AI, vulnerable users, erasure requests, cross-border regulation and agentic systems. Strong answers turn policy into controls engineers can actually use, such as checks in the delivery pipeline and logs that support audits. Thirteen of the 30 are Advanced, including questions about pushing back on a launch. The set has 30 questions: 3 Foundation, 14 Practitioner and 13 Advanced.

**Competencies covered:** Risk Assessment, Regulation, Bias Testing, Transparency, Privacy, Human Oversight, Incident Response, Pressure, AI Inventory, Impact Assessment, Explainability, Fairness Trade-offs, Data Provenance, Vendor Due Diligence, Safety Testing, Policy Guardrails, Audit Trail, Governance Model, Controls in CI, Acceptable Use, Shadow AI, Vulnerable Users, Post-launch Monitoring, Erasure Requests, Cross-border, Generative AI Risk, Agentic AI, Documentation, Third-party Models, plus one behavioural question.

**Sample scenario (Foundation): What documentation should accompany a deployed model?**

<details>
<summary>Model answer, red flags and follow-up</summary>

At minimum a model card covering purpose, training and evaluation data summary, performance by segment, known limitations, intended and prohibited uses, and named owners. For the deployed application I add a system card describing how the model is used with retrieval, tools, guardrails and human oversight, since risk comes from the whole system. Documentation should be versioned, kept up to date, and written for readers such as auditors, product teams and affected users, not just engineers.

**Red-flag answers:** Says a README is enough; Lists no limitations or prohibited uses; Gives no evaluation by segment.

**Expect this follow-up:** Who reads the model card, and what do they need from it?

</details>

All 30 questions with answers: [questions/05-responsible-ai-governance-engineer.md](questions/05-responsible-ai-governance-engineer.md)

**Full breakdown:** [Responsible AI / AI Governance Engineer interview simulator with all 30 scenarios and a write-first answer box](https://aidevdayindia.org/interview-questions/responsible-ai-governance-engineer-interview-questions.html)

## LLMOps Engineer

Covers deploying and versioning LLM applications, monitoring, cost and latency control, provider outages and rate limits, self-hosting, quality drift, prompt registries, CI/CD, model gateways, tracing, semantic caching, GPU autoscaling, multi-tenancy, secrets, privacy in logs, SLOs, cost attribution and runbooks. Answers are expected to be operational: what you monitor, what pages you at 2am, and what you change after an incident. Most questions are Practitioner level. The set has 30 questions: 2 Foundation, 19 Practitioner and 9 Advanced.

**Competencies covered:** Deployment, Monitoring, Cost Control, Latency, Reliability, Self-hosting, Quality Drift, Incident, Prompt Registry, CI/CD, Model Gateway, Tracing, Semantic Caching, GPU Autoscaling, Inference Optimisation, Multi-tenancy, Secrets, Logging & Privacy, Index Refresh, Feature Flags, SLOs, Cost Attribution, Model Registry, Runbooks, Staging, Observability, Rate Limits, Data Governance, plus one behavioural question.

**Sample scenario (Foundation): How do you manage API keys and secrets for LLM services?**

<details>
<summary>Model answer, red flags and follow-up</summary>

API keys live in a secrets manager, never in code, prompts or logs. They are scoped by service and environment, rotated regularly, and issued with the minimum permissions. I monitor usage for anomalies such as sudden spikes, which can indicate a leak, and set spending limits on keys. Developers get separate keys from production. Where possible I use short-lived credentials or workload identity, and have a tested procedure for revoking and replacing a compromised key quickly.

**Red-flag answers:** Keeps keys in code or config files; Never rotates them; Puts secrets in prompts or logs.

**Expect this follow-up:** A key leaks in a log. What do you do?

</details>

All 30 questions with answers: [questions/06-llmops-engineer.md](questions/06-llmops-engineer.md)

**Full breakdown:** [LLMOps Engineer interview simulator with all 30 scenarios and a write-first answer box](https://aidevdayindia.org/interview-questions/llmops-engineer-interview-questions.html)

## AI Solutions Architect

Covers enterprise GenAI architecture, build versus buy versus partner, RAG versus fine-tuning, security, multi-model design, scale and total cost of ownership, PoC-to-production gaps, vendor evaluation, identity and access, model migration, edge AI, AI technical debt and workflow versus agent decisions. Strong answers explain trade-offs to non-technical stakeholders and say what evidence would change the recommendation. The set ends with a question about an architecture decision you got wrong. The set has 30 questions: 4 Foundation, 17 Practitioner and 9 Advanced.

**Competencies covered:** Architecture, Build vs Buy, RAG vs Fine-tuning, Security, Multi-model, Scale & Cost, Stakeholders, Legacy, RAG Reference, Data Architecture, Hosting Choices, Latency Design, Multi-tenant SaaS, Resilience, Integration Patterns, Enterprise Agents, TCO, PoC to Production, Vendor Selection, Identity & Access, Model Migration, Vendor Claims, Edge AI, AI Tech Debt, Workflow vs Agent, Governance, Data Privacy, Evaluation, Generative AI Strategy, plus one behavioural question.

**Sample scenario (Foundation): How do you advise a client choosing between RAG and fine-tuning?**

<details>
<summary>Model answer, red flags and follow-up</summary>

I explain that they solve different problems. RAG suits knowledge that changes or is proprietary, and it gives citations and easy updates. Fine-tuning suits consistent style, format or behaviour, or making a smaller model perform a narrow task. Usually I recommend starting with good prompting and RAG, measuring with an eval set, and fine-tuning only where the evals show a gap that remains. They can also be combined. The client should leave knowing what evidence would change my recommendation.

**Red-flag answers:** Says fine-tuning is always better; Ignores citations and freshness; Doesn't start with prompting.

**Expect this follow-up:** The client insists on fine-tuning. How do you respond?

</details>

All 30 questions with answers: [questions/07-ai-solutions-architect.md](questions/07-ai-solutions-architect.md)

**Full breakdown:** [AI Solutions Architect interview simulator with all 30 scenarios and a write-first answer box](https://aidevdayindia.org/interview-questions/ai-solutions-architect-interview-questions.html)

## Quick reference assets

- **[`questions/`](questions/)**: seven Markdown files, 30 questions each, with a contents list, collapsible answers and red flags. Works as a printable study pack.
- **[`data/ai-engineering-interview-questions.csv`](data/ai-engineering-interview-questions.csv)**: all 210 rows with competency, difficulty, answer, red flags and follow-up. Import into Anki, Notion, a spreadsheet or pandas.
- **[`CHECKLIST.md`](CHECKLIST.md)**: 210 questions, each with its red-flag answers and follow-up as tick boxes for self-checking before an interview.
- **[`CHEATSHEET.md`](CHEATSHEET.md)**: the three-step method, role map, themes that recur across roles, the 27 Foundation questions and the behavioural question for each role.

## Sources & deeper reading

The questions and answers come from these pages, last updated 30 September 2026 on the source site:

- [AI engineering interview questions: overview of all 7 roles](https://aidevdayindia.org/interview-questions/ai-interview-prep.html)
- [AI Engineer (Prompt & Context Engineering) interview questions and answers](https://aidevdayindia.org/interview-questions/ai-engineer-interview-questions.html)
- [Agentic AI Engineer interview questions and answers](https://aidevdayindia.org/interview-questions/agentic-ai-engineer-interview-questions.html)
- [AI Evaluation Engineer interview questions and answers](https://aidevdayindia.org/interview-questions/ai-evaluation-engineer-interview-questions.html)
- [Forward Deployed Engineer interview questions and answers](https://aidevdayindia.org/interview-questions/forward-deployed-engineer-interview-questions.html)
- [Responsible AI / AI Governance Engineer interview questions and answers](https://aidevdayindia.org/interview-questions/responsible-ai-governance-engineer-interview-questions.html)
- [LLMOps Engineer interview questions and answers](https://aidevdayindia.org/interview-questions/llmops-engineer-interview-questions.html)
- [AI Solutions Architect interview questions and answers](https://aidevdayindia.org/interview-questions/ai-solutions-architect-interview-questions.html)

## Contributing / corrections

Tools, regulations and provider behaviour change quickly. If an answer is wrong, outdated or unclear, [open a correction issue](https://github.com/ayushbishtdev/ai-engineering-interview-questions/issues/new?template=correction.md) with the role, question number and what it should say. Pull requests that fix a question or answer in `questions/` are welcome; please update the matching row in the CSV too. The repo is reviewed quarterly.

## License

Content is licensed under CC BY 4.0. Share and adapt it with attribution to this repository.

## About the author

Written by Ayush Bisht ([@ayushbishtdev](https://github.com/ayushbishtdev)). More AI engineering resources live at [aidevdayindia.org](https://aidevdayindia.org/).
