---
name: Run the SambaNova deep research agent
description: Submit a research prompt to the SambaNova deep research agent and retrieve the report.
api: openapi/sambanova-systems-agents-openapi-original.yml
operations: [deepresearch_agent_agent_deepresearch_post, download_agent_file_agent_files__file_id__get]
---

# Run the SambaNova deep research agent

The Agents service coordinates specialized subagents. Deep research produces multi-iteration reports.

## Setup
- Base URL: `https://chat.sambanova.ai/api`
- Auth: `Authorization: Bearer <API_KEY>`

## Steps
1. Call `deepresearch_agent_agent_deepresearch_post` (`POST /agent/deepresearch`) with your research prompt (fire-and-forget: returns the final report in one call). For an approval loop, use the interactive variant with a `thread_id` + `resume=true`.
2. If the response references generated artifacts, call `download_agent_file_agent_files__file_id__get` (`GET /agent/files/{file_id}`) to download them (files are scoped to your user; ownership is verified).

## Rules
- Deep research runs are long; treat them as async and poll/await accordingly.
- Auth and error handling match the Cloud API bearer model. See conventions/sambanova-systems-conventions.yml.
