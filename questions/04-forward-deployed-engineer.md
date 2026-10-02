# Forward Deployed Engineer: 30 interview questions with model answers

Thirty scenarios on customer scoping, messy data, trust, security reviews and taking pilots to production. Write your own answer first, then open the model answer to compare structure and reasoning.

Level mix: 5 Foundation, 18 Practitioner, 7 Advanced. Each question lists what the interviewer is testing, a model answer, red-flag answers to avoid, and the follow-up to expect.

## Contents

1. [What does a forward deployed engineer do that a regular engineer doesn't?](#q1) (Role, Foundation)
2. [A customer asks for 'an AI agent for everything'. How do you scope it?](#q2) (Scoping, Practitioner)
3. [The customer's data is messy and locked in legacy systems. What do you do?](#q3) (Messy Data, Practitioner)
4. [How do you build trust with sceptical stakeholders at a customer?](#q4) (Trust, Practitioner)
5. [How do you turn customer-specific work into product improvements?](#q5) (Product Feedback, Practitioner)
6. [The customer's security team blocks your deployment. How do you respond?](#q6) (Security Review, Practitioner)
7. [How do you take a successful demo to production?](#q7) (Production, Practitioner)
8. [The customer keeps adding requests mid-pilot. What do you do?](#q8) (Scope Creep, Practitioner)
9. [How do you run discovery with a new customer?](#q9) (Discovery, Foundation)
10. [How do you design a demo that convinces a customer?](#q10) (Demos, Foundation)
11. [Your executive sponsor leaves mid-project. What do you do?](#q11) (Sponsor Change, Advanced)
12. [Users aren't using the solution you delivered. What do you do?](#q12) (Adoption, Practitioner)
13. [How do you integrate with legacy ERP or CRM systems?](#q13) (Legacy Integration, Practitioner)
14. [How do you set expectations about AI accuracy with a customer?](#q14) (Accuracy Expectations, Practitioner)
15. [How do you hand over a solution to the customer's team?](#q15) (Handover, Practitioner)
16. [How do you show ROI to a customer's leadership?](#q16) (Value Story, Practitioner)
17. [A pilot didn't meet its success criteria. How do you handle it?](#q17) (Failed Pilot, Advanced)
18. [You support several customers with urgent requests. How do you prioritise?](#q18) (Prioritisation, Practitioner)
19. [How do you work with sales without overpromising?](#q19) (Working with Sales, Practitioner)
20. [Two customer departments want conflicting behaviour from the system. What do you do?](#q20) (Stakeholder Conflict, Advanced)
21. [A customer bug needs a product fix that engineering hasn't prioritised. How do you escalate?](#q21) (Internal Escalation, Practitioner)
22. [How do you train a customer's engineers to work with the solution?](#q22) (Training, Foundation)
23. [A customer requires data to stay in a specific region. How do you respond?](#q23) (Data Residency, Practitioner)
24. [How do you balance fast prototyping with technical debt?](#q24) (Prototype Debt, Practitioner)
25. [How do you deliver bad news to a customer?](#q25) (Bad News, Advanced)
26. [A customer wants a fine-tuned model, but you think retrieval plus prompting would work. How do you handle the disagreement?](#q26) (Technical Judgement, Practitioner)
27. [How do you explain a technical limitation to a non-technical executive?](#q27) (Communication, Foundation)
28. [You are two weeks from a customer go-live and evals show the system misses the agreed accuracy threshold. What do you do?](#q28) (Delivery, Advanced)
29. [The customer wants to send confidential documents to a hosted model API. What questions do you ask?](#q29) (Security, Advanced)
30. [Tell me about a deployment that went wrong at a customer site. What did you do and what did you change?](#q30) (Behavioural, Advanced)

<a id="q1"></a>

### 1. What does a forward deployed engineer do that a regular engineer doesn't?

**Competency:** Role | **Level:** Foundation

**What it tests:** Whether you define the role by customer outcomes.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A forward deployed engineer works inside the customer's environment to turn messy, real needs into working solutions quickly. That means scoping problems with the people who live with them, integrating with the customer's systems, deploying, supporting adoption and feeding what they learn back to the product team. Customer outcomes matter as much as code quality, and much of the job is judgement about what to build, what to skip and what to tell the customer honestly. A regular engineer usually works from a defined spec; an FDE often has to help create it.

**Red-flag answers**

- Describes it as regular engineering with travel
- Ignores customer outcomes
- Doesn't mention feeding learnings back to product

**Expect this follow-up:** Give an example of a customer learning that changed a product.

</details>

<a id="q2"></a>

### 2. A customer asks for 'an AI agent for everything'. How do you scope it?

**Competency:** Scoping | **Level:** Practitioner

**What it tests:** Whether you narrow a broad ask to one valuable pilot.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I resist saying yes to everything and instead find the single highest-value workflow, the one with a clear owner, available data and a measurable outcome. I define success metrics and constraints, agree a small pilot with a fixed timeline, and write down what is explicitly out of scope. Early wins build trust and reveal the real requirements, which are rarely the ones in the first request. I present it as a sequence, so the ambitious vision remains visible as later phases and the customer feels heard.

**Red-flag answers**

- Says yes to everything
- Sets no success metrics
- Doesn't define what is out of scope

**Expect this follow-up:** The customer insists on all use cases at once. What do you say?

</details>

<a id="q3"></a>

### 3. The customer's data is messy and locked in legacy systems. What do you do?

**Competency:** Messy Data | **Level:** Practitioner

**What it tests:** Whether you deliver value despite poor data.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start with a narrow slice of data that supports one use case rather than trying to fix everything. I build minimal connectors, clean only what the use case needs, and involve the customer's data owners early because they know the quirks. I document every assumption and known data-quality issue so nobody is surprised later. This lets me show value quickly while planning the longer data work openly. I also flag risks, such as unreliable fields, before they undermine the model's results.

**Red-flag answers**

- Waits for perfect data
- Cleans everything up front
- Ignores the customer's data owners

**Expect this follow-up:** How do you show value in two weeks with poor data?

</details>

<a id="q4"></a>

### 4. How do you build trust with sceptical stakeholders at a customer?

**Competency:** Trust | **Level:** Practitioner

**What it tests:** Whether you earn trust through small, verifiable wins.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I begin by listening, so I understand their concerns and what has failed for them before. Then I deliver small, verifiable wins in their own metrics, share progress frequently and am candid about limits and risks. Admitting what the system cannot do builds more credibility than overselling. I involve sceptics in testing so their concerns shape the solution, and I follow through on every small commitment. Trust is earned through consistent behaviour over weeks, not persuasion in a meeting.

**Red-flag answers**

- Argues with sceptics
- Overpromises to win them over
- Measures success in their own metrics, not the customer's

**Expect this follow-up:** A stakeholder openly says AI won't work here. What do you do?

</details>

<a id="q5"></a>

### 5. How do you turn customer-specific work into product improvements?

**Competency:** Product Feedback | **Level:** Practitioner

**What it tests:** Whether you generalise customer needs into product change.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I look for patterns across customers, since one request is an anecdote and five is a signal. I separate genuine one-offs from general needs, then write feedback with evidence: the customer problem, how often it appears, the impact and a workaround if one exists. I work with product managers early, explain the underlying need rather than only proposing a feature, and help prototype a generalisable solution. Closing the loop matters too, so customers see their feedback reflected and keep giving it.

**Red-flag answers**

- Ships every custom request into the product
- Has no evidence across deployments
- Doesn't separate one-offs from general needs

**Expect this follow-up:** How do you decide when a request deserves a product change?

</details>

<a id="q6"></a>

### 6. The customer's security team blocks your deployment. How do you respond?

**Competency:** Security Review | **Level:** Practitioner

**What it tests:** Whether you work with security teams instead of against them.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I treat the security team as a partner, not an obstacle. First I understand their specific concerns, then I share architecture diagrams, data-flow documentation and relevant certifications. I offer options that reduce risk, such as private deployment, data redaction, restricted permissions or a limited-scope first release. I follow their process patiently, respond quickly to questions and keep the business sponsor informed of timelines. Trying to bypass security destroys trust and usually delays the project more than working through it.

**Red-flag answers**

- Argues the security team is being difficult
- Has no data-flow documentation
- Offers no deployment options

**Expect this follow-up:** The security team asks for a private deployment. Can you do it, and how?

</details>

<a id="q7"></a>

### 7. How do you take a successful demo to production?

**Competency:** Production | **Level:** Practitioner

**What it tests:** Whether you know what a demo hides.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A demo hides the edge cases production reveals. To move to production I add evaluation on realistic data, monitoring and alerting, error handling and fallbacks, access controls, and logging for audit. I agree service levels with the customer, define who supports what, train users and plan the rollout in stages. I also review cost at real volume. The work between a working demo and a reliable service is often larger than building the demo, and setting that expectation early avoids conflict.

**Red-flag answers**

- Ships the demo as-is
- Adds no evals, monitoring or fallbacks
- Ignores training and support

**Expect this follow-up:** What breaks first when a demo goes live?

</details>

<a id="q8"></a>

### 8. The customer keeps adding requests mid-pilot. What do you do?

**Competency:** Scope Creep | **Level:** Practitioner

**What it tests:** Whether you protect the pilot and the relationship.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I go back to the success criteria we agreed at the start and treat new requests as candidates, not commitments. I log each one, discuss value and effort with the sponsor, and decide together what enters the pilot and what goes to a second phase. This protects the timeline and shows respect for the customer's ideas. I keep the tone collaborative, not defensive, and make trade-offs explicit: adding this means delaying that. Uncontrolled scope is the most common way pilots fail.

**Red-flag answers**

- Says yes to keep the customer happy
- Refuses all new requests
- Doesn't log or prioritise them

**Expect this follow-up:** The sponsor says the new request is critical. What do you do?

</details>

<a id="q9"></a>

### 9. How do you run discovery with a new customer?

**Competency:** Discovery | **Level:** Foundation

**What it tests:** Whether discovery observes real workflows.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I interview the people who do the work as well as the owners, and I watch the actual workflow rather than only hearing it described. I gather data samples, and identify pain points, constraints, integration needs and success metrics. I look for the difference between what people say and what they do. I leave discovery with a prioritised list of use cases, clear assumptions, the risks I see, and a shared understanding of what a good outcome looks like in numbers.

**Red-flag answers**

- Runs a feature-led questionnaire
- Talks only to executives
- Doesn't observe the real workflow

**Expect this follow-up:** What do you do in your first day on site?

</details>

<a id="q10"></a>

### 10. How do you design a demo that convinces a customer?

**Competency:** Demos | **Level:** Foundation

**What it tests:** Whether your demos are relevant, honest and metric-linked.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I use the customer's own data and workflow so they can see their problem being solved. I show the before and after, connect it to a metric they care about, and keep it short. I include an honest failure case and explain how the design handles it, which makes the rest more credible. I rehearse with a fallback for when something breaks. A focused ten-minute demo on their process beats a broad tour of features, because it lets them imagine using it.

**Red-flag answers**

- Shows a generic feature tour
- Uses fake data
- Hides failure cases

**Expect this follow-up:** The demo fails live. What do you do?

</details>

<a id="q11"></a>

### 11. Your executive sponsor leaves mid-project. What do you do?

**Competency:** Sponsor Change | **Level:** Advanced

**What it tests:** Whether you keep momentum when sponsorship changes.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I move quickly to map the new stakeholders and understand who now owns the outcome. I re-confirm the goals and value with the successor rather than assume they inherit the same priorities, and I look for a new executive sponsor who will defend the project. I document results so far in business terms so the value is visible to someone who was not there. I also check for risks to budget and priority. Momentum survives sponsor changes when the business outcomes are clear.

**Red-flag answers**

- Waits for a replacement to appear
- Loses momentum
- Doesn't document results so far

**Expect this follow-up:** The new sponsor doubts the project's value. What is your first meeting?

</details>

<a id="q12"></a>

### 12. Users aren't using the solution you delivered. What do you do?

**Competency:** Adoption | **Level:** Practitioner

**What it tests:** Whether you diagnose low adoption from user friction.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start by observing and interviewing users to find out why they are not using it: lack of trust, poor fit with their workflow, insufficient training, or a real defect. I fix the top friction points first, involve champions inside the team, and provide short, practical training. I track adoption metrics such as active users and task completion so improvement is visible. Sometimes low adoption shows I solved the wrong problem, and I say so and adjust the scope with the customer.

**Red-flag answers**

- Blames users for not adopting
- Adds more features
- Doesn't talk to users

**Expect this follow-up:** Users say they don't trust the output. What do you do?

</details>

<a id="q13"></a>

### 13. How do you integrate with legacy ERP or CRM systems?

**Competency:** Legacy Integration | **Level:** Practitioner

**What it tests:** Whether you integrate with legacy systems safely.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I begin by understanding the system's APIs, data model, change controls and release cycles. I start with read-only access to reduce risk, build thin adapters that isolate the legacy quirks, and test in a sandbox before touching production. I plan around their downtime windows and approval processes, which can take weeks. I document the integration carefully because the people who know the system are often few. Where APIs are missing, I discuss alternatives such as exports or events early.

**Red-flag answers**

- Asks for write access on day one
- Ignores their release cycles
- Skips a sandbox

**Expect this follow-up:** The ERP has no API. What options do you consider?

</details>

<a id="q14"></a>

### 14. How do you set expectations about AI accuracy with a customer?

**Competency:** Accuracy Expectations | **Level:** Practitioner

**What it tests:** Whether you set honest, measurable accuracy expectations.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I explain plainly that the system is probabilistic and will sometimes be wrong. Then I agree measurable thresholds with the customer, based on their own data, and show results on a test set they helped to define. I design fallbacks and human review for the cases that matter most, and set out how errors will be handled. Early honesty prevents disappointment later, and it moves the conversation from whether the AI is perfect to whether it is useful enough with the right safeguards.

**Red-flag answers**

- Promises 99% accuracy
- Doesn't test on their data
- Offers no fallback or review step

**Expect this follow-up:** Accuracy is 88% and they expected 95%. What do you do?

</details>

<a id="q15"></a>

### 15. How do you hand over a solution to the customer's team?

**Competency:** Handover | **Level:** Practitioner

**What it tests:** Whether the customer can operate and evolve the solution.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A good handover is planned from the start. I provide documentation and runbooks, monitoring dashboards, training sessions for the people who will operate it, and a clear support path. Ownership transitions gradually: they shadow me, then I shadow them. I test understanding with real tasks, such as having them handle an incident or a small change. The goal is that they can operate and evolve the solution without me, and I check that by stepping back before I leave.

**Red-flag answers**

- Hands over a repository and leaves
- Provides no runbooks or training
- Keeps sole ownership

**Expect this follow-up:** What must the customer's team be able to do on day one after handover?

</details>

<a id="q16"></a>

### 16. How do you show ROI to a customer's leadership?

**Competency:** Value Story | **Level:** Practitioner

**What it tests:** Whether you prove ROI with baselines and assumptions.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I establish a baseline for the target metric before deployment, then measure the change after: time saved, errors reduced, throughput or revenue effect. I present it in the customer's financial terms and language, with assumptions stated openly and conservative estimates. I separate measured results from projections and include costs, including running costs. Leadership trusts a modest, well-evidenced number more than an impressive one they cannot verify, and it makes expansion easier to approve.

**Red-flag answers**

- Cites usage numbers only
- Has no baseline
- Hides assumptions

**Expect this follow-up:** Time saved is real but hard to convert to money. How do you present it?

</details>

<a id="q17"></a>

### 17. A pilot didn't meet its success criteria. How do you handle it?

**Competency:** Failed Pilot | **Level:** Advanced

**What it tests:** Whether you handle failure with honesty and a recommendation.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start by analysing honestly why it missed: data quality, scope, adoption, technology or unrealistic expectations. I share findings openly with the customer, including my own part, and recommend one of three paths: stop, fix and retry, or pivot to a better use case. Transparency protects trust and often leads to a stronger second attempt. I also capture the lessons internally so the same mistake does not repeat. A pilot that ends with a clear learning is not a wasted effort.

**Red-flag answers**

- Blames the customer or the data
- Hides the results
- Makes no recommendation

**Expect this follow-up:** The customer wants to stop entirely. What do you say?

</details>

<a id="q18"></a>

### 18. You support several customers with urgent requests. How do you prioritise?

**Competency:** Prioritisation | **Level:** Practitioner

**What it tests:** Whether you prioritise across customers transparently.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I weigh impact, contractual risk, effort, strategic value and deadlines, and I do it transparently. I tell each customer what I can do and when, rather than promising everything and missing dates. When priorities genuinely conflict, I involve my manager early so trade-offs are made at the right level, not silently by me. I look for ways to reuse work across customers, and for tasks that can be delegated or automated. Clear communication keeps expectations realistic, which matters more than speed on every request.

**Red-flag answers**

- Answers whoever shouts loudest
- Says nothing about timelines
- Doesn't involve the manager on conflicts

**Expect this follow-up:** Two customers have equal urgency. How do you decide?

</details>

<a id="q19"></a>

### 19. How do you work with sales without overpromising?

**Competency:** Working with Sales | **Level:** Practitioner

**What it tests:** Whether you prevent overpromising with early involvement.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I join scoping calls early so feasibility is part of the conversation, not something discovered after signing. I help define what is realistic, write assumptions and risks into the proposal, and give sales clear language about limits. We agree shared success criteria so we are measured on the same outcomes. When I have to say no to a promise, I do it privately and offer an alternative the sales team can present positively. A good relationship with sales is built on being both helpful and honest.

**Red-flag answers**

- Lets sales define the scope
- Skips early scoping calls
- Documents no assumptions

**Expect this follow-up:** Sales already promised a date you can't meet. What do you do?

</details>

<a id="q20"></a>

### 20. Two customer departments want conflicting behaviour from the system. What do you do?

**Competency:** Stakeholder Conflict | **Level:** Advanced

**What it tests:** Whether you resolve customer conflicts through sponsor decisions.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I bring the groups together to surface each one's goals and constraints, which often reveals the conflict is smaller than it appeared. Then I look for a configurable solution, a phased approach, or a rule that serves both. If they cannot agree, I escalate to the sponsor for a decision, with a clear recommendation and the trade-offs laid out. I avoid quietly favouring one side. The customer needs an explicit decision made by the person with the authority to make it.

**Red-flag answers**

- Picks the more senior department
- Builds both behaviours with no discussion
- Doesn't escalate

**Expect this follow-up:** The sponsor is unavailable. How do you move forward?

</details>

<a id="q21"></a>

### 21. A customer bug needs a product fix that engineering hasn't prioritised. How do you escalate?

**Competency:** Internal Escalation | **Level:** Practitioner

**What it tests:** Whether you escalate with evidence and workarounds.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I document the customer impact with evidence: how many users, what is failing and the business risk, including revenue where relevant. I propose a workaround and an interim fix, and raise the issue through the agreed channel with a clear ask and deadline. I keep the customer updated regularly even when there is no news, so they know it has not been forgotten. If the priority does not change, I escalate with data to the right leader. Internal persuasion is part of the job.

**Red-flag answers**

- Waits silently for engineering
- Escalates emotionally
- Offers no workaround

**Expect this follow-up:** What evidence would convince engineering to prioritise the bug?

</details>

<a id="q22"></a>

### 22. How do you train a customer's engineers to work with the solution?

**Competency:** Training | **Level:** Foundation

**What it tests:** Whether you train customers hands-on in their environment.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I run hands-on workshops in their own environment using their data, supported by clear documentation and example code. I then offer office hours and let them do real tasks while I shadow, before they take over. I check understanding with practical exercises, not by asking whether they understand. I tailor depth to the audience, since operators, developers and managers need different things. The best measure of training is whether they can fix a problem without me.

**Red-flag answers**

- Runs a slide-only session
- Skips their environment
- Doesn't check understanding

**Expect this follow-up:** How do you know the customer's engineers are ready to take over?

</details>

<a id="q23"></a>

### 23. A customer requires data to stay in a specific region. How do you respond?

**Competency:** Data Residency | **Level:** Practitioner

**What it tests:** Whether you respond to residency needs with facts.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I first confirm exactly what the requirement covers: storage, processing, logs, backups and support access. Then I review the architecture and provider regions to see what is possible. Options include regional deployment, private hosting or an on-premises model, each with cost and capability trade-offs that I explain. I document the data flows clearly for their compliance team and involve legal early. If the requirement cannot be met, I say so early rather than at the end of the project.

**Red-flag answers**

- Says it can't be done without checking
- Ignores logs and backups
- Doesn't document data flows

**Expect this follow-up:** The model provider has no region there. What do you offer?

</details>

<a id="q24"></a>

### 24. How do you balance fast prototyping with technical debt?

**Competency:** Prototype Debt | **Level:** Practitioner

**What it tests:** Whether you move fast without shipping throwaway code.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I prototype fast to learn, but I label prototype code clearly and set exit criteria for when it must be replaced. Once the idea is proven, I rebuild the parts that will live on with tests, monitoring, security and proper configuration. I explain to the customer that this step is part of delivery, not extra work. The worst outcome is a demo quietly becoming production without anyone deciding it should, because that is where outages and security incidents come from.

**Red-flag answers**

- Ships the prototype as production
- Sets no exit criteria
- Never labels throwaway code

**Expect this follow-up:** How do you decide which prototype parts to rebuild?

</details>

<a id="q25"></a>

### 25. How do you deliver bad news to a customer?

**Competency:** Bad News | **Level:** Advanced

**What it tests:** Whether you deliver bad news early, with options.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I tell them early and directly, before they hear it elsewhere. I state what happened, the impact, what we are doing about it and when they will hear next. I bring options and a recommendation, take ownership without blaming individuals or the customer, and follow through on the update times I promised. I avoid burying the message in caveats. Customers generally tolerate problems; they do not tolerate surprises or evasiveness, and handled well, bad news can strengthen the relationship.

**Red-flag answers**

- Delays until forced to share
- Blames others
- Arrives with no options

**Expect this follow-up:** You caused the problem. How does the conversation change?

</details>

<a id="q26"></a>

### 26. A customer wants a fine-tuned model, but you think retrieval plus prompting would work. How do you handle the disagreement?

**Competency:** Technical Judgement | **Level:** Practitioner

**What it tests:** Whether you resolve technical disagreement with evidence and respect.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I take their reasoning seriously first, because they may have constraints I do not know about. Then I propose a quick test on their own data: a baseline with retrieval and prompting, measured against the quality bar we agree. If the baseline meets it, we save time and cost; if it falls short, we have evidence for fine-tuning and know where the gap is. I explain trade-offs in terms they care about, such as speed, maintenance and cost, and I let the data lead rather than winning the argument.

**Red-flag answers**

- Dismisses their request outright
- Argues without offering a test
- Agrees to build something they doubt without evidence

**Expect this follow-up:** The test is inconclusive. What do you recommend?

</details>

<a id="q27"></a>

### 27. How do you explain a technical limitation to a non-technical executive?

**Competency:** Communication | **Level:** Foundation

**What it tests:** Whether you communicate constraints in business terms without jargon or hedging.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start with the business consequence, not the mechanism: what it means for cost, risk, timeline or customer experience. I use a simple analogy where it helps, offer options and my recommendation, and avoid jargon. I am honest about uncertainty without burying the message in caveats. I check understanding by asking what they would take away, and I follow up in writing. Executives want to know what decision they need to make and what happens if they choose each path.

**Red-flag answers**

- Explains the internals at length
- Hides the limitation to avoid friction
- Offers no options or recommendation

**Expect this follow-up:** The executive says 'just make it work'. How do you respond?

</details>

<a id="q28"></a>

### 28. You are two weeks from a customer go-live and evals show the system misses the agreed accuracy threshold. What do you do?

**Competency:** Delivery | **Level:** Advanced

**What it tests:** Whether you protect the customer and the relationship over the date.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I tell the customer now, with data, not at the deadline. I analyse where the misses are, since a fix might be narrow, and I present options: delay, launch with reduced scope, launch with human review on low-confidence cases, or a staged rollout. I make a recommendation and the risks of each, and let the sponsor decide. I do not lower the bar quietly or ship and hope. Trust depends on the customer knowing I will be straight with them even when it is inconvenient.

**Red-flag answers**

- Ships anyway and hopes
- Quietly redefines the threshold
- Tells the customer only at the deadline

**Expect this follow-up:** The sponsor insists on going live on time. What safeguards do you put in place?

</details>

<a id="q29"></a>

### 29. The customer wants to send confidential documents to a hosted model API. What questions do you ask?

**Competency:** Security | **Level:** Advanced

**What it tests:** Whether you probe data handling and compliance before deploying.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I ask what is in the documents and how sensitive it is, which regulations and contracts apply, and where data may be processed and stored. I check the provider's terms on retention and training, options such as zero retention or private endpoints, and whether redaction can remove the sensitive fields. I ask who must approve, and how access and logs will be controlled. If the answers show unacceptable risk, I propose alternatives such as a private deployment. The conversation should end with a documented decision.

**Red-flag answers**

- Sends the data without checking terms
- Ignores contractual obligations
- Proposes no alternative if risk is high

**Expect this follow-up:** The provider's terms allow 30-day retention. The customer requires none. What now?

</details>

<a id="q30"></a>

### 30. Tell me about a deployment that went wrong at a customer site. What did you do and what did you change?

**Competency:** Behavioural | **Level:** Advanced

**What it tests:** Whether you take ownership, communicate under pressure and learn.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A strong answer names a real incident and its customer impact, then walks through what I did in order: stabilising the situation, communicating early and honestly, finding the cause and fixing it. I would describe how I kept the customer informed and what I owned. Then the lasting changes: better testing, monitoring or a deployment checklist, so it cannot recur. I would mention what I learned about the relationship, since how you handle a bad day often defines the account.

**Red-flag answers**

- Blames the customer or a colleague
- Describes an incident with no real impact
- Cannot name what changed afterwards

**Expect this follow-up:** What would the customer say about how you handled it?

</details>

---

Prefer to practise with a write-first answer box? The same scenarios are in the [Forward Deployed Engineer interview simulator](https://aidevdayindia.org/interview-questions/forward-deployed-engineer-interview-questions.html). Spotted a wrong or outdated answer? [Open a correction issue](https://github.com/ayushbishtdev/ai-engineering-interview-questions/issues/new?template=correction.md).
