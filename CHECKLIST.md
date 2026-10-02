# Checklist: answers to avoid, by role

Use this before a mock or real interview. Each box is a red-flag answer taken from the model answers in `questions/`. Tick a box when you can say what you would do instead. IDs match [CHEATSHEET.md](CHEATSHEET.md).

## AI Engineer (Prompt & Context Engineering)

Full answers: [questions/01-ai-engineer.md](questions/01-ai-engineer.md)

**AIE-1** How do you structure a production prompt so it stays reliable as requirements change?

- [ ] Avoid: Writes one long unstructured prompt
- [ ] Avoid: Doesn't version prompts
- [ ] Avoid: Changes prompts without running evals
- [ ] Ready for the follow-up: A prompt fix helps one case and breaks another. How do you prevent that?

**AIE-2** What is context engineering and how does it differ from writing prompts?

- [ ] Avoid: Treats it as just better prompt wording
- [ ] Avoid: Sends all retrieved text unfiltered
- [ ] Avoid: Ignores context order and size
- [ ] Ready for the follow-up: What would you cut first when the context is too long?

**AIE-3** Your RAG answers are wrong even though the right document exists. How do you debug it?

- [ ] Avoid: Changes the prompt before checking retrieval
- [ ] Avoid: Blames the model by default
- [ ] Avoid: Has no retrieval metrics
- [ ] Ready for the follow-up: The right chunk is retrieved but ignored. What next?

**AIE-4** How do you reduce hallucinations in a customer-facing assistant?

- [ ] Avoid: Says a stricter prompt solves it
- [ ] Avoid: Never allows 'I don't know'
- [ ] Avoid: Tracks no hallucination rate on an eval set
- [ ] Ready for the follow-up: How do you decide when to route to a human?

**AIE-5** How do you get reliable structured output from an LLM?

- [ ] Avoid: Asks the model politely for JSON
- [ ] Avoid: Does no schema validation
- [ ] Avoid: Retries blindly without the error
- [ ] Ready for the follow-up: The schema is complex and fails often. What do you change?

**AIE-6** How do you choose a model for a new feature?

- [ ] Avoid: Picks the newest or biggest model
- [ ] Avoid: Relies on public benchmarks
- [ ] Avoid: Has no fallback model
- [ ] Ready for the follow-up: The cheaper model is 3% worse. How do you decide?

**AIE-7** When would you use a long context window instead of retrieval?

- [ ] Avoid: Says long context replaces retrieval
- [ ] Avoid: Ignores cost per query
- [ ] Avoid: Doesn't test middle-of-context recall
- [ ] Ready for the follow-up: At what corpus size would you switch to retrieval?

**AIE-8** Your token bill doubled after a launch. What do you check first?

- [ ] Avoid: Blames traffic alone
- [ ] Avoid: Has no per-feature cost visibility
- [ ] Avoid: Cuts quality first
- [ ] Ready for the follow-up: Context per request grew 40%. Where would you look?

**AIE-9** When do few-shot examples help, and when do they hurt?

- [ ] Avoid: Adds many examples by default
- [ ] Avoid: Uses unrepresentative examples
- [ ] Avoid: Never tests with and without
- [ ] Ready for the follow-up: The model copies your example too literally. What do you do?

**AIE-10** How do you defend an LLM app against prompt injection?

- [ ] Avoid: Relies on 'ignore malicious instructions' in the prompt
- [ ] Avoid: Trusts retrieved text as instructions
- [ ] Avoid: Gives tools broad permissions
- [ ] Ready for the follow-up: How would you test your defences before launch?

**AIE-11** How do you decide on a chunking strategy for documents?

- [ ] Avoid: Uses one fixed chunk size everywhere
- [ ] Avoid: Ignores headings and tables
- [ ] Avoid: Has no retrieval metrics on real questions
- [ ] Ready for the follow-up: A table gets split across chunks. How do you handle it?

**AIE-12** How do you choose an embedding model and vector store?

- [ ] Avoid: Picks the top leaderboard model
- [ ] Avoid: Doesn't test on their own data
- [ ] Avoid: Ignores filtering and hybrid support
- [ ] Ready for the follow-up: Retrieval is good in English but poor in Hindi. What do you check?

**AIE-13** Why combine keyword and vector search?

- [ ] Avoid: Says vectors alone are enough
- [ ] Avoid: Doesn't know about exact-term failures
- [ ] Avoid: Adds no reranker
- [ ] Ready for the follow-up: Users search by order ID and get nothing. Why, and what's the fix?

**AIE-14** How do you make function calling reliable?

- [ ] Avoid: Writes vague function descriptions
- [ ] Avoid: Does no argument validation
- [ ] Avoid: Allows unlimited retries
- [ ] Ready for the follow-up: The model calls a function with an invalid argument. What happens next?

**AIE-15** How do you evaluate whether a prompt change is actually better?

- [ ] Avoid: Judges by a few examples
- [ ] Avoid: Reports only averages
- [ ] Avoid: Ships without a canary
- [ ] Ready for the follow-up: The new prompt is better overall but worse for one segment. What do you do?

**AIE-16** Where can caching reduce cost and latency in an LLM app?

- [ ] Avoid: Caches everything
- [ ] Avoid: Ignores privacy and staleness
- [ ] Avoid: Doesn't know prefix caching
- [ ] Ready for the follow-up: What would you never put in a semantic cache?

**AIE-17** When is fine-tuning worth it over prompting?

- [ ] Avoid: Fine-tunes before trying prompting
- [ ] Avoid: Has no quality labelled data
- [ ] Avoid: Cannot state the gap fine-tuning would close
- [ ] Ready for the follow-up: What evidence would convince you fine-tuning is needed?

**AIE-18** How do you handle Indian languages in an LLM feature?

- [ ] Avoid: Assumes English quality carries over
- [ ] Avoid: Ignores code-mixing and transliteration
- [ ] Avoid: Has no native-speaker evaluation
- [ ] Ready for the follow-up: Users type Hindi in Roman script. What breaks and how do you handle it?

**AIE-19** How does streaming change the user experience of an LLM feature?

- [ ] Avoid: Says streaming makes it faster overall
- [ ] Avoid: Ignores validation of partial output
- [ ] Avoid: Doesn't handle cancellation
- [ ] Ready for the follow-up: Safety checks need the full response. How do you stream anyway?

**AIE-20** How do you get more consistent outputs from an LLM?

- [ ] Avoid: Says temperature zero makes it deterministic
- [ ] Avoid: Adds no validation of outputs
- [ ] Avoid: Ignores structured output
- [ ] Ready for the follow-up: The output still varies at temperature zero. Why?

**AIE-21** How do you handle personal data in prompts?

- [ ] Avoid: Sends raw personal data to any provider
- [ ] Avoid: Logs full prompts indefinitely
- [ ] Avoid: Has no data-flow map
- [ ] Ready for the follow-up: Which fields would you redact before the model call?

**AIE-22** How do you manage long conversations within context limits?

- [ ] Avoid: Sends the entire history every turn
- [ ] Avoid: Loses key facts when summarising
- [ ] Avoid: Never tests summarisation
- [ ] Ready for the follow-up: The user's name is forgotten after summarisation. How do you prevent it?

**AIE-23** Product gives you a vague requirement for an AI feature. What do you do?

- [ ] Avoid: Starts building without clarifying
- [ ] Avoid: Waits for a perfect spec
- [ ] Avoid: Doesn't show concrete outputs
- [ ] Ready for the follow-up: The stakeholder still can't say what 'good' means. What do you do?

**AIE-24** Outputs are inconsistent across users. How do you investigate?

- [ ] Avoid: Changes several variables at once
- [ ] Avoid: Doesn't compare traces
- [ ] Avoid: Has no hypothesis
- [ ] Ready for the follow-up: What is the first thing you record in a trace so you can compare users?

**AIE-25** A provider deprecates the model you depend on. How do you prepare?

- [ ] Avoid: Notices only at the deadline
- [ ] Avoid: Has no abstraction or eval suite
- [ ] Avoid: Switches all traffic at once
- [ ] Ready for the follow-up: The replacement model behaves differently on your prompts. What do you do?

**AIE-26** Your AI feature has good answers but a p95 latency of twelve seconds. How do you bring it down?

