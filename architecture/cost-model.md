# Cost Model

## Design Principle

Zero idle cost. You only pay when you're working.

## Core Architecture: $0

The core immortal agent architecture costs nothing beyond your existing AI subscription:

| Component | Cost | Why |
|-----------|------|-----|
| Brain agent | $0 | Just conversation in your existing tool |
| Memory files (markdown) | $0 | Local files on your machine |
| Worker spawns | $0 | Part of your existing AI tool usage |
| Session saves | $0 | File writes to local disk |

**Total core cost: $0/month**

This is the zero-infrastructure promise. No databases. No hosted services. No API keys beyond what you already use. Just markdown files and agents that know how to read them.

## Optional Enhancements

If you want to add searchable long-term memory or automated consolidation:

| Enhancement | Trigger | Approximate Cost |
|-------------|---------|-----------------|
| Embedding-based search | On query | ~$0-2/month |
| Daily brief generation | Manual | ~$0.06/run |
| Weekly consolidation | Manual | ~$0.11/run |
| Pattern detection | Manual | ~$0.08/run |

**Key decision:** All optional features are manually triggered. No cron jobs. No automatic API spend. You run them when you want them.

## Comparison

| Approach | Monthly Cost | Infrastructure |
|----------|-------------|---------------|
| **Immortal Agent (core)** | **$0** | **None — just files** |
| Immortal Agent (full) | ~$3-5 | Supabase free tier |
| Mem0 | $0-99 | Hosted service |
| Letta/MemGPT | $0 + hosting | Self-hosted server |
| LangGraph Cloud | $0-200+ | LangSmith platform |
| Custom RAG pipeline | $10-50+ | Vector DB + embedding API |

The immortal agent achieves persistent memory at a fraction of the cost because it doesn't require infrastructure. The tradeoff: it's file-based and async, not a real-time API. For solo founders and small teams, that tradeoff is worth it.
