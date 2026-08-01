---
name: Create embeddings with SambaNova
description: Turn text into vector embeddings for search and RAG using SambaNova Cloud.
api: openapi/sambanova-systems-cloud-openapi-original.yml
operations: [createEmbedding, getModelList]
---

# Create embeddings with SambaNova

## Setup
- Base URL: `https://api.sambanova.ai/v1`
- Auth: `Authorization: Bearer <API_KEY>`

## Steps
1. (Optional) Call `getModelList` (`GET /models`) and pick an embeddings-capable model.
2. Call `createEmbedding` (`POST /embeddings`) with `model` and `input` (a string or array of strings).
3. Read `data[].embedding` vectors; store them in your vector database keyed to the source text.
4. Use the same model to embed queries at retrieval time so vectors are comparable.

## Rules
- Batch inputs where possible to stay under RPM/RPD rate limits.
- Errors use the OpenAI error object with `request_id`; on `400 context_length_exceeded` shorten the input. See errors/sambanova-systems-error-codes.yml.