- [ ] Avoid: Only proposes a faster model
- [ ] Avoid: Measures average latency, not p95
- [ ] Avoid: Has no per-stage timing
- [ ] Ready for the follow-up: Streaming is on and users still complain. What else could be slow?

**AIE-27** When is a reranker worth the extra latency and cost?

- [ ] Avoid: Adds a reranker without measuring
- [ ] Avoid: Ignores the added latency
- [ ] Avoid: Reranks a huge candidate list
- [ ] Ready for the follow-up: Your reranker adds 400 ms. Product says it is too slow. What are your options?

**AIE-28** You are building a RAG assistant and have no labelled data. How do you create an eval set?

- [ ] Avoid: Uses only unreviewed synthetic questions
- [ ] Avoid: Tunes on the same set they report on
- [ ] Avoid: Includes no unanswerable questions
- [ ] Ready for the follow-up: How do you stop the synthetic questions from being too easy?

**AIE-29** When would you use a reasoning model instead of a standard model, and what does it cost you?

- [ ] Avoid: Uses the reasoning model for everything
- [ ] Avoid: Ignores latency and token cost
- [ ] Avoid: Never compares against a standard model on their eval
- [ ] Ready for the follow-up: How would you decide which requests get routed to the reasoning model?

**AIE-30** Tell me about an AI feature you built that did not work in production. What did you do?

- [ ] Avoid: Blames the model or the users
- [ ] Avoid: Describes a success dressed up as a failure
- [ ] Avoid: Cannot say what changed afterwards
- [ ] Ready for the follow-up: What would you have needed to see before launch to catch it?

## Agentic AI Engineer

Full answers: [questions/02-agentic-ai-engineer.md](questions/02-agentic-ai-engineer.md)

**AGT-1** When should you use an agent instead of a fixed workflow?

- [ ] Avoid: Says agents are always better than workflows
- [ ] Avoid: Cannot explain when a fixed workflow is cheaper and easier to test
- [ ] Avoid: Adds autonomy everywhere from day one
- [ ] Ready for the follow-up: Give a task where you would deliberately choose a workflow over an agent.

**AGT-2** How do you design tools so an agent uses them correctly?

- [ ] Avoid: Builds many overlapping tools
- [ ] Avoid: Uses vague names and descriptions
- [ ] Avoid: Does no tool-selection testing
- [ ] Ready for the follow-up: The agent keeps picking the wrong one of two similar tools. What do you change?

**AGT-3** What problem does the Model Context Protocol solve?

- [ ] Avoid: Describes MCP as just another API wrapper
- [ ] Avoid: Trusts tool descriptions from any server
- [ ] Avoid: Ignores server permissions
- [ ] Ready for the follow-up: How would you vet a third-party MCP server before connecting it?

**AGT-4** How do you stop an agent from taking harmful actions?

- [ ] Avoid: Relies on the prompt saying 'don't do harmful things'
- [ ] Avoid: Gives agents broad admin credentials
- [ ] Avoid: Requires no approval for irreversible actions
- [ ] Ready for the follow-up: Which action would you never let an agent take without human approval?

**AGT-5** How do you handle memory in a long-running agent?

- [ ] Avoid: Stuffs full history into context forever
- [ ] Avoid: Gives users no way to inspect or delete memories
- [ ] Avoid: Never tests stale or conflicting memory
- [ ] Ready for the follow-up: A user says the agent remembers something wrong. How do you fix it?

**AGT-6** An agent keeps looping and burning tokens. What do you do?

- [ ] Avoid: Only raises the token limit
- [ ] Avoid: Sets no step or budget caps
- [ ] Avoid: Doesn't read traces
- [ ] Ready for the follow-up: How would you detect a loop automatically in production?

**AGT-7** When are multi-agent systems worth the extra complexity?

- [ ] Avoid: Uses multi-agent by default
- [ ] Avoid: Cannot show coordination improved results
- [ ] Avoid: Leaves handoffs implicit
- [ ] Ready for the follow-up: How would you prove a multi-agent design beats a single agent on your task?

**AGT-8** How do you debug a wrong agent decision after the fact?

- [ ] Avoid: Cannot reproduce the failed run
- [ ] Avoid: Logs only final outputs
- [ ] Avoid: Doesn't turn failures into tests
- [ ] Ready for the follow-up: What exactly is in a trace that lets you replay a run?

**AGT-9** How do agents plan, and when do you choose plan-then-execute over ReAct?

- [ ] Avoid: Treats ReAct and plan-then-execute as the same thing
- [ ] Avoid: Never replans on failure
- [ ] Avoid: Offers no reviewable plan for structured tasks
- [ ] Ready for the follow-up: The plan was fine but step three failed. What should the agent do?

**AGT-10** How do you design human-in-the-loop approvals for an agent?

- [ ] Avoid: Asks for approval on every action
- [ ] Avoid: Shows reviewers no context or impact
- [ ] Avoid: Never measures override rates
- [ ] Ready for the follow-up: Reviewers approve 99% of requests without reading them. What do you do?

**AGT-11** How can tool outputs be used to attack an agent, and what do you do?

- [ ] Avoid: Trusts retrieved content as instructions
- [ ] Avoid: Relies on a single filter
- [ ] Avoid: Doesn't monitor for unexpected tool calls
- [ ] Ready for the follow-up: A web page tells the agent to email customer data elsewhere. What stops it?

**AGT-12** How do you evaluate an agent end to end?

- [ ] Avoid: Judges only by the final answer
- [ ] Avoid: Tests only on happy-path demos
- [ ] Avoid: Leaves out cost and latency
- [ ] Ready for the follow-up: The agent succeeds but takes 40 steps. Is that a pass?

**AGT-13** How do you keep agent session costs predictable?

- [ ] Avoid: Tracks cost per call instead of per task
- [ ] Avoid: Sets no session budget caps
- [ ] Avoid: Uses the largest model for every step
- [ ] Ready for the follow-up: Which steps would you move to a smaller model first?

**AGT-14** How do you make long-running agents resumable?

- [ ] Avoid: Restarts the whole task after a crash
- [ ] Avoid: Makes actions non-idempotent
- [ ] Avoid: Saves no checkpoints
- [ ] Ready for the follow-up: A payment step ran twice after a resume. What design flaw caused that?

**AGT-15** How should an agent handle tool failures?

- [ ] Avoid: Returns raw stack traces to the model
- [ ] Avoid: Retries forever
- [ ] Avoid: Has no escalation after limits
- [ ] Ready for the follow-up: How do you tell a transient failure from a tool bug?

**AGT-16** How do you choose an agent framework?

- [ ] Avoid: Picks the most popular framework
- [ ] Avoid: Ignores observability and lock-in
- [ ] Avoid: Cannot describe the plain-code alternative
- [ ] Ready for the follow-up: When would you drop the framework and write plain code?

**AGT-17** How do you handle tasks that take hours or many steps?

- [ ] Avoid: Runs one giant uninterrupted loop
- [ ] Avoid: Gives the user no progress updates
- [ ] Avoid: Loses partial results on failure
- [ ] Ready for the follow-up: The user comes back after two hours. What should they see?

**AGT-18** How do you give agents access to user accounts safely?

- [ ] Avoid: Shares the user's password with the agent
- [ ] Avoid: Uses long-lived broad tokens
- [ ] Avoid: Gives users no way to revoke access
- [ ] Ready for the follow-up: The user revokes access mid-run. What should happen?

**AGT-19** How do you safely let an agent execute code?

- [ ] Avoid: Runs code on the host machine
- [ ] Avoid: Leaves secrets in the environment
- [ ] Avoid: Sets no network, time or resource limits
- [ ] Ready for the follow-up: The generated code tries to reach the internet. What do you want to happen?

**AGT-20** Agent context grows with every step. How do you manage it?

- [ ] Avoid: Keeps every tool result forever
- [ ] Avoid: Ignores accuracy loss from long context
- [ ] Avoid: Has no summarisation strategy
- [ ] Ready for the follow-up: What do you drop first when context is full, and how do you know it's safe?

**AGT-21** What is agent-to-agent communication and when do you need it?

- [ ] Avoid: Says agent-to-agent is the same as function calling
- [ ] Avoid: Ignores identity and permission checks between agents
- [ ] Avoid: Adds it when one service would do
- [ ] Ready for the follow-up: Another company's agent asks yours to act. How do you authenticate and limit it?

