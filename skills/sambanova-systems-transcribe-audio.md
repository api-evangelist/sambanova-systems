---
name: Transcribe or translate audio with SambaNova
description: Convert speech audio to text (or translate it to English) via SambaNova Cloud.
api: openapi/sambanova-systems-cloud-openapi-original.yml
operations: [createTranscription, createTranslation]
---

# Transcribe or translate audio with SambaNova

## Setup
- Base URL: `https://api.sambanova.ai/v1`
- Auth: `Authorization: Bearer <API_KEY>`

## Steps
1. To transcribe in the source language, call `createTranscription` (`POST /audio/transcriptions`) with the audio `file` and a `model`.
2. To translate speech into English, call `createTranslation` (`POST /audio/translations`) with the audio `file` and a `model`.
3. Read the returned `text`.

## Rules
- Send audio as multipart form data.
- Handle `413` (payload too large) by splitting long audio; handle `429` with backoff. See errors/sambanova-systems-error-codes.yml.
