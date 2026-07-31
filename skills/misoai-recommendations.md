---
name: Serve personalized recommendations
description: Return conversion-driving product recommendations for a user or an anchor product.
api: openapi/misoai-openapi-original.json
operations:
  - user_to_products_v1_recommendation_user_to_products_post
  - product_to_products_v1_recommendation_product_to_products_post
  - trending_items_v1_recommendation_user_to_trending_post
---

# Serve personalized recommendations

## Auth
- Base URL: `https://api.askmiso.com`; publishable key allowed for read-only recs (hash `user_id`).

## Steps
1. **For a user** — `POST /v1/recommendation/user_to_products?api_key=KEY` (`user_to_products_v1_recommendation_user_to_products_post`). Send `user_id`; returns products most likely to drive the conversion metric your Engine was trained on (`add_to_cart`, `checkout`, `read`).
2. **For an anchor product** — `POST /v1/recommendation/product_to_products?api_key=KEY` (`product_to_products_v1_recommendation_product_to_products_post`). Send a `product_id` (e.g. the product currently viewed); returns related, conversion-likely products.
3. **Trending for a user** — `POST /v1/recommendation/user_to_trending?api_key=KEY` (`trending_items_v1_recommendation_user_to_trending_post`). Returns currently-trending products of interest to the user.

## Conventions
- Page with `start` / `rows`; choose returned fields with `fl`; filter with `fq`.
- Recommendation quality depends on having ingested products, users, and interactions first (see `skills/misoai-ingest-catalog.md`).
