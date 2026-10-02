# AI Engineer (Prompt & Context Engineering): 30 interview questions with model answers

Thirty scenarios on prompt and context engineering, RAG, structured output, model selection and cost for production LLM features. Write your own answer first, then open the model answer to compare structure and reasoning.

Level mix: 6 Foundation, 18 Practitioner, 6 Advanced. Each question lists what the interviewer is testing, a model answer, red-flag answers to avoid, and the follow-up to expect.

## Contents

1. [How do you structure a production prompt so it stays reliable as requirements change?](#q1) (Prompt Engineering, Practitioner)
2. [What is context engineering and how does it differ from writing prompts?](#q2) (Context Engineering, Practitioner)
3. [Your RAG answers are wrong even though the right document exists. How do you debug it?](#q3) (RAG, Practitioner)
4. [How do you reduce hallucinations in a customer-facing assistant?](#q4) (Hallucinations, Practitioner)
5. [How do you get reliable structured output from an LLM?](#q5) (Structured Output, Foundation)
6. [How do you choose a model for a new feature?](#q6) (Model Selection, Foundation)
7. [When would you use a long context window instead of retrieval?](#q7) (Long Context, Practitioner)
8. [Your token bill doubled after a launch. What do you check first?](#q8) (Cost, Practitioner)
9. [When do few-shot examples help, and when do they hurt?](#q9) (Few-shot Prompting, Foundation)
10. [How do you defend an LLM app against prompt injection?](#q10) (Prompt Injection, Advanced)
11. [How do you decide on a chunking strategy for documents?](#q11) (Chunking, Practitioner)
12. [How do you choose an embedding model and vector store?](#q12) (Embeddings, Practitioner)
13. [Why combine keyword and vector search?](#q13) (Hybrid Search, Practitioner)
14. [How do you make function calling reliable?](#q14) (Function Calling, Practitioner)
15. [How do you evaluate whether a prompt change is actually better?](#q15) (Prompt Evaluation, Practitioner)
16. [Where can caching reduce cost and latency in an LLM app?](#q16) (Caching, Practitioner)
17. [When is fine-tuning worth it over prompting?](#q17) (Fine-tuning, Advanced)
18. [How do you handle Indian languages in an LLM feature?](#q18) (Multilingual, Practitioner)
19. [How does streaming change the user experience of an LLM feature?](#q19) (Streaming UX, Foundation)
20. [How do you get more consistent outputs from an LLM?](#q20) (Determinism, Foundation)
21. [How do you handle personal data in prompts?](#q21) (PII Handling, Advanced)
22. [How do you manage long conversations within context limits?](#q22) (Conversation Memory, Practitioner)
23. [Product gives you a vague requirement for an AI feature. What do you do?](#q23) (Ambiguous Requirements, Foundation)
24. [Outputs are inconsistent across users. How do you investigate?](#q24) (Debugging, Practitioner)
25. [A provider deprecates the model you depend on. How do you prepare?](#q25) (Model Deprecation, Practitioner)
26. [Your AI feature has good answers but a p95 latency of twelve seconds. How do you bring it down?](#q26) (Latency, Practitioner)
27. [When is a reranker worth the extra latency and cost?](#q27) (Retrieval, Practitioner)
28. [You are building a RAG assistant and have no labelled data. How do you create an eval set?](#q28) (Evaluation Data, Advanced)
29. [When would you use a reasoning model instead of a standard model, and what does it cost you?](#q29) (Model Selection, Advanced)
30. [Tell me about an AI feature you built that did not work in production. What did you do?](#q30) (Behavioural, Advanced)

<a id="q1"></a>

### 1. How do you structure a production prompt so it stays reliable as requirements change?

**Competency:** Prompt Engineering | **Level:** Practitioner

**What it tests:** Whether prompts are structured, versioned and eval-gated.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I split the prompt into role, task, constraints, context and output format so each part can change without disturbing the others, and I keep it in version control with a changelog. Examples come from real inputs, not invented ones. Before any change I run a fixed eval set of common and edge cases and compare against the previous version. Small targeted edits beat rewrites because I can attribute a regression to one change. When a requirement shifts, I add the new cases to the eval set first, watch them fail, then adjust the prompt until they pass without breaking the older ones.

**Red-flag answers**

- Writes one long unstructured prompt
- Doesn't version prompts
- Changes prompts without running evals

**Expect this follow-up:** A prompt fix helps one case and breaks another. How do you prevent that?

</details>

<a id="q2"></a>

### 2. What is context engineering and how does it differ from writing prompts?

**Competency:** Context Engineering | **Level:** Practitioner

**What it tests:** Whether you curate what the model sees, not just what you say.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Prompting is the instruction; context engineering is deciding everything the model sees when it reads that instruction: retrieved documents, memory, tool results, conversation history, and the order and size of each. I rank, filter and compress context because irrelevant tokens cost money, add latency and pull attention away from what matters. I also decide what goes near the start or end of the window, since position affects recall. In practice most quality gains in production systems come from better context, not cleverer wording, and I measure that with evals rather than intuition.

**Red-flag answers**

- Treats it as just better prompt wording
- Sends all retrieved text unfiltered
- Ignores context order and size

**Expect this follow-up:** What would you cut first when the context is too long?

</details>

<a id="q3"></a>

### 3. Your RAG answers are wrong even though the right document exists. How do you debug it?

**Competency:** RAG | **Level:** Practitioner

**What it tests:** Whether you separate retrieval failures from generation failures.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I split the problem in two: retrieval and generation. First I check whether the right chunk was retrieved and where it ranked. If it was missing, I look at chunking, embedding quality, hybrid search, metadata filters and query rewriting. If it was retrieved but ranked low, I add a reranker. If it was in the context and the answer is still wrong, the problem is generation: prompt clarity, context order, or too much noise. I keep retrieval metrics such as recall at k so I can tell which side broke before I touch the prompt.

**Red-flag answers**

- Changes the prompt before checking retrieval
- Blames the model by default
- Has no retrieval metrics

**Expect this follow-up:** The right chunk is retrieved but ignored. What next?

</details>

<a id="q4"></a>

### 4. How do you reduce hallucinations in a customer-facing assistant?

**Competency:** Hallucinations | **Level:** Practitioner

**What it tests:** Whether you reduce hallucination with grounding and measurement.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I ground answers in retrieved sources and require citations, so every claim can be checked. I explicitly allow 'I don't know' and reward it in evals, because a model that must always answer will invent. I constrain output format, add a verification step for high-risk claims, and route low-confidence or high-stakes cases to a human. Then I measure: a labelled eval set gives me a hallucination rate I can track across releases. A stricter prompt helps a little, but only measurement tells me whether the assistant is actually safer.

**Red-flag answers**

- Says a stricter prompt solves it
- Never allows 'I don't know'
- Tracks no hallucination rate on an eval set

**Expect this follow-up:** How do you decide when to route to a human?

</details>

<a id="q5"></a>

### 5. How do you get reliable structured output from an LLM?

**Competency:** Structured Output | **Level:** Foundation

**What it tests:** Whether you enforce schemas instead of asking politely.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I stop asking politely and enforce a schema. Native structured output or schema-constrained decoding guarantees valid shape, and I still validate values against the schema in code, because valid JSON can hold wrong content. On failure I retry once with the validation error included so the model can correct itself, then fall back to a safe default or a human. I keep schemas simple, with enums where possible, and log every failure. Recurring failures usually point to an ambiguous field description or an over-complex schema, which I fix at the source.

**Red-flag answers**

- Asks the model politely for JSON
- Does no schema validation
- Retries blindly without the error

**Expect this follow-up:** The schema is complex and fails often. What do you change?

</details>

<a id="q6"></a>

### 6. How do you choose a model for a new feature?

**Competency:** Model Selection | **Level:** Foundation

**What it tests:** Whether you choose models by your own evals and constraints.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start from requirements: quality bar, latency, cost per request, context length, data privacy and language coverage. I shortlist two or three models and compare them on my own eval set, not public benchmarks, because benchmarks rarely match my task. I pick the cheapest model that clears the quality bar with some margin, and I keep a second model as a fallback behind a thin abstraction so switching is cheap. I also plan to re-run the comparison periodically, since new models change the cost and quality picture every few months.

**Red-flag answers**

- Picks the newest or biggest model
- Relies on public benchmarks
- Has no fallback model

**Expect this follow-up:** The cheaper model is 3% worse. How do you decide?

</details>

<a id="q7"></a>

### 7. When would you use a long context window instead of retrieval?

**Competency:** Long Context | **Level:** Practitioner

**What it tests:** Whether you weigh long context against retrieval honestly.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Long context suits small, self-contained material and one-off analysis, like reading a single contract. Retrieval wins when the corpus is large, changes often, or needs citations, and it is cheaper per query because I send only what is relevant. I test both on the real task, because models can lose facts buried in the middle of a long prompt. Cost matters too: sending a full corpus on every request adds up quickly. Often the best design is hybrid: retrieve broadly, then place a generous but curated set of passages in a long window.

**Red-flag answers**

- Says long context replaces retrieval
- Ignores cost per query
- Doesn't test middle-of-context recall

**Expect this follow-up:** At what corpus size would you switch to retrieval?

</details>

<a id="q8"></a>

### 8. Your token bill doubled after a launch. What do you check first?

**Competency:** Cost | **Level:** Practitioner

**What it tests:** Whether you diagnose cost from tokens and traffic, not guesses.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start with the numbers, not guesses. I break the bill down by feature: tokens per request, request volume, retries, and how much context grew. Common causes are ballooning conversation history, an over-retrieved context, retry storms and a new feature routed to an expensive model. Fixes follow the cause: trim prompts, cap history, cache repeated prefixes, route easy tasks to a smaller model and set budgets with alerts per feature. I avoid cutting quality first; I only accept a quality trade-off after the eval set shows it is small.

**Red-flag answers**

- Blames traffic alone
- Has no per-feature cost visibility
- Cuts quality first

**Expect this follow-up:** Context per request grew 40%. Where would you look?

</details>

<a id="q9"></a>

### 9. When do few-shot examples help, and when do they hurt?

**Competency:** Few-shot Prompting | **Level:** Foundation

**What it tests:** Whether you know when examples help or bias output.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Few-shot examples help when the format or edge-case behaviour is hard to describe in words, such as tone, labelling rules or output structure. They hurt when examples are unrepresentative, when the model over-copies their surface pattern, or when they consume tokens that context could use better. I choose diverse examples from real data, include an edge case, and vary them so the model learns the rule, not the sample. Then I test with and without them on the eval set. If the gain is small, I drop them and save the tokens.

**Red-flag answers**

- Adds many examples by default
- Uses unrepresentative examples
- Never tests with and without

**Expect this follow-up:** The model copies your example too literally. What do you do?

</details>

<a id="q10"></a>

### 10. How do you defend an LLM app against prompt injection?

**Competency:** Prompt Injection | **Level:** Advanced

**What it tests:** Whether you layer defences and treat inputs as untrusted.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I assume all retrieved and user-supplied text is untrusted. I separate instructions from data with clear delimiters, but I know that alone is weak. The real protections are architectural: least-privilege tool permissions, confirmation for sensitive actions, no secrets in the prompt, output filtering, and never letting retrieved text trigger actions unchecked. I add an input and output classifier as another layer and log suspicious attempts. Before launch I run adversarial tests, including indirect injection through documents. No single defence works, so I layer them and plan for the case where one fails.

**Red-flag answers**

- Relies on 'ignore malicious instructions' in the prompt
- Trusts retrieved text as instructions
- Gives tools broad permissions

**Expect this follow-up:** How would you test your defences before launch?

</details>

<a id="q11"></a>

### 11. How do you decide on a chunking strategy for documents?

**Competency:** Chunking | **Level:** Practitioner

**What it tests:** Whether chunking follows structure and is tuned on metrics.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start with the document's own structure: headings, sections, lists and tables, so chunks hold complete ideas. Then I tune size and overlap against retrieval metrics on real user questions, since the best setting depends on the content and the questions. Each chunk carries metadata such as source, section title, date and access level, which supports filtering and citation. Tables and code need special handling so rows and columns stay together. I treat chunking as an experiment: change one parameter, re-run retrieval evals, and keep what measurably improves recall.

**Red-flag answers**

- Uses one fixed chunk size everywhere
- Ignores headings and tables
- Has no retrieval metrics on real questions

**Expect this follow-up:** A table gets split across chunks. How do you handle it?

</details>

<a id="q12"></a>

### 12. How do you choose an embedding model and vector store?

**Competency:** Embeddings | **Level:** Practitioner

**What it tests:** Whether you test embeddings on your own data and languages.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I compare candidate embedding models on my own retrieval eval, using real queries and documents in the languages my users write in. I weigh quality against dimensions, storage, latency, cost and licensing. For the vector store I look at scale, metadata filtering, hybrid search support, update patterns, and whether it fits our operations, such as managed versus self-hosted. Leaderboards are a starting shortlist, not a decision. I also plan for re-embedding, since changing the model later means reprocessing the whole corpus.

**Red-flag answers**

- Picks the top leaderboard model
- Doesn't test on their own data
- Ignores filtering and hybrid support

**Expect this follow-up:** Retrieval is good in English but poor in Hindi. What do you check?

</details>

<a id="q13"></a>

### 13. Why combine keyword and vector search?

**Competency:** Hybrid Search | **Level:** Practitioner

**What it tests:** Whether you know where vector search alone fails.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Vector search captures meaning but often misses exact tokens such as order IDs, product codes, names and rare terms. Keyword search does the opposite: precise on exact terms, weak on paraphrase. Combining both, then reranking the merged list, gives better recall and precision than either alone. I confirm the benefit on a set of real queries rather than assuming it, and I tune the fusion weights. For structured identifiers I sometimes add a direct lookup path, because no retrieval trick beats an exact match.

**Red-flag answers**

- Says vectors alone are enough
- Doesn't know about exact-term failures
- Adds no reranker

**Expect this follow-up:** Users search by order ID and get nothing. Why, and what's the fix?

</details>

<a id="q14"></a>

### 14. How do you make function calling reliable?

**Competency:** Function Calling | **Level:** Practitioner

**What it tests:** Whether tool calls are validated and evaluated.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Reliability starts with the tool definitions: clear names, precise descriptions and strict typed schemas with enums for closed choices. I validate every argument in code before executing, and return an informative error to the model so it can correct itself, with a hard cap on retries. Fewer, well-separated tools are chosen more accurately than many overlapping ones. I evaluate tool-selection and argument accuracy on realistic tasks, including ambiguous ones, and I log every call so failures can be traced and turned into new test cases.

**Red-flag answers**

- Writes vague function descriptions
- Does no argument validation
- Allows unlimited retries

**Expect this follow-up:** The model calls a function with an invalid argument. What happens next?

</details>

<a id="q15"></a>

### 15. How do you evaluate whether a prompt change is actually better?

**Competency:** Prompt Evaluation | **Level:** Practitioner

**What it tests:** Whether you prove improvement statistically and by segment.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I run the old and new prompt on the same eval set and compare metrics overall and by segment, because an average can hide a regression in an important group. I read a sample of failures by hand rather than trusting a score alone, and I check whether the difference is bigger than run-to-run noise. If it holds up, I release to a small share of traffic first and watch real-world metrics before going wide. Judging by a handful of examples is how teams ship regressions with confidence.

**Red-flag answers**

- Judges by a few examples
- Reports only averages
- Ships without a canary

**Expect this follow-up:** The new prompt is better overall but worse for one segment. What do you do?

</details>

<a id="q16"></a>

### 16. Where can caching reduce cost and latency in an LLM app?

**Competency:** Caching | **Level:** Practitioner

**What it tests:** Whether you cut cost without leaking or staling answers.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Prefix or prompt caching cuts cost and latency when a long system prompt or shared document is reused across requests. Response caching helps for identical queries. Embedding caching avoids recomputing vectors for unchanged text, and semantic caching can serve near-duplicate questions when the answers are safe to reuse. The risks are staleness and privacy: cached answers can go out of date, and a cache shared between users must never leak one person's data to another. I set expiry, scope caches by tenant, and measure hit rate to confirm the saving is real.

**Red-flag answers**

- Caches everything
- Ignores privacy and staleness
- Doesn't know prefix caching

**Expect this follow-up:** What would you never put in a semantic cache?

</details>

<a id="q17"></a>

### 17. When is fine-tuning worth it over prompting?

**Competency:** Fine-tuning | **Level:** Advanced

**What it tests:** Whether you justify fine-tuning with evidence of a gap.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Fine-tuning earns its place when prompting has a proven gap: consistent style or format at scale, lower latency and cost from a smaller model, or behaviour prompts cannot reach. It needs quality labelled data and an eval set to prove it worked. I always start with prompting, retrieval and evals, because they are faster to iterate and cheaper to undo. Fine-tuning also adds a maintenance burden, since I must retrain when the base model or the data changes. I fine-tune to close a measured gap, not to feel sophisticated.

**Red-flag answers**

- Fine-tunes before trying prompting
- Has no quality labelled data
- Cannot state the gap fine-tuning would close

**Expect this follow-up:** What evidence would convince you fine-tuning is needed?

</details>

<a id="q18"></a>

### 18. How do you handle Indian languages in an LLM feature?

**Competency:** Multilingual | **Level:** Practitioner

**What it tests:** Whether you test quality per language, including code-mixing.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I test quality per language on real user text, not translated English, because performance often drops for lower-resource languages. Users mix languages and write Hindi in Roman script, so I test code-mixing and transliteration explicitly. I tune prompts and retrieval per language, check that the embedding model actually handles them, and involve native speakers in evaluation. I also watch token cost, since some scripts tokenise into many more tokens. If a language falls below the quality bar, I limit the feature or add human review rather than ship something unreliable.

**Red-flag answers**

- Assumes English quality carries over
- Ignores code-mixing and transliteration
- Has no native-speaker evaluation

**Expect this follow-up:** Users type Hindi in Roman script. What breaks and how do you handle it?

</details>

<a id="q19"></a>

### 19. How does streaming change the user experience of an LLM feature?

**Competency:** Streaming UX | **Level:** Foundation

**What it tests:** Whether you understand streaming's effect on perceived latency.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Streaming shows the first words within a second or so, which sharply improves perceived latency even though total time is similar. The cost is complexity. Partial output can be wrong or later retracted, structured output cannot be parsed until it is complete, and safety checks may need the whole response. I handle cancellation so abandoned requests stop spending tokens, and I design the UI to handle a response that changes or stops midway. Where a check needs the full text, I may stream a draft and validate before enabling actions.

**Red-flag answers**

- Says streaming makes it faster overall
- Ignores validation of partial output
- Doesn't handle cancellation

**Expect this follow-up:** Safety checks need the full response. How do you stream anyway?

</details>

<a id="q20"></a>

### 20. How do you get more consistent outputs from an LLM?

**Competency:** Determinism | **Level:** Foundation

**What it tests:** Whether you accept variability and design validation around it.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I lower temperature, tighten the prompt, use structured output and fixed examples, and use a seed where the provider supports it. I also accept that full determinism is not guaranteed: batching, hardware and model updates can shift outputs even at temperature zero. So instead of assuming identical outputs, I design tolerance into the feature: validation, tests that check properties rather than exact strings, and monitoring for drift. If exact repeatability matters, such as for audit, I store the output rather than trying to regenerate it.

**Red-flag answers**

- Says temperature zero makes it deterministic
- Adds no validation of outputs
- Ignores structured output

**Expect this follow-up:** The output still varies at temperature zero. Why?

</details>

<a id="q21"></a>

### 21. How do you handle personal data in prompts?

**Competency:** PII Handling | **Level:** Advanced

**What it tests:** Whether you minimise and control personal data in prompts.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I minimise what I send: only the fields the task needs. Identifiers are redacted or tokenised before the call and restored afterwards where required. I choose providers whose data terms match our obligations, such as no training on our data and suitable retention, and I restrict what is logged and for how long. I map the data flows end to end and review them with security and legal. I also make sure evals and debugging tools do not become a side door that copies personal data into less protected places.

**Red-flag answers**

- Sends raw personal data to any provider
- Logs full prompts indefinitely
- Has no data-flow map

**Expect this follow-up:** Which fields would you redact before the model call?

</details>

<a id="q22"></a>

### 22. How do you manage long conversations within context limits?

**Competency:** Conversation Memory | **Level:** Practitioner

**What it tests:** Whether summaries preserve the facts that matter.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I keep recent turns verbatim, summarise older ones, and store durable facts such as the user's name, preferences and open tasks in a separate memory that I retrieve when relevant. The risk is that summaries quietly drop something important, so I test that key facts survive summarisation across many turns. I also cap history to control cost and latency. For sensitive facts I make memory visible and correctable to the user. The goal is that the conversation feels continuous without paying to resend everything each time.

**Red-flag answers**

- Sends the entire history every turn
- Loses key facts when summarising
- Never tests summarisation

**Expect this follow-up:** The user's name is forgotten after summarisation. How do you prevent it?

</details>

<a id="q23"></a>

### 23. Product gives you a vague requirement for an AI feature. What do you do?

**Competency:** Ambiguous Requirements | **Level:** Foundation

**What it tests:** Whether you turn vague asks into testable examples.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I turn the vague ask into something testable. I talk to the requester about the user problem and what success would look like, then build a quick prototype and run it on real examples. Showing actual outputs to stakeholders is far more effective than debating a spec, because people recognise good and bad results when they see them. I collect those reactions into an eval set, which becomes the definition of done. That way the requirement becomes concrete through iteration instead of waiting for a perfect document.

**Red-flag answers**

- Starts building without clarifying
- Waits for a perfect spec
- Doesn't show concrete outputs

**Expect this follow-up:** The stakeholder still can't say what 'good' means. What do you do?

</details>

<a id="q24"></a>

### 24. Outputs are inconsistent across users. How do you investigate?

**Competency:** Debugging | **Level:** Practitioner

**What it tests:** Whether you debug by comparing traces and changing one variable.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I compare traces across affected and unaffected cases: the input, the retrieved context, the prompt version, the model and its settings, and the tool results. I look for what differs, segment failures by user type, language or input length, and form a hypothesis. Then I change one variable at a time and re-run the evals so I know what fixed it. Changing several things at once makes the result unexplainable. Good tracing from the start makes this fast, which is why I insist on logging the full chain of context per request.

**Red-flag answers**

- Changes several variables at once
- Doesn't compare traces
- Has no hypothesis

**Expect this follow-up:** What is the first thing you record in a trace so you can compare users?

</details>

<a id="q25"></a>

### 25. A provider deprecates the model you depend on. How do you prepare?

**Competency:** Model Deprecation | **Level:** Practitioner

**What it tests:** Whether you plan migration before the deadline.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I treat deprecation as a scheduled event, not a surprise. I track provider notices, keep a model abstraction layer, and maintain an eval suite so I can test a replacement quickly on my own tasks. As soon as a successor is available, I compare it, adapt prompts where behaviour differs, and roll it out gradually with canary traffic while watching quality and cost. I keep the old model available until the new one has proven itself, and I never move all traffic at once. Starting early turns a deadline into a routine migration.

**Red-flag answers**

- Notices only at the deadline
- Has no abstraction or eval suite
- Switches all traffic at once

**Expect this follow-up:** The replacement model behaves differently on your prompts. What do you do?

</details>

<a id="q26"></a>

### 26. Your AI feature has good answers but a p95 latency of twelve seconds. How do you bring it down?

**Competency:** Latency | **Level:** Practitioner

**What it tests:** Whether you diagnose latency by stage and know the levers beyond a faster model.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I measure where the time goes: retrieval, prompt size, time to first token and output length. Output tokens usually dominate, so I shorten responses, stream them and cap length. I trim context, use prefix caching, and run independent calls such as retrieval and classification in parallel. Simple requests go to a smaller, faster model and only hard ones to the larger one. I set a latency budget per stage and watch p95, not the average, because users feel the slow tail.

**Red-flag answers**

- Only proposes a faster model
- Measures average latency, not p95
- Has no per-stage timing

**Expect this follow-up:** Streaming is on and users still complain. What else could be slow?

</details>

<a id="q27"></a>

### 27. When is a reranker worth the extra latency and cost?

**Competency:** Retrieval | **Level:** Practitioner

**What it tests:** Whether you add components because measurement shows a gain.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A reranker helps when first-stage retrieval finds the right passage but ranks it too low, which is common with large corpora and ambiguous queries. I measure it: compare recall and answer quality at the top few results with and without reranking on real queries. If the right chunk is already first most of the time, the extra hop is waste. I keep the candidate list small to limit latency, and I consider a lighter reranker if speed matters. It earns its place only if the gain is visible in the eval.

**Red-flag answers**

- Adds a reranker without measuring
- Ignores the added latency
- Reranks a huge candidate list

**Expect this follow-up:** Your reranker adds 400 ms. Product says it is too slow. What are your options?

</details>

<a id="q28"></a>

### 28. You are building a RAG assistant and have no labelled data. How do you create an eval set?

**Competency:** Evaluation Data | **Level:** Advanced

**What it tests:** Whether you can bootstrap evaluation honestly from real material.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

I start with real questions from support tickets, search logs or subject experts, since they reflect real usage. Where those are thin, I generate synthetic questions from the documents, then have an expert review and correct them, because unreviewed synthetic data flatters the system. Each item gets an expected answer or a rubric and the source passage. I include hard cases: ambiguous, multi-document and unanswerable questions. I keep a held-out part untouched for final checks and grow the set from production failures.

**Red-flag answers**

- Uses only unreviewed synthetic questions
- Tunes on the same set they report on
- Includes no unanswerable questions

**Expect this follow-up:** How do you stop the synthetic questions from being too easy?

</details>

<a id="q29"></a>

### 29. When would you use a reasoning model instead of a standard model, and what does it cost you?

**Competency:** Model Selection | **Level:** Advanced

**What it tests:** Whether you match model type to task difficulty and account for the trade-offs.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

Reasoning models help on multi-step problems such as planning, complex analysis or code with many constraints, where extra thinking improves correctness. They cost more, respond more slowly and consume extra tokens for the hidden reasoning. For simple extraction, classification or lookup they add cost with little benefit. I test both on my eval set by task type and route accordingly, sending only hard requests to the reasoning model. I also check that prompts written for standard models do not over-constrain the reasoning one.

**Red-flag answers**

- Uses the reasoning model for everything
- Ignores latency and token cost
- Never compares against a standard model on their eval

**Expect this follow-up:** How would you decide which requests get routed to the reasoning model?

</details>

<a id="q30"></a>

### 30. Tell me about an AI feature you built that did not work in production. What did you do?

**Competency:** Behavioural | **Level:** Advanced

**What it tests:** Whether you own failures, learn from them and change your process.

<details>
<summary>Model answer, red flags and follow-up</summary>

**Model answer**

A strong answer names a specific feature and what went wrong in concrete terms, such as answers that looked fine in demos but failed on real user phrasing. I would explain how I detected it, through user feedback, monitoring or an eval gap, and what I did first to limit harm. Then the root cause: usually an eval set that did not resemble real traffic. The lasting change is process: adding production samples to the eval set and gating releases on it. I would say plainly what I got wrong.

**Red-flag answers**

- Blames the model or the users
- Describes a success dressed up as a failure
- Cannot say what changed afterwards

**Expect this follow-up:** What would you have needed to see before launch to catch it?

</details>

---

Prefer to practise with a write-first answer box? The same scenarios are in the [AI Engineer (Prompt & Context Engineering) interview simulator](https://aidevdayindia.org/interview-questions/ai-engineer-interview-questions.html). Spotted a wrong or outdated answer? [Open a correction issue](https://github.com/ayushbishtdev/ai-engineering-interview-questions/issues/new?template=correction.md).
