---
name: Generate a chat completion with SambaNova
description: Call a SambaNova-hosted open model for a chat completion, with streaming and tool calls.
api: openapi/sambanova-systems-cloud-openapi-original.yml
operations: [createChatCompletion, getModelList]
---

# Generate a chat completion with SambaNova

SambaNova Cloud is OpenAI-compatible. Point any OpenAI client at the base URL and use your API key.

## Setup
- Base URL: `https://api.sambanova.ai/v1`
- Auth: `Authorization: Bearer <API_KEY>` (generate keys at https://cloud.sambanova.ai/apis).

## Steps
1. (Optional) Call `getModelList` (`GET /models`) to discover currently available model IDs (e.g. `Meta-Llama-3.3-70B-Instruct`, `DeepSeek-V3.1`, `gpt-oss-120b`, `MiniMax-M2.7`).
2. Call `createChatCompletion` (`POST /chat/completions`) with `model` and a `messages[]` array of `{role, content}` (roles: `system`, `user`, `assistant`).
3. For token-by-token output, set `stream: true` and read server-sent-event chunks; each chunk may carry multiple tokens.
4. Read `choices[0].message.content`; check `usage` for `prompt_tokens`/`completion_tokens`/`total_tokens` (and `cached_tokens` when prompt caching applies).

## Rules
- Watch rate-limit headers (`x-ratelimit-remaining-requests`, `x-ratelimit-remaining-requests-day`); on `429` (`insufficient_quota`/`queue_full`) back off and retry.
- On `410` (`model_deprecated`) switch to a supported model — see lifecycle/sambanova-systems-lifecycle.yml.
- Errors follow the OpenAI error object with a `request_id`; log it for support. See errors/sambanova-systems-error-codes.yml.
