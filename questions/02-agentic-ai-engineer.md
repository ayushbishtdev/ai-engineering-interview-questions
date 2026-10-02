# Agentic AI Engineer: 30 interview questions with model answers

Thirty scenarios on agent design, tools and MCP, guardrails, memory, multi-agent systems and observability. Write your own answer first, then open the model answer to compare structure and reasoning.

Level mix: 3 Foundation, 16 Practitioner, 11 Advanced. Each question lists what the interviewer is testing, a model answer, red-flag answers to avoid, and the follow-up to expect.

## Contents

1. [When should you use an agent instead of a fixed workflow?](#q1) (Agent Design, Practitioner)
2. [How do you design tools so an agent uses them correctly?](#q2) (Tool Design, Practitioner)
3. [What problem does the Model Context Protocol solve?](#q3) (MCP, Foundation)
4. [How do you stop an agent from taking harmful actions?](#q4) (Guardrails, Advanced)
5. [How do you handle memory in a long-running agent?](#q5) (Memory, Practitioner)
6. [An agent keeps looping and burning tokens. What do you do?](#q6) (Failure Loops, Practitioner)
7. [When are multi-agent systems worth the extra complexity?](#q7) (Multi-agent, Advanced)
8. [How do you debug a wrong agent decision after the fact?](#q8) (Observability, Practitioner)
9. [How do agents plan, and when do you choose plan-then-execute over ReAct?](#q9) (Planning, Practitioner)
10. [How do you design human-in-the-loop approvals for an agent?](#q10) (Human Approval, Practitioner)
11. [How can tool outputs be used to attack an agent, and what do you do?](#q11) (Tool Injection, Advanced)
12. [How do you evaluate an agent end to end?](#q12) (Agent Evals, Advanced)
13. [How do you keep agent session costs predictable?](#q13) (Cost Control, Practitioner)
14. [How do you make long-running agents resumable?](#q14) (State & Resume, Advanced)
15. [How should an agent handle tool failures?](#q15) (Tool Errors, Practitioner)
16. [How do you choose an agent framework?](#q16) (Frameworks, Foundation)
17. [How do you handle tasks that take hours or many steps?](#q17) (Long Tasks, Practitioner)
18. [How do you give agents access to user accounts safely?](#q18) (Delegated Access, Advanced)
19. [How do you safely let an agent execute code?](#q19) (Code Sandbox, Advanced)
20. [Agent context grows with every step. How do you manage it?](#q20) (Context Growth, Practitioner)
21. [What is agent-to-agent communication and when do you need it?](#q21) (A2A, Advanced)
22. [Which metrics show whether an agent is production-ready?](#q22) (Reliability Metrics, Practitioner)
23. [How do you test agents whose behaviour varies run to run?](#q23) (Non-determinism, Practitioner)
24. [How should an agent handle an ambiguous goal?](#q24) (Clarification, Foundation)
25. [How do you roll out a new agent to users safely?](#q25) (Rollout, Practitioner)
26. [How do you write the system prompt for an agent so its behaviour stays predictable?](#q26) (Prompt Design, Practitioner)
27. [Your agent passes its evals but users say it is unreliable. What could explain the gap?](#q27) (Evaluation, Advanced)
28. [An agent can read email and also send it. What risks does that combination create, and how do you reduce them?](#q28) (Security, Advanced)
29. [A user asks the agent to complete a task that will take 20 minutes. How do you design the experience?](#q29) (Trade-offs, Practitioner)
30. [Tell me about an agent behaviour that surprised you in testing. How did you respond?](#q30) (Behavioural, Advanced)

<a id="q1"></a>

### 1. When should you use an agent instead of a fixed workflow?

**Competency:** Agent Design | **Level:** Practitioner

**What it tests:** Whether you add autonomy only where it pays off.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I use an agent when the steps cannot be known in advance and the task needs dynamic tool choices, such as investigating an unfamiliar bug. If the path is predictable, a fixed workflow with model calls at specific steps is cheaper, faster and far easier to test and audit. I start with the simplest design that works and add autonomy only where it clearly pays off, measured by task success against cost and latency. Many good systems are workflows with one small agentic step inside, which keeps most of the behaviour predictable.

**Red-flag answers**

- Says agents are always better than workflows
- Cannot explain when a fixed workflow is cheaper and easier to test
- Adds autonomy everywhere from day one

**Expect this follow-up:** Give a task where you would deliberately choose a workflow over an agent.

</details>

<a id="q2"></a>

### 2. How do you design tools so an agent uses them correctly?

**Competency:** Tool Design | **Level:** Practitioner

**What it tests:** Whether you design tools a model can use correctly.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I make tools narrow, clearly named and well described, with typed parameters, enums for closed choices and examples of correct use. Results are compact and structured, and errors say what went wrong and how to fix it. Tools are idempotent where possible so a retry is safe. I prefer a few non-overlapping tools to many similar ones, because overlap causes wrong selection. Then I test tool choice and argument accuracy on realistic tasks, and I treat confusing tool calls in traces as a sign the description needs work, not the model.

**Red-flag answers**

- Builds many overlapping tools
- Uses vague names and descriptions
- Does no tool-selection testing

**Expect this follow-up:** The agent keeps picking the wrong one of two similar tools. What do you change?

</details>

<a id="q3"></a>

### 3. What problem does the Model Context Protocol solve?

**Competency:** MCP | **Level:** Foundation

**What it tests:** Whether you understand MCP's purpose and its trust limits.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

MCP standardises how models and clients connect to tools and data, so one server can work across many applications instead of each needing custom glue. That reduces integration effort and makes capabilities reusable. It does not remove security work. I review each server's permissions, prefer trusted or self-hosted servers, and treat tool descriptions and outputs as untrusted input, since they can carry hidden instructions. I also limit which tools are exposed to a given agent, because a larger tool surface means more chance of misuse.

**Red-flag answers**

- Describes MCP as just another API wrapper
- Trusts tool descriptions from any server
- Ignores server permissions

**Expect this follow-up:** How would you vet a third-party MCP server before connecting it?

</details>

<a id="q4"></a>

### 4. How do you stop an agent from taking harmful actions?

**Competency:** Guardrails | **Level:** Advanced

**What it tests:** Whether safety comes from architecture, not prompt wording.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I assume the agent will sometimes be wrong or manipulated, so safety comes from the environment, not the prompt. Credentials are least-privilege and short-lived, tools are allow-listed, and spend, step and time limits cap the damage. Irreversible or high-impact actions such as payments, deletions and external messages require human approval. Code runs in a sandbox, and every action is logged for audit. I also defend against prompt injection in retrieved content and test with adversarial scenarios before release. A polite instruction not to do harm is not a control.

**Red-flag answers**

- Relies on the prompt saying 'don't do harmful things'
- Gives agents broad admin credentials
- Requires no approval for irreversible actions

**Expect this follow-up:** Which action would you never let an agent take without human approval?

</details>

<a id="q5"></a>

### 5. How do you handle memory in a long-running agent?

**Competency:** Memory | **Level:** Practitioner

**What it tests:** Whether you manage memory as a curated, inspectable store.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I separate working context, which is the current task, from long-term memory in an external store. Older history is summarised or pruned, and I retrieve only memories relevant to the current step. Memories carry timestamps and sources so stale or conflicting ones can be resolved, and users can inspect, correct and delete what the agent remembers. I test for bad memories: outdated facts, contradictions and anything sensitive stored without need. Memory that grows unchecked makes the agent slower, costlier and less accurate.

**Red-flag answers**

- Stuffs full history into context forever
- Gives users no way to inspect or delete memories
- Never tests stale or conflicting memory

**Expect this follow-up:** A user says the agent remembers something wrong. How do you fix it?

</details>

<a id="q6"></a>

### 6. An agent keeps looping and burning tokens. What do you do?

**Competency:** Failure Loops | **Level:** Practitioner

**What it tests:** Whether you contain runaway behaviour and diagnose from traces.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

First I stop the bleeding with step, token and time budgets so no run can burn unlimited tokens. Then I read the traces to find the trigger. Usual causes are a vague goal with no clear stop condition, a tool returning unhelpful errors so the agent retries, or state that is not carried forward. I add repeated-action detection, sharpen the stop criteria and improve tool error messages. When the loop hits a limit, the agent should stop with a useful partial result and escalate, not fail silently.

**Red-flag answers**

- Only raises the token limit
- Sets no step or budget caps
- Doesn't read traces

**Expect this follow-up:** How would you detect a loop automatically in production?

</details>

<a id="q7"></a>

### 7. When are multi-agent systems worth the extra complexity?

**Competency:** Multi-agent | **Level:** Advanced

**What it tests:** Whether you justify multi-agent complexity with evidence.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Multi-agent designs are worth it when subtasks need different tools, context or expertise and can run in parallel, or when isolating noisy work in a sub-agent keeps the main context clean. Otherwise a single agent is simpler, cheaper and easier to debug, because every handoff adds latency, cost and a place for information to get lost. I keep handoffs explicit with structured messages, and I measure whether the multi-agent version actually beats a single agent on my evals. Complexity has to earn its keep.

**Red-flag answers**

- Uses multi-agent by default
- Cannot show coordination improved results
- Leaves handoffs implicit

**Expect this follow-up:** How would you prove a multi-agent design beats a single agent on your task?

</details>

<a id="q8"></a>

### 8. How do you debug a wrong agent decision after the fact?

**Competency:** Observability | **Level:** Practitioner

**What it tests:** Whether you can reproduce and learn from a wrong decision.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I rely on tracing built before the failure. Every run has an ID and records each step: the prompt, retrieved context, tool calls with arguments and results, and the model's reasoning summary or decision. After a bad outcome I replay the trace, find the first step where it diverged from what a good run would do, and identify the cause, whether a tool error, missing context or a misread instruction. The failure then becomes a regression test so it cannot quietly return. Without traces, debugging agents is guesswork.

**Red-flag answers**

- Cannot reproduce the failed run
- Logs only final outputs
- Doesn't turn failures into tests

**Expect this follow-up:** What exactly is in a trace that lets you replay a run?

</details>

<a id="q9"></a>

### 9. How do agents plan, and when do you choose plan-then-execute over ReAct?

**Competency:** Planning | **Level:** Practitioner

**What it tests:** Whether you know when planning beats interleaved reasoning.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

ReAct interleaves reasoning and action, letting the agent adapt to what each tool returns, which suits exploratory tasks with uncertain paths. Plan-then-execute produces a plan first and then follows it, which suits well-structured tasks: the plan can be reviewed or approved, and it usually costs less and errs less. I often combine them: plan up front, execute step by step, and replan when a step fails or new information changes things. I choose by task predictability and by whether a human should see the plan before action.

**Red-flag answers**

- Treats ReAct and plan-then-execute as the same thing
- Never replans on failure
- Offers no reviewable plan for structured tasks

**Expect this follow-up:** The plan was fine but step three failed. What should the agent do?

</details>

<a id="q10"></a>

### 10. How do you design human-in-the-loop approvals for an agent?

**Competency:** Human Approval | **Level:** Practitioner

**What it tests:** Whether approvals are targeted and actually meaningful.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I gate actions that are irreversible or high-impact and let low-risk actions proceed. The reviewer sees what the agent proposes to do, the evidence behind it and the likely impact, so approval is an informed decision rather than a rubber stamp. I keep approvals fast, with clear approve, edit and reject options, so they do not become a bottleneck people route around. I track approval, edit and rejection rates: a near-100% approval rate suggests the gate can be relaxed, while frequent rejections show the agent needs improving.

**Red-flag answers**

- Asks for approval on every action
- Shows reviewers no context or impact
- Never measures override rates

**Expect this follow-up:** Reviewers approve 99% of requests without reading them. What do you do?

</details>

<a id="q11"></a>

### 11. How can tool outputs be used to attack an agent, and what do you do?

**Competency:** Tool Injection | **Level:** Advanced

**What it tests:** Whether you treat tool output as untrusted data.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Tool outputs such as web pages, emails, documents and API responses can contain hidden instructions that try to redirect the agent, for example to send data elsewhere. I treat all tool output as data, never as instructions, and keep it clearly separated in the prompt. Defences are architectural: least-privilege permissions, no free-form access to sensitive tools after reading untrusted content, approval for sensitive actions, and output filtering. I monitor for unexpected tool calls and test with injected documents before launch. Prompt wording alone will not hold.

**Red-flag answers**

- Trusts retrieved content as instructions
- Relies on a single filter
- Doesn't monitor for unexpected tool calls

**Expect this follow-up:** A web page tells the agent to email customer data elsewhere. What stops it?

</details>

<a id="q12"></a>

### 12. How do you evaluate an agent end to end?

**Competency:** Agent Evals | **Level:** Advanced

**What it tests:** Whether you evaluate the path, not only the answer.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I evaluate on realistic end-to-end scenarios in a sandboxed environment, scoring several things: whether the task was completed correctly, the quality of the trajectory, whether tools were used correctly, and the cost and latency. Because runs vary, each scenario runs several times and I report pass rates, not single results. I include adversarial and failure cases such as tool errors and ambiguous goals. Failed traces from production become new regression tests. Judging an agent by its final message alone misses the way it got there.

**Red-flag answers**

- Judges only by the final answer
- Tests only on happy-path demos
- Leaves out cost and latency

**Expect this follow-up:** The agent succeeds but takes 40 steps. Is that a pass?

</details>

<a id="q13"></a>

### 13. How do you keep agent session costs predictable?

**Competency:** Cost Control | **Level:** Practitioner

**What it tests:** Whether you manage cost per task rather than per call.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I set a budget per session and per task, cap steps, and terminate early when the agent is not making progress. I route simple steps to smaller models, trim context, cache repeated prefixes and avoid unnecessary tool calls. The metric that matters is cost per completed task, not cost per call, because a cheap but unreliable agent is expensive once retries and failures are counted. I add per-feature dashboards and alerts so a cost spike shows up in hours, not at month end.

**Red-flag answers**

- Tracks cost per call instead of per task
- Sets no session budget caps
- Uses the largest model for every step

**Expect this follow-up:** Which steps would you move to a smaller model first?

</details>

<a id="q14"></a>

### 14. How do you make long-running agents resumable?

**Competency:** State & Resume | **Level:** Advanced

**What it tests:** Whether long runs survive crashes without duplicate actions.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I persist state after each meaningful step: the plan, completed actions, tool results and any pending decisions. Actions are idempotent, or carry a key, so replaying a step after a crash does not duplicate its side effects, such as sending an email twice. For long or critical workflows I use a durable execution engine that handles retries and resumes automatically. On restart the agent loads its checkpoint and continues, not starts over. I test this by killing runs deliberately at different points.

**Red-flag answers**

- Restarts the whole task after a crash
- Makes actions non-idempotent
- Saves no checkpoints

**Expect this follow-up:** A payment step ran twice after a resume. What design flaw caused that?

</details>

<a id="q15"></a>

### 15. How should an agent handle tool failures?

**Competency:** Tool Errors | **Level:** Practitioner

**What it tests:** Whether failures become recoverable, structured signals.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I want tool errors to be structured and informative: what failed, whether it is retryable, and what the agent might change. Transient failures such as timeouts get retries with backoff, while validation errors go back to the model so it can correct the arguments. Retries have a hard limit, after which the agent escalates or reports the failure clearly rather than looping. I log every failure with context, because patterns in tool errors usually point to a tool that needs better design or documentation.

**Red-flag answers**

- Returns raw stack traces to the model
- Retries forever
- Has no escalation after limits

**Expect this follow-up:** How do you tell a transient failure from a tool bug?

</details>

<a id="q16"></a>

### 16. How do you choose an agent framework?

**Competency:** Frameworks | **Level:** Foundation

**What it tests:** Whether you choose tooling on control and observability.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I evaluate frameworks on how much control they give over the flow, how good the observability and state handling are, how well they fit our stack, and how much lock-in they create. Heavy frameworks can hide what is happening, which makes debugging and evaluation harder. For simple needs, plain code with a model SDK is often clearer and more maintainable. I prototype the real task in the top candidates, and I keep the model and tool layers behind interfaces so switching later stays possible.

**Red-flag answers**

- Picks the most popular framework
- Ignores observability and lock-in
- Cannot describe the plain-code alternative

**Expect this follow-up:** When would you drop the framework and write plain code?

</details>

<a id="q17"></a>

### 17. How do you handle tasks that take hours or many steps?

**Competency:** Long Tasks | **Level:** Practitioner

**What it tests:** Whether you design for checkpoints and partial results.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I break long tasks into checkpointed subtasks with clear outputs, persist progress and report status so the user is not left waiting in the dark. I set timeouts and review points where a human can redirect the work. Recovery is designed in: if the run stops at step nine of fifteen, the first eight steps' results are kept and useful. I also manage context across the run by summarising finished stages. Long tasks fail in the middle, so I plan for partial success rather than assuming completion.

**Red-flag answers**

- Runs one giant uninterrupted loop
- Gives the user no progress updates
- Loses partial results on failure

**Expect this follow-up:** The user comes back after two hours. What should they see?

</details>

<a id="q18"></a>

### 18. How do you give agents access to user accounts safely?

**Competency:** Delegated Access | **Level:** Advanced

**What it tests:** Whether agents act with scoped, revocable user permissions.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I use delegated access with scoped, short-lived credentials, typically through OAuth, so the agent acts with the user's permissions and no more. It never holds broad standing credentials. Every action is logged with who, what and when, and users can review what the agent did and revoke access at any time. Sensitive actions need explicit confirmation. I also separate read and write scopes and request the minimum needed. The principle is that the agent should never be able to do more than the user could do themselves.

**Red-flag answers**

- Shares the user's password with the agent
- Uses long-lived broad tokens
- Gives users no way to revoke access

**Expect this follow-up:** The user revokes access mid-run. What should happen?

</details>

<a id="q19"></a>

### 19. How do you safely let an agent execute code?

**Competency:** Code Sandbox | **Level:** Advanced

**What it tests:** Whether you isolate untrusted code execution properly.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I run agent-generated code in isolated, disposable environments such as containers or microVMs, with no secrets, restricted or no network access, limited file access, and strict CPU, memory and time limits. Each run starts clean so nothing persists between users. The output is treated as untrusted, since the code may have been influenced by injected content. I log what was executed. If the agent needs external access, it goes through a narrow, audited interface rather than open network access from the sandbox.

**Red-flag answers**

- Runs code on the host machine
- Leaves secrets in the environment
- Sets no network, time or resource limits

**Expect this follow-up:** The generated code tries to reach the internet. What do you want to happen?

</details>

<a id="q20"></a>

### 20. Agent context grows with every step. How do you manage it?

**Competency:** Context Growth | **Level:** Practitioner

**What it tests:** Whether you keep context compact without losing accuracy.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Context grows with every step and eventually slows the agent and reduces accuracy. I summarise or drop old tool results once they are no longer needed, keep a compact structured state of goals and decisions, and retrieve details on demand instead of holding everything. Noisy subtasks such as long searches can go to a sub-agent that returns only a summary. I track context size against accuracy on my evals to find where quality starts to degrade, and I set a budget for it.

**Red-flag answers**

- Keeps every tool result forever
- Ignores accuracy loss from long context
- Has no summarisation strategy

**Expect this follow-up:** What do you drop first when context is full, and how do you know it's safe?

</details>

<a id="q21"></a>

### 21. What is agent-to-agent communication and when do you need it?

**Competency:** A2A | **Level:** Advanced

**What it tests:** Whether you know when agent interoperability needs identity checks.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Agent-to-agent communication lets agents in different systems discover each other's capabilities and delegate tasks through standard protocols, rather than one team hard-coding every integration. I need it when capabilities live in separate services or organisations, for example a travel agent delegating to an airline's agent. It brings requirements I do not compromise on: strong identity, authentication, scoped permissions, audit trails and clear handling of what data crosses the boundary. Inside a single system, ordinary function calls are simpler and safer.

**Red-flag answers**

- Says agent-to-agent is the same as function calling
- Ignores identity and permission checks between agents
- Adds it when one service would do

**Expect this follow-up:** Another company's agent asks yours to act. How do you authenticate and limit it?

</details>

<a id="q22"></a>

### 22. Which metrics show whether an agent is production-ready?

**Competency:** Reliability Metrics | **Level:** Practitioner

**What it tests:** Whether readiness means stable performance across many runs.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

One good demo proves nothing, so I look at stable behaviour across many runs. Key metrics are task success rate, error and escalation rates, cost and latency percentiles, guardrail triggers, and how often users correct or abandon the agent. I break these down by scenario type to find weak areas. I also check trends over time and after each model or prompt change. Production readiness means the numbers are consistently good and I know how the agent fails, not just that it can succeed.

**Red-flag answers**

- Points to one good demo
- Reports only success rate
- Has no view on variance across runs

**Expect this follow-up:** What success rate would you require, and over how many runs?

</details>

<a id="q23"></a>

### 23. How do you test agents whose behaviour varies run to run?

**Competency:** Non-determinism | **Level:** Practitioner

**What it tests:** Whether you test variable behaviour statistically.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I accept variability and test for it. Each scenario runs many times and I report pass rates against a threshold. Where possible I use fixed seeds and mocked tools so I can isolate the model's behaviour from the environment. Assertions target outcomes and constraints, such as the right record updated and no forbidden action taken, not exact wording. I keep a set of scenarios that must always pass, and track flaky ones separately, since flakiness is itself a signal that the design or prompts are fragile.

**Red-flag answers**

- Tests each scenario once
- Asserts on exact wording
- Ignores tool mocking

**Expect this follow-up:** A scenario passes 7 of 10 times. Is it fixed?

</details>

<a id="q24"></a>

### 24. How should an agent handle an ambiguous goal?

**Competency:** Clarification | **Level:** Foundation

**What it tests:** Whether you balance asking against guessing by risk.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I weigh the cost of a wrong guess. If acting on a bad assumption is expensive or irreversible, the agent asks a short, specific clarifying question. If the cost is low, it states its assumptions and proceeds, so the user can correct it. Over-asking is a real failure mode that frustrates users, so I test for it as well as for under-asking. Good clarifying questions offer options rather than open-ended prompts, and the agent remembers the answers for the rest of the task.

**Red-flag answers**

- Always asks clarifying questions
- Never asks and guesses silently
- Doesn't weigh the cost of a wrong guess

**Expect this follow-up:** How would you test that it isn't over-asking?

</details>

<a id="q25"></a>

### 25. How do you roll out a new agent to users safely?

**Competency:** Rollout | **Level:** Practitioner

**What it tests:** Whether you stage launches with gates and a kill switch.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I roll out in stages: internal testing first, then a limited beta with tight permissions and close monitoring, then gradual expansion. Each stage has explicit success and safety criteria that must be met before moving on, such as task success rate, escalation rate and no serious incidents. Throughout there is a kill switch and a fallback to the previous process. I gather user feedback and review traces of failures at every stage. Expanding permissions comes last, after the agent has earned trust on smaller ones.

**Red-flag answers**

- Launches to everyone at once
- Has no kill switch
- Sets no success or safety criteria per stage

**Expect this follow-up:** What would make you roll back during the limited beta?

</details>

<a id="q26"></a>

### 26. How do you write the system prompt for an agent so its behaviour stays predictable?

**Competency:** Prompt Design | **Level:** Practitioner

**What it tests:** Whether you give an agent goals, boundaries and stop conditions rather than a wall of instructions.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I state the goal, the agent's scope, the tools available and when to use each, the boundaries it must not cross, and how to know it is done. I use short, unambiguous rules and put critical constraints where they are least likely to be missed. I include a few worked examples of good behaviour, including when to escalate. Then I test against tricky scenarios and revise from traces. Long prompts full of exceptions usually signal a design problem that belongs in tools or code, not text.

**Red-flag answers**

- Writes a long prompt of exceptions
- Gives no stop or escalation condition
- Never tests it against adversarial scenarios

**Expect this follow-up:** The agent ignores one rule in a long prompt. What do you do?

</details>

<a id="q27"></a>

### 27. Your agent passes its evals but users say it is unreliable. What could explain the gap?

**Competency:** Evaluation | **Level:** Advanced

**What it tests:** Whether you question how representative your evals are.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

The eval set probably does not match real usage. Real users phrase things differently, ask ambiguous things, chain tasks and hit tool failures that a clean test environment never produces. I would sample production traces, cluster the failures, and add those cases to the evals. I would also check whether the metrics reward the right outcome, since a task can be technically completed while the user is unhappy. Finally I would look at variance: a system that passes once may fail on repeated runs.

**Red-flag answers**

- Assumes the users are wrong
- Adds more of the same easy tests
- Ignores run-to-run variance

**Expect this follow-up:** How would you find the failure types that your evals do not currently cover?

</details>

<a id="q28"></a>

### 28. An agent can read email and also send it. What risks does that combination create, and how do you reduce them?

**Competency:** Security | **Level:** Advanced

**What it tests:** Whether you recognise the danger of combining untrusted input with powerful actions.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Reading untrusted email while holding the ability to send is a classic injection risk: a crafted message could instruct the agent to forward sensitive data. I reduce it by separating capabilities so content read from untrusted sources cannot directly trigger sending, requiring human approval for outbound messages, restricting recipients to allow-lists and stripping instruction-like content. I also log every action and test with malicious emails. The principle is to break the chain between untrusted input and sensitive action.

**Red-flag answers**

- Says the prompt tells it to ignore instructions
- Gives the agent broad send permissions
- Does no adversarial testing

**Expect this follow-up:** What would you do if the business insists on fully automatic sending?

</details>

<a id="q29"></a>

### 29. A user asks the agent to complete a task that will take 20 minutes. How do you design the experience?

**Competency:** Trade-offs | **Level:** Practitioner

**What it tests:** Whether you design for asynchronous work, feedback and interruption.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I make it asynchronous. The agent acknowledges the task, states what it will do and how long it may take, and runs in the background with visible progress. The user can leave and return, get a notification on completion, and interrupt or redirect midway. Checkpoints and review points reduce the risk of wasted work, and the result includes what was done and what was skipped. A blocking chat window for 20 minutes is a poor experience and makes failures more painful.

**Red-flag answers**

- Keeps the user blocked on a spinner
- Offers no way to cancel or redirect
- Gives no summary of what was done

**Expect this follow-up:** The agent finishes 80% and then fails. What does the user see?

</details>

<a id="q30"></a>

### 30. Tell me about an agent behaviour that surprised you in testing. How did you respond?

**Competency:** Behavioural | **Level:** Advanced

**What it tests:** Whether you investigate surprises systematically instead of patching symptoms.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A good answer describes a concrete surprise, such as an agent taking an unexpected shortcut or using a tool in a way nobody designed. I would explain how I found it through trace review, what caused it, often an ambiguous goal or a permissive tool, and the fix. That fix should be structural: tighter tool scope, a clearer stop condition or a new guardrail, plus a regression test. The learning is that surprises are information about the design, not just bugs to hide.

**Red-flag answers**

- Patches the symptom in the prompt only
- Cannot describe a specific example
- Adds no regression test

**Expect this follow-up:** How did you check the fix did not create a different surprise?

</details>

---

Prefer to practise with a write-first answer box? The same scenarios are in the [Agentic AI Engineer interview simulator](https://aidevdayindia.org/interview-questions/agentic-ai-engineer-interview-questions.html). Spotted a wrong or outdated answer? [Open a correction issue](https://github.com/ayushbishtdev/ai-engineering-interview-questions/issues/new?template=correction.md).
