# FLN Assessment Portal – Onboarding Notes

## 1. Introduction

The FLN Assessment Portal supports the assessment and evaluation of students' foundational literacy and numeracy skills.

## 2. My Contribution

I worked on the OCR response review functionality for scanned student assessment submissions.

My contribution includes:

- Persisting OCR-extracted student responses.
- Storing extracted text, OCR confidence, provider information, page number, and bounding-box information.
- Identifying blank, unclear, unreadable, or low-confidence responses that require teacher review.
- Supporting response updates while preserving responses that have already been reviewed.

## 3. Review Logic

The `computeRequiresReview` function determines whether an extracted response requires teacher review.

A response is flagged when:

- The extracted text is blank.
- The text indicates an unclear or unreadable response.
- The OCR confidence is below `0.6`, when a valid confidence score is provided.

Readable responses with sufficient confidence are not automatically flagged by this rule.

## 4. Testing

I added tests for the review-flagging logic.

All four tests passed locally, covering:

- Blank responses.
- Ambiguous or unreadable responses.
- Low-confidence responses.
- Readable responses with sufficient confidence.

The test is registered in `backend/package.json` as `test:ocr-response-review`.

## 5. Relevant Files

- `backend/src/services/scanExtraction.ts` – OCR response persistence and review logic.
- `backend/src/services/scanExtraction.test.ts` – Tests for review-flagging logic.
- `backend/src/db.ts` – Database types and persistence methods related to extracted responses.
- `backend/src/routes/evaluation.ts` – Evaluation route changes related to scan submissions.
- `backend/package.json` – OCR review test command.

## 6. Gaps Observed in the Repository

During implementation, I identified areas that require further testing and validation:

1. **Persistence testing:** The current OCR test file tests `computeRequiresReview`, but does not directly test response creation, updating pending responses, or preserving reviewed responses.
   - File: `backend/src/services/scanExtraction.test.ts`
   - File: `backend/src/services/scanExtraction.ts`, lines 73–115.

2. **Database workflow:** Extracted-response database methods are implemented, but their create, update, and retrieval behaviour needs dedicated automated testing.
   - File: `backend/src/db.ts`, lines 1917–1958.

3. **Integration validation:** The evaluation routes support optional scan-submission tracking, but the complete OCR-to-evaluation workflow needs further integration testing.
   - File: `backend/src/routes/evaluation.ts`, lines 579–637 and 1001–1012.

These are areas requiring additional validation, not confirmed production failures.

## 7. Current Scope and Limitations

My contribution focuses on OCR response persistence and review handling. The four review-logic tests pass locally. The complete OCR workflow and its integration with the database and evaluation routes require further validation before the entire workflow can be considered fully verified.