**AGT-22** Which metrics show whether an agent is production-ready?

- [ ] Avoid: Points to one good demo
- [ ] Avoid: Reports only success rate
- [ ] Avoid: Has no view on variance across runs
- [ ] Ready for the follow-up: What success rate would you require, and over how many runs?

**AGT-23** How do you test agents whose behaviour varies run to run?

- [ ] Avoid: Tests each scenario once
- [ ] Avoid: Asserts on exact wording
- [ ] Avoid: Ignores tool mocking
- [ ] Ready for the follow-up: A scenario passes 7 of 10 times. Is it fixed?

**AGT-24** How should an agent handle an ambiguous goal?

- [ ] Avoid: Always asks clarifying questions
- [ ] Avoid: Never asks and guesses silently
- [ ] Avoid: Doesn't weigh the cost of a wrong guess
- [ ] Ready for the follow-up: How would you test that it isn't over-asking?

**AGT-25** How do you roll out a new agent to users safely?

- [ ] Avoid: Launches to everyone at once
- [ ] Avoid: Has no kill switch
- [ ] Avoid: Sets no success or safety criteria per stage
- [ ] Ready for the follow-up: What would make you roll back during the limited beta?

**AGT-26** How do you write the system prompt for an agent so its behaviour stays predictable?

- [ ] Avoid: Writes a long prompt of exceptions
- [ ] Avoid: Gives no stop or escalation condition
- [ ] Avoid: Never tests it against adversarial scenarios
- [ ] Ready for the follow-up: The agent ignores one rule in a long prompt. What do you do?

**AGT-27** Your agent passes its evals but users say it is unreliable. What could explain the gap?

- [ ] Avoid: Assumes the users are wrong
- [ ] Avoid: Adds more of the same easy tests
- [ ] Avoid: Ignores run-to-run variance
- [ ] Ready for the follow-up: How would you find the failure types that your evals do not currently cover?

**AGT-28** An agent can read email and also send it. What risks does that combination create, and how do you reduce them?

- [ ] Avoid: Says the prompt tells it to ignore instructions
- [ ] Avoid: Gives the agent broad send permissions
- [ ] Avoid: Does no adversarial testing
- [ ] Ready for the follow-up: What would you do if the business insists on fully automatic sending?

**AGT-29** A user asks the agent to complete a task that will take 20 minutes. How do you design the experience?

- [ ] Avoid: Keeps the user blocked on a spinner
- [ ] Avoid: Offers no way to cancel or redirect
- [ ] Avoid: Gives no summary of what was done
- [ ] Ready for the follow-up: The agent finishes 80% and then fails. What does the user see?

**AGT-30** Tell me about an agent behaviour that surprised you in testing. How did you respond?

- [ ] Avoid: Patches the symptom in the prompt only
- [ ] Avoid: Cannot describe a specific example
- [ ] Avoid: Adds no regression test
- [ ] Ready for the follow-up: How did you check the fix did not create a different surprise?

## AI Evaluation Engineer

Full answers: [questions/03-ai-evaluation-engineer.md](questions/03-ai-evaluation-engineer.md)

**EVAL-1** How do you build an eval set for a new LLM feature?

- [ ] Avoid: Uses only easy or synthetic examples
- [ ] Avoid: Keeps no held-out set
- [ ] Avoid: Has no labelled answers or rubrics
- [ ] Ready for the follow-up: How do you know your eval set covers real usage?

**EVAL-2** What are the risks of using an LLM as a judge, and how do you mitigate them?

- [ ] Avoid: Trusts the judge without calibration
- [ ] Avoid: Ignores position and length bias
- [ ] Avoid: Uses the same model to generate and judge
- [ ] Ready for the follow-up: Judge and human agree only 65% of the time. What do you do?

**EVAL-3** How do you choose metrics for a summarisation or Q&A system?

- [ ] Avoid: Reports one average metric
- [ ] Avoid: Uses BLEU or ROUGE alone
- [ ] Avoid: Ignores factuality
- [ ] Ready for the follow-up: Summaries score well but users say they miss key points. What's wrong?

**EVAL-4** How do you stop prompt or model changes from silently breaking quality?

- [ ] Avoid: Tests manually before release
- [ ] Avoid: Sets no thresholds or baselines
- [ ] Avoid: Ignores segment-level regressions
- [ ] Ready for the follow-up: The overall score rose but one critical segment dropped. Do you ship?

**EVAL-5** How do you design a reliable human annotation process?

- [ ] Avoid: Skips guidelines and training
- [ ] Avoid: Uses a single annotator
- [ ] Avoid: Never measures agreement
- [ ] Ready for the follow-up: Raters keep disagreeing on one criterion. What do you fix?

**EVAL-6** How do offline evals and online metrics work together?

- [ ] Avoid: Relies on offline scores alone
- [ ] Avoid: Ignores online signals
- [ ] Avoid: Never checks that offline predicts online
- [ ] Ready for the follow-up: Offline scores improved but users are less satisfied. Why?

**EVAL-7** How would you evaluate a model for harmful or biased outputs?

- [ ] Avoid: Tests only obvious harmful prompts
- [ ] Avoid: Ignores group-level gaps
- [ ] Avoid: Doesn't re-test after fixes
- [ ] Ready for the follow-up: How do you decide the residual risk is acceptable?

**EVAL-8** A vendor claims state-of-the-art benchmark scores. Do you trust them?

- [ ] Avoid: Accepts the claim as fact
- [ ] Avoid: Ignores contamination
- [ ] Avoid: Doesn't test cost and latency
- [ ] Ready for the follow-up: The model wins on the vendor's benchmark and loses on yours. What do you report?

**EVAL-9** How do you keep a golden dataset useful over time?

- [ ] Avoid: Freezes the dataset
- [ ] Avoid: Never adds production failures
- [ ] Avoid: Doesn't review labels
- [ ] Ready for the follow-up: How often would you refresh it, and what triggers a change?

**EVAL-10** When is synthetic data appropriate for evals?

- [ ] Avoid: Uses synthetic data only
- [ ] Avoid: Lets the same model generate and grade
- [ ] Avoid: Doesn't validate samples by hand
- [ ] Ready for the follow-up: Where could synthetic data mislead you?

**EVAL-11** How do you evaluate a RAG system?

- [ ] Avoid: Evaluates only final answers
- [ ] Avoid: Doesn't separate retrieval from generation
- [ ] Avoid: Ignores faithfulness to sources
- [ ] Ready for the follow-up: Recall is high but answers are wrong. Where do you look next?

**EVAL-12** How do you evaluate multi-step agent trajectories?

- [ ] Avoid: Judges only the final outcome
- [ ] Avoid: Ignores unnecessary steps and unsafe actions
- [ ] Avoid: Runs on live systems
- [ ] Ready for the follow-up: Two agents succeed, one in 5 steps and one in 40. How do you compare them?

**EVAL-13** LLM eval scores fluctuate between runs. How do you draw reliable conclusions?

- [ ] Avoid: Concludes from small score differences
- [ ] Avoid: Runs each case once
- [ ] Avoid: Reports no confidence intervals
- [ ] Ready for the follow-up: How many runs would you do to trust a 2-point gain?

**EVAL-14** When do you use pairwise comparison instead of absolute scoring?

- [ ] Avoid: Uses absolute scores for everything
- [ ] Avoid: Doesn't know when pairwise helps
- [ ] Avoid: Ignores rater consistency
- [ ] Ready for the follow-up: Which method would you use to track quality over six months, and why?

**EVAL-15** What makes a good evaluation rubric?

- [ ] Avoid: Uses vague criteria like 'good quality'
- [ ] Avoid: Bundles accuracy and tone together
- [ ] Avoid: Never tests with several raters
- [ ] Ready for the follow-up: Write one criterion with score definitions for 'helpfulness'.

**EVAL-16** Your eval suite is slow and expensive. How do you fix it?

- [ ] Avoid: Runs the full suite on every change
- [ ] Avoid: Cuts cases at random
- [ ] Avoid: Uses cheaper judges without calibration
- [ ] Ready for the follow-up: Which tests go in the fast tier, and why?

**EVAL-17** How do you detect and avoid benchmark contamination?

- [ ] Avoid: Trusts public leaderboards
- [ ] Avoid: Keeps no private held-out set
- [ ] Avoid: Doesn't check for overlap
- [ ] Ready for the follow-up: How would you suspect a model has seen your test data?

