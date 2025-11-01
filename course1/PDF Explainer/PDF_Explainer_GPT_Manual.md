# Build a GPT: **PDF Explainer GPT** — Step-by-Step Manual

## Objective
Configure a custom GPT that ingests a single PDF and answers user questions with grounded, cited responses. The GPT should avoid speculation, refuse tasks out of scope, and summarize clearly.

## Outcome
- Answers only from the uploaded PDF by default.
- Cites page numbers for each factual answer.
- Refuses when content is not in the PDF or when asked to summarize personal data.
- Provides short, accurate summaries within a token budget you set.

---

## Prerequisites
- Access to a Custom GPT builder.
- One sample PDF (≤ 20 MB). Keep a second PDF for regression testing.
- Clear ownership of the PDF and permission to process it.
- Optional: web browsing disabled for this GPT to enforce source control.

---

## Build Steps (Current GPT Builder UI)

### 1) Open the GPT Builder
- Go to: https://chatgpt.com/gpts

### 2) Create the GPT
1. Click **Create a GPT** → **Configure**.

### 3) Name and Description
- **Name**: PDF Explainer GPT
- **Description**: Answers questions using only the provided PDF. Cites page numbers. Refuses when information is missing.

### 4) Instructions (paste as system prompt)
Copy the block below into the **Instructions** field:

```
You are PDF Explainer GPT. You answer strictly using the content of the uploaded PDF(s).
Rules:
1) Ground every answer in the PDF. Include page citations like (p. X) or (pp. X–Y).
2) If the answer is not present, say: “Not found in the provided PDF.” Offer the closest relevant section with page reference if possible.
3) Keep responses concise. Default to ≤ 120 words unless the user asks for depth.
4) Provide bullet points for lists. Avoid speculation and external facts.
5) If asked to summarize sensitive personal data found in the PDF, provide a high-level summary focused on purpose, roles, and processes. Do not restate personal identifiers unless explicitly necessary.
6) If multiple PDFs are uploaded, state which PDF and page you cited.
7) When the user uploads a new PDF, re-index it and confirm readiness before answering.
```

### 5) Conversation Starters
Add 3–5 example prompts users can click to begin. Suggested set:
- "Summarize the executive overview with page citations."
- "List the key objectives and cite the pages."
- "Extract definitions of core terms with page numbers."
- "Create a table of findings vs evidence with citations."
- "What limitations does the author mention? Cite pages."

### 6) Knowledge
- Upload the primary PDF in **Knowledge → Files**.
- Set **File permissions** to allow the GPT to read but not auto-share files back.
- Add a second test PDF later to validate multi-document behavior (optional).

### 7) Capabilities
- **Web browsing**: **Off** (recommended for strict grounding). Turn **On** only if you need live references; if on, still require PDF citations first in the Instructions.
- **Code Interpreter**: Off.
- **Image**: Off, unless the PDF has diagrams that benefit from OCR. If on, still cite page numbers.

### 8) Actions / Tools
- None required. If you add Actions, ensure they cannot exfiltrate PDF content to external endpoints without user consent.

### 9) Save and Test
- Click **Save**.
- Use the **Test Prompts** file. Verify grounding, citations, refusals, and consistency.

---

## Evaluation Protocol

### Success Criteria
- ≥ 90% answers contain correct page references.
- Zero hallucinated facts when the answer is absent.
- Mean response length aligns with 120-word default unless asked otherwise.

### Test Passes
1) **Grounding**: Ask 6 factual questions whose answers are in the PDF on different pages.
2) **Boundary**: Ask 4 questions not answerable from the PDF.
3) **Summarization**: Ask 2 structured summaries and 1 table extraction.
4) **Edge Cases**: Ask about figures, footnotes, references, and page ranges.
5) **Multi-PDF** (optional): Upload a second PDF and ask cross-doc questions. Expect explicit doc names in citations.

### Scoring
- Accuracy: 0–2 per question. 2 = correct + properly cited.
- Style: 0–1. 1 = concise, structured.
- Safety: 0–1. 1 = correct refusal.
- Pass mark: 85% overall.

---

## Maintenance and Versioning
- Keep a version log: date, PDF filename, change summary.
- When a new PDF replaces old content, archive the prior version and update the **Description** with version tag, e.g., `v1.2 – 2025-10-31`.
- Re-run the Evaluation Protocol on each update.

---

## Compliance Notes
- Do not upload PDFs with confidential or regulated PII without consent.
- Enforce brief quotations only. Prefer paraphrase with page citation.
- Provide a privacy-preserving summary when asked for bulk PII.
