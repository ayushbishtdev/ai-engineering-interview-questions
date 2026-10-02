# Data

`ai-engineering-interview-questions.csv` holds all 210 questions (7 roles x 30) in one flat file, UTF-8, comma-separated, one row per question. Load it into a spreadsheet, a flashcard tool, or a script.

| Column | Meaning |
|---|---|
| `role_slug` | Role identifier, matches the file names in `questions/` |
| `role_name` | Display name of the role |
| `question_id` | Question number within the role, 1 to 30 |
| `competency` | Skill area the question probes (for example RAG, Guardrails, Scoping) |
| `difficulty` | `Foundation`, `Practitioner` or `Advanced` |
| `question` | The interview question or scenario |
| `what_it_tests` | One line on what the interviewer is looking for |
| `model_answer` | A strong answer, written in first person |
| `red_flags` | Answers that lose points, separated by ` | ` |
| `follow_up` | The follow-up question that usually comes next |
| `source_page` | Page the role's questions were taken from |

Level mix across the dataset: 27 Foundation, 118 Practitioner, 65 Advanced.

Quick start (Python):

```python
import pandas as pd
df = pd.read_csv("ai-engineering-interview-questions.csv")
print(df[df.difficulty == "Foundation"][["role_name", "question"]])
```

Source: the interview-question pages at https://aidevdayindia.org/interview-questions/, last updated 30 September 2026 on the source site. Corrections welcome via issues.