**EVAL-18** How do you evaluate quality across languages?

- [ ] Avoid: Assumes English results transfer
- [ ] Avoid: Uses machine-translated tests only
- [ ] Avoid: Has no native reviewers
- [ ] Ready for the follow-up: Scores are lower in Tamil. How do you tell if it's the model or the test?

**EVAL-19** How do you evaluate open-ended tasks with no single right answer?

- [ ] Avoid: Insists on one right answer
- [ ] Avoid: Relies on exact match
- [ ] Avoid: Never checks the judge against humans
- [ ] Ready for the follow-up: How do you evaluate a creative-writing assistant?

**EVAL-20** How do you do error analysis on failing cases?

- [ ] Avoid: Reads a few failures anecdotally
- [ ] Avoid: Has no failure taxonomy
- [ ] Avoid: Doesn't rank by frequency and severity
- [ ] Ready for the follow-up: You have 200 failures. How do you start?

**EVAL-21** How do you report eval results to executives?

- [ ] Avoid: Sends raw score dumps
- [ ] Avoid: Gives no thresholds or recommendation
- [ ] Avoid: Hides failure categories
- [ ] Ready for the follow-up: What one sentence would you say to an executive about release readiness?

**EVAL-22** How do you structure a red-teaming exercise?

- [ ] Avoid: Runs a one-off jailbreak session
- [ ] Avoid: Has no threat model or harm categories
- [ ] Avoid: Lets findings skip the release gates
- [ ] Ready for the follow-up: How do you turn red-team findings into permanent tests?

**EVAL-23** How do you check whether a model's confidence can be trusted?

- [ ] Avoid: Takes model-stated confidence at face value
- [ ] Avoid: Uses no calibration plots
- [ ] Avoid: Doesn't use confidence for routing
- [ ] Ready for the follow-up: The model says 95% confident but is right 70% of the time. What do you do?

**EVAL-24** How do you A/B test an LLM feature?

- [ ] Avoid: Ends the test early on a good day
- [ ] Avoid: Has no guardrail metrics
- [ ] Avoid: Ignores cost and novelty effects
- [ ] Ready for the follow-up: The variant wins on clicks but complaints rise. What do you do?

**EVAL-25** How do you build an eval-driven culture in a team?

- [ ] Avoid: Runs evals only before big launches
- [ ] Avoid: Makes evals hard to run
- [ ] Avoid: Doesn't turn production bugs into tests
- [ ] Ready for the follow-up: How would you make evals part of the definition of done?

**EVAL-26** Your LLM judge and your human reviewers disagree on 30% of cases. What do you do?

- [ ] Avoid: Trusts the judge because it is cheaper
- [ ] Avoid: Discards the human labels
- [ ] Avoid: Never reads the disagreeing cases
- [ ] Ready for the follow-up: How much agreement would you require before letting the judge gate a release?

**EVAL-27** How do you monitor quality in production when you have no ground-truth labels?

- [ ] Avoid: Waits for customers to complain
- [ ] Avoid: Relies on a single proxy metric
- [ ] Avoid: Reviews no real samples
- [ ] Ready for the follow-up: Thumbs-down rates are flat but you suspect quality has fallen. How do you check?

**EVAL-28** How do you decide how large your eval set needs to be?

- [ ] Avoid: Picks a round number arbitrarily
- [ ] Avoid: Ignores per-segment counts
- [ ] Avoid: Values size over label quality
- [ ] Ready for the follow-up: Your set has 200 items and two versions differ by 2 points. What do you conclude?

**EVAL-29** What would you look for when choosing an evaluation framework or platform?

- [ ] Avoid: Picks the most popular tool by default
- [ ] Avoid: Ignores data privacy and export
- [ ] Avoid: Never prototypes on a real feature
- [ ] Ready for the follow-up: Would you build or buy for a team of five engineers? Why?

**EVAL-30** Tell me about a time an evaluation result changed a decision the team had already made.

- [ ] Avoid: Cannot give a specific case
- [ ] Avoid: Presents it as personal victory
- [ ] Avoid: Ignores the pushback
- [ ] Ready for the follow-up: How did you make sure the result was not just noise?

## Forward Deployed Engineer

Full answers: [questions/04-forward-deployed-engineer.md](questions/04-forward-deployed-engineer.md)

**FDE-1** What does a forward deployed engineer do that a regular engineer doesn't?

- [ ] Avoid: Describes it as regular engineering with travel
- [ ] Avoid: Ignores customer outcomes
- [ ] Avoid: Doesn't mention feeding learnings back to product
- [ ] Ready for the follow-up: Give an example of a customer learning that changed a product.

**FDE-2** A customer asks for 'an AI agent for everything'. How do you scope it?

- [ ] Avoid: Says yes to everything
- [ ] Avoid: Sets no success metrics
- [ ] Avoid: Doesn't define what is out of scope
- [ ] Ready for the follow-up: The customer insists on all use cases at once. What do you say?

**FDE-3** The customer's data is messy and locked in legacy systems. What do you do?

- [ ] Avoid: Waits for perfect data
- [ ] Avoid: Cleans everything up front
- [ ] Avoid: Ignores the customer's data owners
- [ ] Ready for the follow-up: How do you show value in two weeks with poor data?

**FDE-4** How do you build trust with sceptical stakeholders at a customer?

- [ ] Avoid: Argues with sceptics
- [ ] Avoid: Overpromises to win them over
- [ ] Avoid: Measures success in their own metrics, not the customer's
- [ ] Ready for the follow-up: A stakeholder openly says AI won't work here. What do you do?

**FDE-5** How do you turn customer-specific work into product improvements?

- [ ] Avoid: Ships every custom request into the product
- [ ] Avoid: Has no evidence across deployments
- [ ] Avoid: Doesn't separate one-offs from general needs
- [ ] Ready for the follow-up: How do you decide when a request deserves a product change?

**FDE-6** The customer's security team blocks your deployment. How do you respond?

- [ ] Avoid: Argues the security team is being difficult
- [ ] Avoid: Has no data-flow documentation
- [ ] Avoid: Offers no deployment options
- [ ] Ready for the follow-up: The security team asks for a private deployment. Can you do it, and how?

**FDE-7** How do you take a successful demo to production?

- [ ] Avoid: Ships the demo as-is
- [ ] Avoid: Adds no evals, monitoring or fallbacks
- [ ] Avoid: Ignores training and support
- [ ] Ready for the follow-up: What breaks first when a demo goes live?

**FDE-8** The customer keeps adding requests mid-pilot. What do you do?

- [ ] Avoid: Says yes to keep the customer happy
- [ ] Avoid: Refuses all new requests
- [ ] Avoid: Doesn't log or prioritise them
- [ ] Ready for the follow-up: The sponsor says the new request is critical. What do you do?

**FDE-9** How do you run discovery with a new customer?

- [ ] Avoid: Runs a feature-led questionnaire
- [ ] Avoid: Talks only to executives
- [ ] Avoid: Doesn't observe the real workflow
- [ ] Ready for the follow-up: What do you do in your first day on site?

**FDE-10** How do you design a demo that convinces a customer?

- [ ] Avoid: Shows a generic feature tour
- [ ] Avoid: Uses fake data
- [ ] Avoid: Hides failure cases
- [ ] Ready for the follow-up: The demo fails live. What do you do?

**FDE-11** Your executive sponsor leaves mid-project. What do you do?

- [ ] Avoid: Waits for a replacement to appear
- [ ] Avoid: Loses momentum
- [ ] Avoid: Doesn't document results so far
- [ ] Ready for the follow-up: The new sponsor doubts the project's value. What is your first meeting?

**FDE-12** Users aren't using the solution you delivered. What do you do?

- [ ] Avoid: Blames users for not adopting
- [ ] Avoid: Adds more features
- [ ] Avoid: Doesn't talk to users
- [ ] Ready for the follow-up: Users say they don't trust the output. What do you do?

**FDE-13** How do you integrate with legacy ERP or CRM systems?

- [ ] Avoid: Asks for write access on day one
- [ ] Avoid: Ignores their release cycles
- [ ] Avoid: Skips a sandbox
- [ ] Ready for the follow-up: The ERP has no API. What options do you consider?

**FDE-14** How do you set expectations about AI accuracy with a customer?

