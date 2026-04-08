# Architecture Overview

## The Core Insight

An agent can live forever if its context never fills up.

Context fills from heavy operations: file reads, code generation, tool outputs, image processing. Conversation and decisions barely touch it. If the brain agent physically cannot perform heavy operations, its context stays light indefinitely.

## The Human Memory Model

| Human Memory | Agent Equivalent | How It Works |
|-------------|-----------------|-------------|
| Working memory | Context window | Active thoughts — limited capacity, fast access |
| Short-term memory | Session notes | Important bits saved throughout the day as they happen |
| Sleep | Context compression | Consolidation — harmless reset because important stuff is already saved |
| Long-term memory | Knowledge base | Permanent storage — searchable, consolidated, curated |
| Forgetting | Intentional dropping | Not everything makes it to long-term. That's a feature, not a bug. |

### Why This Matters

Most AI memory systems treat session end as the save point — like a human trying to remember their entire day right before falling asleep. You lose things.

The immortal agent saves continuously, like a human brain encoding memories throughout the day. Context compression (sleep) becomes harmless because the important stuff is already stored.

## The Two-Layer Architecture

### Layer 1: The Brain (Immortal)

One agent that only thinks. No build tools. No file editing. No bash commands. Just:
- Read files (up to 3, for quick context)
- Spawn worker agents (for everything else)
- Write to memory files (to save decisions and session notes)
- Converse with the human (strategy, planning, decisions)

**Why it lives forever:** It never does the things that fill context. Heavy file reads happen in worker contexts. Code generation happens in worker contexts. The brain only sees summaries.

### Layer 2: Workers (Disposable)

Specialized agents spawned by the brain for specific tasks. Each worker:
- Has full tool access (Edit, Write, Bash, everything)
- Runs in its own context (fills up independently)
- Returns a short summary when done (3-5 lines)
- Dies when done (context is released)

The brain triages the summary: save what matters, drop the rest.

## Why "Routing, Not Restriction"

When you tell an agent "you cannot edit files," it interprets this as "editing files is impossible." It stops and reports failure.

When you tell an agent "file edits go to the Builder agent," it interprets this as "I know who handles this." It delegates and continues.

Same constraint. Completely different behavior. The framing determines whether the agent stops or routes.

This is the single most important pattern in the architecture.
