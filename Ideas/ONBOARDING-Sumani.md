\# Onboarding Notes – Sumani



\## 1. Project Overview



The FLN Assessment Portal supports the assessment and evaluation of students' foundational literacy and numeracy skills.



\## 2. My Contribution



I worked on the OCR response review functionality for scanned student assessment submissions.



My work focuses on:

\- Persisting OCR-extracted student responses.

\- Storing extracted text, OCR confidence, provider information, page number, and bounding-box information.

\- Identifying blank, unclear, unreadable, or low-confidence responses that require teacher review.

\- Supporting response updates while preserving responses that have already been reviewed.



\## 3. Review Logic



The `computeRequiresReview` function determines whether an extracted response requires review.



A response is flagged when:

\- The extracted text is blank.

\- The text indicates an unclear or unreadable response.

\- The OCR confidence is below `0.6`, when a valid confidence score is provided.



Readable responses with sufficient confidence are not automatically flagged by this rule.



\## 4. Testing



I added tests for the review-flagging logic. The four tests passed locally, covering blank responses, ambiguous responses, low-confidence responses, and readable responses with sufficient confidence.



\## 5. Relevant Files



\- `backend/src/services/scanExtraction.ts` – OCR response persistence and review logic.

\- `backend/src/services/scanExtraction.test.ts` – Tests for review-flagging logic.

\- `backend/src/db.ts` – Database types and persistence methods related to extracted responses.

\- `backend/src/routes/evaluation.ts` – Evaluation route changes related to scan submissions.



\## 6. Current Scope



My contribution is focused on OCR response persistence and review handling. Further integration testing and validation should be completed before claiming the entire OCR workflow is fully verified.