- [ ] Avoid: Promises 99% accuracy
- [ ] Avoid: Doesn't test on their data
- [ ] Avoid: Offers no fallback or review step
- [ ] Ready for the follow-up: Accuracy is 88% and they expected 95%. What do you do?

**FDE-15** How do you hand over a solution to the customer's team?

- [ ] Avoid: Hands over a repository and leaves
- [ ] Avoid: Provides no runbooks or training
- [ ] Avoid: Keeps sole ownership
- [ ] Ready for the follow-up: What must the customer's team be able to do on day one after handover?

**FDE-16** How do you show ROI to a customer's leadership?

- [ ] Avoid: Cites usage numbers only
- [ ] Avoid: Has no baseline
- [ ] Avoid: Hides assumptions
- [ ] Ready for the follow-up: Time saved is real but hard to convert to money. How do you present it?

**FDE-17** A pilot didn't meet its success criteria. How do you handle it?

- [ ] Avoid: Blames the customer or the data
- [ ] Avoid: Hides the results
- [ ] Avoid: Makes no recommendation
- [ ] Ready for the follow-up: The customer wants to stop entirely. What do you say?

**FDE-18** You support several customers with urgent requests. How do you prioritise?

- [ ] Avoid: Answers whoever shouts loudest
- [ ] Avoid: Says nothing about timelines
- [ ] Avoid: Doesn't involve the manager on conflicts
- [ ] Ready for the follow-up: Two customers have equal urgency. How do you decide?

**FDE-19** How do you work with sales without overpromising?

- [ ] Avoid: Lets sales define the scope
- [ ] Avoid: Skips early scoping calls
- [ ] Avoid: Documents no assumptions
- [ ] Ready for the follow-up: Sales already promised a date you can't meet. What do you do?

**FDE-20** Two customer departments want conflicting behaviour from the system. What do you do?

- [ ] Avoid: Picks the more senior department
- [ ] Avoid: Builds both behaviours with no discussion
- [ ] Avoid: Doesn't escalate
- [ ] Ready for the follow-up: The sponsor is unavailable. How do you move forward?

**FDE-21** A customer bug needs a product fix that engineering hasn't prioritised. How do you escalate?

- [ ] Avoid: Waits silently for engineering
- [ ] Avoid: Escalates emotionally
- [ ] Avoid: Offers no workaround
- [ ] Ready for the follow-up: What evidence would convince engineering to prioritise the bug?

**FDE-22** How do you train a customer's engineers to work with the solution?

- [ ] Avoid: Runs a slide-only session
- [ ] Avoid: Skips their environment
- [ ] Avoid: Doesn't check understanding
- [ ] Ready for the follow-up: How do you know the customer's engineers are ready to take over?

**FDE-23** A customer requires data to stay in a specific region. How do you respond?

- [ ] Avoid: Says it can't be done without checking
- [ ] Avoid: Ignores logs and backups
- [ ] Avoid: Doesn't document data flows
- [ ] Ready for the follow-up: The model provider has no region there. What do you offer?

**FDE-24** How do you balance fast prototyping with technical debt?

- [ ] Avoid: Ships the prototype as production
- [ ] Avoid: Sets no exit criteria
- [ ] Avoid: Never labels throwaway code
- [ ] Ready for the follow-up: How do you decide which prototype parts to rebuild?

**FDE-25** How do you deliver bad news to a customer?

- [ ] Avoid: Delays until forced to share
- [ ] Avoid: Blames others
- [ ] Avoid: Arrives with no options
- [ ] Ready for the follow-up: You caused the problem. How does the conversation change?

**FDE-26** A customer wants a fine-tuned model, but you think retrieval plus prompting would work. How do you handle the disagreement?

- [ ] Avoid: Dismisses their request outright
- [ ] Avoid: Argues without offering a test
- [ ] Avoid: Agrees to build something they doubt without evidence
- [ ] Ready for the follow-up: The test is inconclusive. What do you recommend?

**FDE-27** How do you explain a technical limitation to a non-technical executive?

- [ ] Avoid: Explains the internals at length
- [ ] Avoid: Hides the limitation to avoid friction
- [ ] Avoid: Offers no options or recommendation
- [ ] Ready for the follow-up: The executive says 'just make it work'. How do you respond?

**FDE-28** You are two weeks from a customer go-live and evals show the system misses the agreed accuracy threshold. What do you do?

- [ ] Avoid: Ships anyway and hopes
- [ ] Avoid: Quietly redefines the threshold
- [ ] Avoid: Tells the customer only at the deadline
- [ ] Ready for the follow-up: The sponsor insists on going live on time. What safeguards do you put in place?

**FDE-29** The customer wants to send confidential documents to a hosted model API. What questions do you ask?

- [ ] Avoid: Sends the data without checking terms
- [ ] Avoid: Ignores contractual obligations
- [ ] Avoid: Proposes no alternative if risk is high
- [ ] Ready for the follow-up: The provider's terms allow 30-day retention. The customer requires none. What now?

**FDE-30** Tell me about a deployment that went wrong at a customer site. What did you do and what did you change?

- [ ] Avoid: Blames the customer or a colleague
- [ ] Avoid: Describes an incident with no real impact
- [ ] Avoid: Cannot name what changed afterwards
- [ ] Ready for the follow-up: What would the customer say about how you handled it?

## Responsible AI / AI Governance Engineer

Full answers: [questions/05-responsible-ai-governance-engineer.md](questions/05-responsible-ai-governance-engineer.md)

**RAI-1** How do you assess the risk of a new AI use case?

- [ ] Avoid: Treats all use cases the same
- [ ] Avoid: Ignores reversibility and autonomy
- [ ] Avoid: Applies no tiered controls
- [ ] Ready for the follow-up: Classify a résumé-screening tool and an internal meeting summariser, and explain your reasoning.

**RAI-2** How do you keep systems aligned with rules like the EU AI Act and India's DPDP Act?

- [ ] Avoid: Says compliance is legal's job
- [ ] Avoid: Adds it at the end
- [ ] Avoid: Keeps no inventory or documentation
- [ ] Ready for the follow-up: A new regulation lands. How do you find which systems are affected?

**RAI-3** How do you test an AI system for bias?

- [ ] Avoid: Tests only overall accuracy
- [ ] Avoid: Doesn't define groups or metrics
- [ ] Avoid: Doesn't re-test after mitigation
- [ ] Ready for the follow-up: You find a 6-point gap for one group. What next?

**RAI-4** What documentation should accompany a deployed model?

- [ ] Avoid: Says a README is enough
- [ ] Avoid: Lists no limitations or prohibited uses
- [ ] Avoid: Gives no evaluation by segment
- [ ] Ready for the follow-up: Who reads the model card, and what do they need from it?

**RAI-5** How do you prevent sensitive data leaking through an LLM application?

- [ ] Avoid: Relies on the provider's promises
- [ ] Avoid: Ignores access control at retrieval
- [ ] Avoid: Keeps logs indefinitely
- [ ] Ready for the follow-up: How do you test for leakage before launch?

**RAI-6** How do you design meaningful human oversight?

- [ ] Avoid: Adds a human reviewer as a checkbox
- [ ] Avoid: Doesn't measure override rates
- [ ] Avoid: Gives reviewers no time or authority
- [ ] Ready for the follow-up: Reviewers approve 99% of outputs. Is oversight working?

**RAI-7** An AI system produced a harmful output publicly. What is your response?

- [ ] Avoid: Denies or delays
- [ ] Avoid: Skips logs and root cause
- [ ] Avoid: Does no governance review
- [ ] Ready for the follow-up: Who do you tell first, and what do you say?

**RAI-8** The business wants to launch despite unresolved fairness findings. What do you do?

- [ ] Avoid: Complies quietly
- [ ] Avoid: Refuses without alternatives
- [ ] Avoid: Doesn't document risk acceptance
- [ ] Ready for the follow-up: Leadership signs off on the risk. What do you still do?

**RAI-9** Why keep an inventory of AI systems, and what goes in it?

- [ ] Avoid: Keeps a spreadsheet nobody updates
- [ ] Avoid: Assigns no owner or risk tier
- [ ] Avoid: Cannot find shadow AI
- [ ] Ready for the follow-up: How would you discover AI systems that aren't in the inventory?

**RAI-10** How do you run an AI impact assessment?

