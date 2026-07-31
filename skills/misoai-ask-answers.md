---
name: Answer questions from your content (Ask)
description: Submit a question to Miso's Ask/Answers API and poll for the LLM-generated, citation-backed answer grounded in your own content.
api: openapi/misoai-openapi-original.json
operations:
  - questions_v1_ask_questions_post
  - questions_answer_v1_ask_questions__question_id__answer_get
---

# Answer questions from your content (Ask)

Miso Answers generates answers built only on the customer's own content (reducing hallucination), with citations.

## Auth
- Base URL: `https://api.askmiso.com`

## Steps
1. **Submit a question** — `POST /v1/ask/questions?api_key=KEY` (`questions_v1_ask_questions_post`). Send the user's question; the response returns a `question_id`.
2. **Get the answer** — `GET /v1/ask/questions/{question_id}/answer?api_key=KEY` (`questions_answer_v1_ask_questions__question_id__answer_get`). Fetch the latest generated answer for that `question_id`. Answers are produced asynchronously — poll this endpoint until the answer is complete.

## Notes
- Answers are grounded in the products/content you ingested (`skills/misoai-ingest-catalog.md`); richer catalogs yield better answers.
- The embeddable **Ask** UI module wraps this flow for the browser (see `components/misoai-components.yml`).
- Errors return `{ "errors": true, "message": ..., "data": ... }` (see `errors/misoai-problem-types.yml`).
