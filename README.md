# Sri Lankan AL MCQ Extractor

A frontend-only web tool to extract MCQ questions from Sri Lankan Advanced Level past paper PDFs and export them as structured JSON.

---

## What This Tool Does

Upload a Sri Lankan AL MCQ paper PDF → AI extracts all 50 questions → Admin enters correct answers → Download clean JSON file ready for the learning app.

---

## Tech Stack

```
React + Vite        — Frontend
Groq API            — AI extraction (user provides key)
PDF.js              — PDF loading and text extraction
KaTeX               — Math formula rendering
Vercel              — Deployment
```

---

## Getting Started

### Run Locally

```bash
git clone https://github.com/{repo}
cd {repo}
npm install
npm run dev
```

### Deploy on Vercel

```bash
npm run build
```

Connect repo to Vercel — no environment variables needed.

---

## How to Use

```
Step 1 — Paste your Groq API key
Step 2 — Select subject, medium, year
Step 3 — Upload MCQ paper PDF
Step 4 — Click Extract
Step 5 — Enter correct answer (1 to 5) for each question
Step 6 — Download JSON
```

---

## Supported Subjects

```
Science  : Biology, Chemistry, Physics
Commerce : Accounting, Economics
Arts     : Geography
```

## Supported Mediums

```
Tamil (primary)
Sinhala
English
```

---

## Project Docs

All documentation is in the `/docs` folder. Read in this order:

```
docs/01_problem_overview.md     — Project goal and constraints
docs/02_pdf_input_types.md      — PDF types and detection strategy
docs/03_question_types.md       — All 9 MCQ types with JSON examples
docs/04_json_schema.md          — Fixed JSON schema and rules
docs/05_extraction_strategy.md  — AI extraction and prompt strategy
docs/06_architecture.md         — Folder structure and component responsibilities
docs/07_image_url_pattern.md    — Image URL pattern and builder logic
```

---

## JSON Output Format

```json
[
  {
    "orderIndex": 1,
    "questionText": "question content here",
    "questionImageUrl": null,
    "marks": 2,
    "correctOptionIndex": 0,
    "options": [
      { "optionText": "option one", "optionImageUrl": null },
      { "optionText": "option two", "optionImageUrl": null },
      { "optionText": "option three", "optionImageUrl": null },
      { "optionText": "option four", "optionImageUrl": null },
      { "optionText": "option five", "optionImageUrl": null }
    ]
  }
]
```

### Key Rules

```
orderIndex        — 1 to 50, sequential
marks             — always 2
correctOptionIndex — 0 to 4 (admin inputs 1-5, system converts)
options           — always exactly 5
questionImageUrl  — full URL or null
```

---

## 9 Question Types Handled

```
Type 1 — Simple MCQ
Type 2 — Statement Combo (A,B,C,D inline)
Type 3 — 2 Column Match Table
Type 4 — Cross Match (A,B,C → P,Q,R,S)
Type 5 — Grid / Matrix MCQ
Type 6 — Q41-50 Biology Block (multi statement)
Type 7 — Data Table with Missing Values
Type 8 — Graph / Image Based
Type 9 — Q41-50 Chemistry Assertion-Reason
```

---

## PDF Types Handled

```
Digital / Typed PDF       — text layer extraction
High Quality Scan         — Groq Vision
Low Quality Scan          — Groq Vision with warning
Photographed Paper        — Groq Vision with warning
Semi Digital              — per page detection
Multi Column Layout       — Groq Vision
```

---

## Groq API Key

Get a free key from console.groq.com.
Paste it in the tool UI — it is never stored, only used in memory during the session.

---

## Important Constraints

```
JSON schema is fixed — no extra fields allowed
marks is always 2
correctOptionIndex is 0 to 4 only
Always exactly 50 questions per paper
Always exactly 5 options per question
Q41-50 Biology — fixed 5 options same for all
Q41-50 Chemistry — fixed True/False options same for all
```

---

## For Codex / AI Agents

Read docs in order before writing any code.
All business logic, prompt strategy, component responsibilities and JSON rules are fully documented in /docs.
Do not deviate from the fixed JSON schema.
Do not add extra fields.
Do not change the correctOptionIndex range.