- [ ] Avoid: Fills in a form once
- [ ] Avoid: Ignores affected groups
- [ ] Avoid: Never revisits after changes
- [ ] Ready for the follow-up: What triggers a reassessment?

**RAI-11** How do you approach explainability for different audiences?

- [ ] Avoid: Gives one explanation for all audiences
- [ ] Avoid: Confuses plausible with faithful
- [ ] Avoid: Ignores audit needs
- [ ] Ready for the follow-up: How do you check an explanation is faithful?

**RAI-12** Fairness metrics can conflict. How do you choose?

- [ ] Avoid: Picks a metric without context
- [ ] Avoid: Ignores the legal context
- [ ] Avoid: Doesn't quantify trade-offs
- [ ] Ready for the follow-up: Two fairness metrics can't both be met. Which do you choose, and why?

**RAI-13** How do you assess data provenance, consent and copyright for training or retrieval?

- [ ] Avoid: Ignores licences and consent
- [ ] Avoid: Keeps no lineage records
- [ ] Avoid: Trusts third-party data blindly
- [ ] Ready for the follow-up: A source's licence is unclear. What do you do?

**RAI-14** What do you check before adopting a third-party model or AI vendor?

- [ ] Avoid: Relies on the vendor's marketing
- [ ] Avoid: Ignores training on customer data
- [ ] Avoid: Leaves out exit terms
- [ ] Ready for the follow-up: The vendor won't share evaluation evidence. Do you proceed?

**RAI-15** How do you design safety testing before launch?

- [ ] Avoid: Tests only common cases
- [ ] Avoid: Sets no pass thresholds by risk tier
- [ ] Avoid: Requires no sign-off on residual risk
- [ ] Ready for the follow-up: The test fails one critical category. Who can approve a launch?

**RAI-16** How do you turn a responsible-AI policy into guardrails engineers can use?

- [ ] Avoid: Publishes a policy PDF only
- [ ] Avoid: Adds no code or pipeline checks
- [ ] Avoid: Offers principles with no concrete controls
- [ ] Ready for the follow-up: Turn 'be fair' into three checks an engineer can run.

**RAI-17** What should be logged to support AI audits?

- [ ] Avoid: Logs everything including personal data
- [ ] Avoid: Logs too little to audit
- [ ] Avoid: Lets logs be edited
- [ ] Ready for the follow-up: How do you keep logs useful without over-collecting?

**RAI-18** How do you set up an AI governance operating model?

- [ ] Avoid: Builds a slow committee
- [ ] Avoid: Applies the same review to all risks
- [ ] Avoid: Sets no owners or SLAs
- [ ] Ready for the follow-up: Low-risk teams say governance slows them down. What do you change?

**RAI-19** How do you embed governance into the delivery pipeline?

- [ ] Avoid: Reviews every release manually
- [ ] Avoid: Generates no automated evidence
- [ ] Avoid: Ties approvals to nothing about risk
- [ ] Ready for the follow-up: Which check would you automate first?

**RAI-20** How would you write a generative-AI acceptable-use policy for employees?

- [ ] Avoid: Writes a long legal policy
- [ ] Avoid: Doesn't say what data must never be entered
- [ ] Avoid: Offers no training
- [ ] Ready for the follow-up: An employee pastes customer data into a public tool. What now?

**RAI-21** Employees are using unapproved AI tools. How do you respond?

- [ ] Avoid: Bans tools and hopes
- [ ] Avoid: Punishes users
- [ ] Avoid: Doesn't ask why they use them
- [ ] Ready for the follow-up: What approved alternative would you offer first?

**RAI-22** What extra safeguards are needed when users may be children or vulnerable?

- [ ] Avoid: Treats every user the same
- [ ] Avoid: Ignores legal duties
- [ ] Avoid: Skips expert testing
- [ ] Ready for the follow-up: How does your escalation path change for a distressed user?

**RAI-23** How do you monitor fairness and safety after launch?

- [ ] Avoid: Stops monitoring after launch
- [ ] Avoid: Tracks overall metrics only
- [ ] Avoid: Sets no thresholds or rollback triggers
- [ ] Ready for the follow-up: What metric shift would make you roll back?

**RAI-24** How do you handle a data deletion request when data may be in a model?

- [ ] Avoid: Says deleting a row is enough
- [ ] Avoid: Ignores logs and indexes
- [ ] Avoid: Doesn't assess training use
- [ ] Ready for the follow-up: The data was used for fine-tuning. What are your options?

**RAI-25** How do you manage differing regulations across countries?

- [ ] Avoid: Follows one country's rules only
- [ ] Avoid: Builds no control matrix
- [ ] Avoid: Doesn't track regulatory change
- [ ] Ready for the follow-up: How do you design for a country with stricter rules than your baseline?

**RAI-26** What are the main governance risks specific to generative AI compared with traditional ML?

- [ ] Avoid: Treats it as identical to traditional ML
- [ ] Avoid: Believes testing can prove absence of harm
- [ ] Avoid: Ignores over-trust by users
- [ ] Ready for the follow-up: Which of these risks would you prioritise for an internal HR chatbot?

**RAI-27** How does governance change when an AI system can take actions, not only produce text?

- [ ] Avoid: Applies only content-safety controls
- [ ] Avoid: Leaves accountability unassigned
- [ ] Avoid: Grants broad standing permissions
- [ ] Ready for the follow-up: Who is accountable when an agent takes a harmful action within its permissions?

**RAI-28** A team says documentation slows them down. How do you keep it useful and lightweight?

- [ ] Avoid: Demands the same documents for every project
- [ ] Avoid: Ignores the team's actual pain
- [ ] Avoid: Keeps documents nobody reads
- [ ] Ready for the follow-up: Which documents would you require for a low-risk internal tool?

**RAI-29** A provider updates its model and outputs change for your regulated use case. How do you govern that?

- [ ] Avoid: Accepts silent updates
- [ ] Avoid: Re-tests only accuracy
- [ ] Avoid: Has no rollback path
- [ ] Ready for the follow-up: The provider gives only a week's notice of deprecation. What do you do?

**RAI-30** Tell me about a time you had to say no to a launch or slow one down for governance reasons. How did you handle it?

- [ ] Avoid: Presents governance as a veto for its own sake
- [ ] Avoid: Offers no alternatives
- [ ] Avoid: Cannot name a real example
- [ ] Ready for the follow-up: What would you do if a senior leader overruled you?

## LLMOps Engineer

Full answers: [questions/06-llmops-engineer.md](questions/06-llmops-engineer.md)

**OPS-1** How do you deploy and version LLM applications safely?

- [ ] Avoid: Versions code but not prompts and models
- [ ] Avoid: Deploys straight to production
- [ ] Avoid: Has no rollback path
- [ ] Ready for the follow-up: How do you deploy a prompt change without redeploying the app?

**OPS-2** What do you monitor in production LLM systems?

- [ ] Avoid: Monitors uptime only
- [ ] Avoid: Doesn't sample quality
- [ ] Avoid: Sets alerts with no thresholds
- [ ] Ready for the follow-up: Everything is green but users complain. What is missing?

**OPS-3** How do you control LLM costs at scale?

- [ ] Avoid: Cuts quality to save cost
- [ ] Avoid: Tracks no cost per task
- [ ] Avoid: Sets no per-team budgets
- [ ] Ready for the follow-up: Which cost lever do you pull first, and why?

**OPS-4** How do you reduce latency for a chat application?

- [ ] Avoid: Only switches to a smaller model
- [ ] Avoid: Ignores streaming and caching
- [ ] Avoid: Measures average latency
- [ ] Ready for the follow-up: p95 is bad but the average is fine. What do you check?

**OPS-5** How do you handle provider outages and rate limits?

- [ ] Avoid: Uses a single provider with no fallback
- [ ] Avoid: Retries with no backoff
- [ ] Avoid: Never rehearses failover
- [ ] Ready for the follow-up: The fallback model behaves differently. How do you manage that?

**OPS-6** When would you self-host an open model instead of using an API?

- [ ] Avoid: Assumes self-hosting is always cheaper
- [ ] Avoid: Ignores GPU and on-call costs
- [ ] Avoid: Has no volume estimate
- [ ] Ready for the follow-up: At what volume does self-hosting break even?

**OPS-7** Quality dropped and no code changed. What do you investigate?

