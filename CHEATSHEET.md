# Cheatsheet: AI engineering interview prep

One page to print or pin. IDs like `AIE-4` mean question 4 in the AI Engineer set; every ID resolves to a file in `questions/`.

## The three-step method

1. **Write first.** Answer in your own words, aloud or typed, before opening the model answer. If you cannot produce about sixty words unaided, you cannot produce them under pressure.
2. **Compare structure, not wording.** Model answers show how a strong candidate frames a trade-off. Copying phrasing is obvious to an interviewer.
3. **Rehearse the follow-up.** Each scenario lists the question that usually comes next. That second question is where most candidates come apart.

## Role map

| Code | Role | Foundation | Practitioner | Advanced | File |
|---|---|---|---|---|---|
| AIE | AI Engineer (Prompt & Context Engineering) | 6 | 18 | 6 | [questions/01-ai-engineer.md](questions/01-ai-engineer.md) |
| AGT | Agentic AI Engineer | 3 | 16 | 11 | [questions/02-agentic-ai-engineer.md](questions/02-agentic-ai-engineer.md) |
| EVAL | AI Evaluation Engineer | 4 | 16 | 10 | [questions/03-ai-evaluation-engineer.md](questions/03-ai-evaluation-engineer.md) |
| FDE | Forward Deployed Engineer | 5 | 18 | 7 | [questions/04-forward-deployed-engineer.md](questions/04-forward-deployed-engineer.md) |
| RAI | Responsible AI / AI Governance Engineer | 3 | 14 | 13 | [questions/05-responsible-ai-governance-engineer.md](questions/05-responsible-ai-governance-engineer.md) |
| OPS | LLMOps Engineer | 2 | 19 | 9 | [questions/06-llmops-engineer.md](questions/06-llmops-engineer.md) |
| ARCH | AI Solutions Architect | 4 | 17 | 9 | [questions/07-ai-solutions-architect.md](questions/07-ai-solutions-architect.md) |
| | **Total** | **27** | **118** | **65** | |

## Where topics recur across roles

The same ideas are asked from different angles depending on the role. Practising one angle helps with the others.

| Theme | Questions |
|---|---|
| Evaluating before shipping | `AIE-15`, `AGT-12`, `EVAL-12`, `AGT-27`, `ARCH-28`, `AIE-28`, `EVAL-1`, `EVAL-11` |
| Security and security reviews | `AIE-10`, `AGT-11`, `AGT-28`, `FDE-29`, `ARCH-4`, `FDE-6` |
| Cost control | `AIE-8`, `AGT-13`, `OPS-3`, `OPS-22`, `EVAL-16`, `ARCH-17`, `ARCH-6` |
| Personal data and privacy | `AIE-21`, `RAI-5`, `OPS-18`, `ARCH-27`, `RAI-24`, `FDE-23`, `OPS-29` |
| Model or vendor change | `AIE-25`, `ARCH-21`, `RAI-29`, `ARCH-19`, `ARCH-22`, `RAI-14` |
| Human oversight | `EVAL-5`, `AGT-10`, `RAI-6` |

## Start here: the Foundation questions

Twenty-seven questions at Foundation level, a sensible first pass before the harder ones.

**AI Engineer (Prompt & Context Engineering)**

- `AIE-5` How do you get reliable structured output from an LLM?
- `AIE-6` How do you choose a model for a new feature?
- `AIE-9` When do few-shot examples help, and when do they hurt?
- `AIE-19` How does streaming change the user experience of an LLM feature?
- `AIE-20` How do you get more consistent outputs from an LLM?
- `AIE-23` Product gives you a vague requirement for an AI feature. What do you do?

**Agentic AI Engineer**

- `AGT-3` What problem does the Model Context Protocol solve?
- `AGT-16` How do you choose an agent framework?
- `AGT-24` How should an agent handle an ambiguous goal?

**AI Evaluation Engineer**

- `EVAL-8` A vendor claims state-of-the-art benchmark scores. Do you trust them?
- `EVAL-15` What makes a good evaluation rubric?
- `EVAL-21` How do you report eval results to executives?
- `EVAL-29` What would you look for when choosing an evaluation framework or platform?

**Forward Deployed Engineer**

- `FDE-1` What does a forward deployed engineer do that a regular engineer doesn't?
- `FDE-9` How do you run discovery with a new customer?
- `FDE-10` How do you design a demo that convinces a customer?
- `FDE-22` How do you train a customer's engineers to work with the solution?
- `FDE-27` How do you explain a technical limitation to a non-technical executive?

**Responsible AI / AI Governance Engineer**

- `RAI-4` What documentation should accompany a deployed model?
- `RAI-9` Why keep an inventory of AI systems, and what goes in it?
- `RAI-20` How would you write a generative-AI acceptable-use policy for employees?

**LLMOps Engineer**

- `OPS-17` How do you manage API keys and secrets for LLM services?
- `OPS-24` What belongs in an on-call runbook for an LLM service?

**AI Solutions Architect**

- `ARCH-3` How do you advise a client choosing between RAG and fine-tuning?
- `ARCH-7` How do you explain trade-offs to non-technical executives?
- `ARCH-22` A vendor promises big accuracy gains. How do you validate the claim?
- `ARCH-29` A client asks you to choose their first generative AI use case. How do you decide?

## The behavioural question in every set

Question 30 of each role is a "tell me about a time" prompt. Prepare one real story per role you are targeting.

- `AIE-30` Tell me about an AI feature you built that did not work in production. What did you do?
- `AGT-30` Tell me about an agent behaviour that surprised you in testing. How did you respond?
- `EVAL-30` Tell me about a time an evaluation result changed a decision the team had already made.
- `FDE-30` Tell me about a deployment that went wrong at a customer site. What did you do and what did you change?
- `RAI-30` Tell me about a time you had to say no to a launch or slow one down for governance reasons. How did you handle it?
- `OPS-30` Tell me about an outage or incident you handled on an ML or LLM system. What did you change afterwards?
- `ARCH-30` Tell me about an architecture decision you got wrong. What happened and what did you learn?

## Habits that appear in many model answers

These are patterns you can check against the answers in `questions/`:

- Start with the simplest design that works, add complexity only where evidence shows a gap (see `AGT-1`, `ARCH-3`).
- Measure with your own eval set instead of trusting a vendor benchmark or a stricter prompt (see `EVAL-8`, `AIE-4`).
- Say what evidence would change your recommendation (see `ARCH-3`).
- Keep secrets, personal data and prompts out of logs by design (see `OPS-17`, `OPS-29`).
- Treat documentation as versioned, audience-specific and owned (see `RAI-4`).
