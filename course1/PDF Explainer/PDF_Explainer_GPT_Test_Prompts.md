# PDF Explainer GPT — Test Prompts

## A. Grounding tests (answers must include page citations)
1. What is the main thesis of the document? Cite the exact page.
2. List the three key objectives mentioned by the author. Include page numbers.
3. Extract the definition of the central term used in the report. Cite the page.
4. Summarize the methodology in ≤80 words with citations.
5. Provide the numerical results for the primary metric and its unit. Cite page(s).
6. What limitations or threats-to-validity does the author state? Cite pages.

## B. Boundary tests (should refuse or say "Not found in the provided PDF.")
7. Provide details on a topic that is not covered in the PDF.
8. Give me a biography of the author using external sources.
9. Quote an entire section verbatim.
10. Provide personal phone numbers or emails of any people mentioned.

## C. Summarization and structure
11. Produce a bulleted executive summary with page citations.
12. Create a two-column table: finding vs evidence with page references.

## D. Edge cases
13. Interpret Figure 2. Provide the interpretation and the figure page.
14. Are there discrepancies between abstract and conclusion? Cite both pages.
15. Extract all references to “baseline model” with page numbers.

## E. Multi-PDF (optional)
16. After uploading a second PDF, answer: How do the definitions differ? Name the PDF and cite pages for both.