- [ ] Avoid: Says nothing changed so it can't be us
- [ ] Avoid: Ignores provider updates
- [ ] Avoid: Has no eval set to compare against
- [ ] Ready for the follow-up: How would you confirm the provider changed the model?

**OPS-8** A prompt change caused a spike of bad outputs at 2am. How do you respond?

- [ ] Avoid: Debugs live before rolling back
- [ ] Avoid: Skips the blameless review
- [ ] Avoid: Doesn't turn failures into tests
- [ ] Ready for the follow-up: What release gate would have caught this?

**OPS-9** Why use a prompt registry, and what should it support?

- [ ] Avoid: Keeps prompts scattered across code
- [ ] Avoid: Has no owners or audit history
- [ ] Avoid: Has no environment separation
- [ ] Ready for the follow-up: Who should be allowed to change a production prompt?

**OPS-10** What does CI/CD look like for an LLM application?

- [ ] Avoid: Skips evals in the pipeline
- [ ] Avoid: Tests only the code
- [ ] Avoid: Has no automatic rollback
- [ ] Ready for the follow-up: What fails the build in your pipeline?

**OPS-11** What does a model gateway provide?

- [ ] Avoid: Calls providers directly from each app
- [ ] Avoid: Has no central logging
- [ ] Avoid: Enforces no policy
- [ ] Ready for the follow-up: What would you put in the gateway first?

**OPS-12** What should LLM tracing capture?

- [ ] Avoid: Logs only final responses
- [ ] Avoid: Uses no trace IDs
- [ ] Avoid: Stores raw personal data
- [ ] Ready for the follow-up: How do you debug one bad conversation from production?

**OPS-13** When is semantic caching a good idea?

- [ ] Avoid: Caches every response
- [ ] Avoid: Sets loose similarity thresholds
- [ ] Avoid: Caches personalised answers
- [ ] Ready for the follow-up: A cached answer is wrong for a different user. How did that happen?

**OPS-14** How do you autoscale GPU inference?

- [ ] Avoid: Scales on CPU only
- [ ] Avoid: Ignores cold starts
- [ ] Avoid: Sets no cost ceiling
- [ ] Ready for the follow-up: Traffic spikes at 9am daily. How do you handle cold starts?

**OPS-15** How can you make self-hosted inference cheaper and faster?

- [ ] Avoid: Buys bigger GPUs first
- [ ] Avoid: Doesn't validate quality after quantisation
- [ ] Avoid: Ignores batching
- [ ] Ready for the follow-up: How do you check quality didn't drop after quantising?

**OPS-16** How do you isolate tenants in a shared LLM platform?

- [ ] Avoid: Shares indexes and caches across tenants
- [ ] Avoid: Sets no per-tenant quotas
- [ ] Avoid: Never tests isolation
- [ ] Ready for the follow-up: How do you prove one tenant can't see another's data?

**OPS-17** How do you manage API keys and secrets for LLM services?

- [ ] Avoid: Keeps keys in code or config files
- [ ] Avoid: Never rotates them
- [ ] Avoid: Puts secrets in prompts or logs
- [ ] Ready for the follow-up: A key leaks in a log. What do you do?

**OPS-18** How do you balance detailed logging with privacy?

- [ ] Avoid: Logs everything forever
- [ ] Avoid: Logs nothing to protect privacy
- [ ] Avoid: Sets no access restrictions
- [ ] Ready for the follow-up: Debugging needs full prompts. How do you allow that safely?

**OPS-19** How do you keep a RAG index fresh?

- [ ] Avoid: Re-indexes everything manually
- [ ] Avoid: Ignores deleted documents
- [ ] Avoid: Doesn't monitor freshness
- [ ] Ready for the follow-up: A document is deleted at the source. How does it leave the index?

**OPS-20** How do feature flags help with LLM releases?

- [ ] Avoid: Releases to everyone at once
- [ ] Avoid: Has no way to switch off instantly
- [ ] Avoid: Ties release to deployment
- [ ] Ready for the follow-up: How would you run a 5% rollout of a new model?

**OPS-21** How do you define SLOs for an LLM service?

- [ ] Avoid: Sets availability targets only
- [ ] Avoid: Adds no quality indicators
- [ ] Avoid: Has no error budgets
- [ ] Ready for the follow-up: How do you turn a quality dip into an SLO breach?

**OPS-22** How do you attribute LLM costs to teams and features?

- [ ] Avoid: Tracks total spend only
- [ ] Avoid: Uses no tags by team or feature
- [ ] Avoid: Reviews costs annually
- [ ] Ready for the follow-up: One feature's cost spikes. How fast can you find it?

**OPS-23** How do you manage fine-tuned models across their lifecycle?

- [ ] Avoid: Stores models with no lineage
- [ ] Avoid: Cannot reproduce training
- [ ] Avoid: Requires no approvals
- [ ] Ready for the follow-up: An auditor asks how model v3 was produced. What do you show?

**OPS-24** What belongs in an on-call runbook for an LLM service?

- [ ] Avoid: Writes runbooks with generic steps
- [ ] Avoid: Leaves out rollback and failover steps
- [ ] Avoid: Never updates them after incidents
- [ ] Ready for the follow-up: What is on the first page of your runbook?

**OPS-25** How do you make staging environments realistic for LLM apps?

- [ ] Avoid: Uses mocked responses only
- [ ] Avoid: Uses unrealistic traffic and data
- [ ] Avoid: Skips real provider limits
- [ ] Ready for the follow-up: What issue only shows up in realistic staging?

**OPS-26** How would you detect that an LLM application has started producing lower-quality answers before customers complain?

- [ ] Avoid: Monitors only uptime and latency
- [ ] Avoid: Waits for customer complaints
- [ ] Avoid: Uses a judge that was never validated
- [ ] Ready for the follow-up: The judge score is stable but complaints rise. What do you check?

**OPS-27** Your traffic doubles during a marketing campaign and you hit provider rate limits. What do you do in the moment and afterwards?

- [ ] Avoid: Only asks the provider for more quota
- [ ] Avoid: Has no priority between traffic types
- [ ] Avoid: Never load-tests the peak
- [ ] Ready for the follow-up: Which requests would you drop first, and how would you decide?

**OPS-28** How do you roll out a new model version when you cannot fully predict how it will behave?

- [ ] Avoid: Switches all traffic at once
- [ ] Avoid: Relies only on public benchmarks
- [ ] Avoid: Removes the old model immediately
- [ ] Ready for the follow-up: The canary looks fine on average but worse for one customer. What now?

**OPS-29** How do you handle user data that ends up in prompts, logs and traces in your LLM platform?

- [ ] Avoid: Logs full prompts forever
- [ ] Avoid: Gives all engineers access to traces
- [ ] Avoid: Forgets caches when handling deletion
- [ ] Ready for the follow-up: A user requests deletion. Where might their data still exist in your platform?

**OPS-30** Tell me about an outage or incident you handled on an ML or LLM system. What did you change afterwards?

- [ ] Avoid: Blames one person
- [ ] Avoid: Cannot describe any lasting change
- [ ] Avoid: Focuses only on the heroics
- [ ] Ready for the follow-up: How did you know your fix worked?

## AI Solutions Architect

Full answers: [questions/07-ai-solutions-architect.md](questions/07-ai-solutions-architect.md)

**ARCH-1** How do you design an enterprise architecture for generative AI?

- [ ] Avoid: Draws boxes with no security or cost
- [ ] Avoid: Locks into one model
- [ ] Avoid: Assigns no ownership per layer
- [ ] Ready for the follow-up: Which layer would you build first for a pilot, and why?

**ARCH-2** How do you decide between build, buy and partner for AI capabilities?

- [ ] Avoid: Builds everything, or buys everything
- [ ] Avoid: Ignores lock-in and skills
- [ ] Avoid: Never revisits the decision
- [ ] Ready for the follow-up: The vendor's price doubles after year one. What is your exit?

**ARCH-3** How do you advise a client choosing between RAG and fine-tuning?

- [ ] Avoid: Says fine-tuning is always better
- [ ] Avoid: Ignores citations and freshness
- [ ] Avoid: Doesn't start with prompting
- [ ] Ready for the follow-up: The client insists on fine-tuning. How do you respond?

**ARCH-4** What are the key security risks in LLM architectures?

