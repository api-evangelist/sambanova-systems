---
title: "MiniMax M3 Prompt Caching on SambaCloud: How It Works"
url: "https://sambanova.ai/blog/introducing-prompt-caching-for-minimax-m3-on-sambacloud"
date: "2026-10-07"
author: "SambaNova"
feed_url: "https://sambanova.ai/blog/rss.xml"
---
Prompt caching, first introduced on SambaCloud with MiniMax M2.7 , is now available for MiniMax M3. When requests share a stable prefix of at least 4,096 tokens, SambaCloud can serve that prefix from cache instead of recomputing it, with no code changes required. Cached tokens are billed at 90% below the standard input rate, and across 8k to 192k tokens of context, cache hits cut time to first token (TTFT) by 35% to 88%.
