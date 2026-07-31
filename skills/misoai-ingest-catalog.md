---
name: Ingest your catalog, users, and interactions
description: Load the three data sets Miso trains its Engines on — products/content, users, and interaction events.
api: openapi/misoai-openapi-original.json
operations:
  - content_write_api_v1_products_post
  - user_write_api_v1_users_post
  - interaction_upload_api_v1_interactions_post
---

# Ingest your catalog, users, and interactions

Miso trains personalization Engines on three data sets. Load them before calling search, recommendation, or Ask endpoints.

## Auth
- Base URL: `https://api.askmiso.com`
- Use your **secret** API key on the `api_key` query parameter (server-side only). Never expose the secret key in browser code.

## Steps
1. **Upload products / content** — `POST /v1/products?api_key=SECRET` (`content_write_api_v1_products_post`). Send `{ "data": [ { "product_id": "...", ... } ] }`. This is a bulk upsert keyed by `product_id`.
2. **Upload users** — `POST /v1/users?api_key=SECRET` (`user_write_api_v1_users_post`). Send `{ "data": [ { "user_id": "...", ... } ] }`, upserted by `user_id`.
3. **Stream interactions** — `POST /v1/interactions?api_key=KEY` (`interaction_upload_api_v1_interactions_post`). Log events (view, add_to_cart, checkout, read) linking a `user_id` to `product_ids`. The **publishable** key may be used here from the browser (hash the `user_id`).

## Rules
- Bulk write endpoints validate every record and may reject the **whole batch** if any record has a schema error — inspect the `data` field of the error envelope for per-record detail (see `errors/misoai-problem-types.yml`).
- There is no request-level idempotency key; writes dedupe naturally by `product_id` / `user_id` (see `conventions/misoai-conventions.yml`).