- [ ] Avoid: Mentions only hallucinations
- [ ] Avoid: Ignores agent permissions
- [ ] Avoid: Has no supply-chain thinking
- [ ] Ready for the follow-up: Which single control gives the most protection for the least effort?

**ARCH-5** How do you design for multiple models and vendors?

- [ ] Avoid: Integrates each vendor directly
- [ ] Avoid: Has no central logging or policy
- [ ] Avoid: Ignores eval-driven switching
- [ ] Ready for the follow-up: How do you switch a model without breaking the application?

**ARCH-6** How do you plan for scale and cost in an AI platform?

- [ ] Avoid: Ignores token volumes
- [ ] Avoid: Sets no quotas
- [ ] Avoid: Estimates cost per call only
- [ ] Ready for the follow-up: Usage grows 5x in six months. What breaks first?

**ARCH-7** How do you explain trade-offs to non-technical executives?

- [ ] Avoid: Uses jargon with executives
- [ ] Avoid: Presents options with no recommendation
- [ ] Avoid: Hides uncertainty
- [ ] Ready for the follow-up: The CFO asks 'why can't it be 100% accurate?' What do you say?

**ARCH-8** A bank wants AI on top of legacy systems under strict compliance. What is your approach?

- [ ] Avoid: Proposes a big-bang rebuild
- [ ] Avoid: Ignores compliance and audit
- [ ] Avoid: Moves data outside approved regions
- [ ] Ready for the follow-up: Which use case would you start with at the bank, and why?

**ARCH-9** What does a production RAG reference architecture include?

- [ ] Avoid: Lists only a vector database and an LLM
- [ ] Avoid: Leaves out evaluation and monitoring
- [ ] Avoid: Ignores access control at retrieval
- [ ] Ready for the follow-up: A user retrieves a document they shouldn't see. Where did the design fail?

**ARCH-10** How do you prepare enterprise data for AI use?

- [ ] Avoid: Says data is the client's problem
- [ ] Avoid: Ignores ownership, quality and lineage
- [ ] Avoid: Has no plan for freshness
- [ ] Ready for the follow-up: Data is scattered across ten systems. Where do you start?

**ARCH-11** How do you choose between cloud AI services, private cloud and on-premises?

- [ ] Avoid: Always recommends public cloud
- [ ] Avoid: Ignores regulation and skills
- [ ] Avoid: Offers no hybrid option
- [ ] Ready for the follow-up: Which workloads would you keep private, and why?

**ARCH-12** How do you design for tight latency requirements?

- [ ] Avoid: Only picks a faster model
- [ ] Avoid: Sets no per-step latency budget
- [ ] Avoid: Measures average, not p95
- [ ] Ready for the follow-up: Latency is 6s and the target is 2s. Where do you cut first?

**ARCH-13** How do you add AI features to a multi-tenant SaaS product?

- [ ] Avoid: Shares prompts and caches across tenants
- [ ] Avoid: Has no per-tenant metering
- [ ] Avoid: Ignores fair use
- [ ] Ready for the follow-up: How would you test that tenant data never leaks?

**ARCH-14** How do you make an AI system resilient?

- [ ] Avoid: Uses a single provider and region
- [ ] Avoid: Has no fallback or graceful degradation
- [ ] Avoid: Never tests failover
- [ ] Ready for the follow-up: The provider is down for an hour. What do users see?

**ARCH-15** Which integration patterns work well for AI in enterprise systems?

- [ ] Avoid: Tightly couples AI to the core system
- [ ] Avoid: Uses synchronous calls for everything
- [ ] Avoid: Ignores adapters for legacy systems
- [ ] Ready for the follow-up: When would you use events instead of an API call?

**ARCH-16** What architectural concerns are specific to enterprise agents?

- [ ] Avoid: Treats agents like chatbots
- [ ] Avoid: Ignores identity and delegated permissions
- [ ] Avoid: Has no audit logs or cost limits
- [ ] Ready for the follow-up: How do you stop an agent acting beyond the user's permissions?

**ARCH-17** How do you estimate total cost of ownership for an AI solution?

- [ ] Avoid: Counts only model costs
- [ ] Avoid: Ignores data, integration and support
- [ ] Avoid: Shows no sensitivity to usage
- [ ] Ready for the follow-up: Which cost line do clients usually underestimate?

**ARCH-18** What typically breaks between a PoC and production?

- [ ] Avoid: Says the PoC just needs scaling
- [ ] Avoid: Ignores evals and monitoring
- [ ] Avoid: Discovers security reviews late
- [ ] Ready for the follow-up: What would be on your production-readiness checklist?

**ARCH-19** How do you run a fair vendor evaluation?

- [ ] Avoid: Chooses on demos or price
- [ ] Avoid: Uses no shared eval set
- [ ] Avoid: Skips contract and security review
- [ ] Ready for the follow-up: Two vendors score equally. How do you decide?

**ARCH-20** How should identity and access work in an AI architecture?

- [ ] Avoid: Gives the model service-level access
- [ ] Avoid: Doesn't propagate user identity
- [ ] Avoid: Enforces permissions only in the UI
- [ ] Ready for the follow-up: How do you enforce document-level permissions in RAG?

**ARCH-21** How do you migrate an application to a new model safely?

- [ ] Avoid: Swaps the model with no evals
- [ ] Avoid: Ignores behavioural differences
- [ ] Avoid: Has no rollback
- [ ] Ready for the follow-up: How would you shadow-test a new model?

**ARCH-22** A vendor promises big accuracy gains. How do you validate the claim?

- [ ] Avoid: Accepts vendor benchmarks
- [ ] Avoid: Runs no trial on client data
- [ ] Avoid: Ignores failure modes and load
- [ ] Ready for the follow-up: The vendor won't allow a trial on your data. What do you do?

**ARCH-23** When does on-device or edge AI make sense?

- [ ] Avoid: Says edge AI is always cheaper
- [ ] Avoid: Ignores device constraints
- [ ] Avoid: Doesn't test on target hardware
- [ ] Ready for the follow-up: How do you update models on devices in the field?

**ARCH-24** What kinds of technical debt are unique to AI systems?

- [ ] Avoid: Says AI has no unique debt
- [ ] Avoid: Leaves prompts and models untracked
- [ ] Avoid: Has no evals or ownership
- [ ] Ready for the follow-up: Which debt would hurt you most a year from now?

**ARCH-25** How do you choose between a workflow and an agentic architecture for a client?

- [ ] Avoid: Recommends agents by default
- [ ] Avoid: Doesn't justify autonomy with evals
- [ ] Avoid: Ignores risk analysis
- [ ] Ready for the follow-up: The client wants an agent for a fixed process. How do you respond?

**ARCH-26** How do you design an AI platform so that individual teams can build quickly while central risk requirements are still met?

- [ ] Avoid: Requires manual approval for everything
- [ ] Avoid: Builds a platform teams find slow
- [ ] Avoid: Leaves each team to solve security alone
- [ ] Ready for the follow-up: A team wants a model outside the approved list. How do you decide?

**ARCH-27** A client wants to use customer conversations to improve their AI assistant. How do you advise them?

- [ ] Avoid: Uses all data because it is available
- [ ] Avoid: Ignores consent and retention
- [ ] Avoid: Skips legal review
- [ ] Ready for the follow-up: A customer asks for their conversations to be removed from the training set. What must the architecture support?

**ARCH-28** How do you build evaluation into the architecture, not treat it as a later testing phase?

- [ ] Avoid: Leaves testing until the end
- [ ] Avoid: Stores no traces to replay
- [ ] Avoid: Has no route from production failures to the eval set
- [ ] Ready for the follow-up: What would you cut if the budget were halved, and what would you keep?

**ARCH-29** A client asks you to choose their first generative AI use case. How do you decide?

- [ ] Avoid: Picks the most impressive demo
- [ ] Avoid: Chooses a high-risk customer-facing case first
- [ ] Avoid: Defines no success metric
- [ ] Ready for the follow-up: The CEO wants the most ambitious use case first. How do you respond?

**ARCH-30** Tell me about an architecture decision you got wrong. What happened and what did you learn?

- [ ] Avoid: Claims never to have been wrong
- [ ] Avoid: Blames the client or the team
- [ ] Avoid: Cannot say what changed in their practice
- [ ] Ready for the follow-up: How do you now decide which decisions are easy to reverse and which are not?
