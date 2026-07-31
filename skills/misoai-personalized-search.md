---
name: Add personalized search and autocomplete
description: Serve personalized, typo-tolerant semantic search and typeahead over your Miso catalog.
api: openapi/misoai-openapi-original.json
operations:
  - search_v1_search_search_post
  - autocomplete_v1_search_autocomplete_post
  - mget_v1_search_mget_post
---

# Add personalized search and autocomplete

## Auth
- Base URL: `https://api.askmiso.com`
- Front-end search may use the **publishable** key on `api_key`; hash the `user_id`.

## Steps
1. **Autocomplete** — `POST /v1/search/autocomplete?api_key=KEY` (`autocomplete_v1_search_autocomplete_post`). Send what the user is typing (`q`) plus the `user_id`; get completed query suggestions.
2. **Search** — `POST /v1/search/search?api_key=KEY` (`search_v1_search_search_post`). Send the query `q` and `user_id`. Personalized, typo-correcting, semantic results tailored to the user.
3. **Fetch by id** — `POST /v1/search/mget?api_key=KEY` (`mget_v1_search_mget_post`). Send `{ "product_ids": ["...", "..."] }` to hydrate specific products.

## Conventions
- **Pagination** is offset-based: `start` (offset) + `rows` (page size).
- **Field selection**: `fl` lists the product fields to return.
- **Filtering**: `fq` is a Solr-syntax filter query to restrict results.
- Errors return `{ "errors": true, "message": ..., "data": ... }` (see `errors/misoai-problem-types.yml`).
