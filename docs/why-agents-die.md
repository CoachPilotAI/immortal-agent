# Why AI Agents Die

## The Context Window Problem

Every AI agent operates within a context window — a fixed amount of text it can "see" at once. For Claude, this is roughly 200K tokens. Sounds like a lot. It's not.

A single large file read can consume 5-10K tokens. A code generation response can use 2-5K. A screenshot or image can use 10-50K. Error logs, command outputs, search results — they all eat context.

In a heavy coding session, you can fill 200K tokens in under an hour.

## What Happens When Context Fills

When the context window fills, the system compresses earlier messages. Details are lost. Decisions you made 30 minutes ago become fuzzy. The agent starts asking questions you already answered. It forgets the plan you agreed on.

This is "agent death" — not a crash, but a gradual loss of coherence until the agent is functionally useless and needs to be restarted.

## Why Bigger Context Windows Don't Fix This

Bigger windows just delay the crash. They don't prevent it. And they come with their own problems:

- **Cost scales with context** — larger windows are more expensive per message
- **Attention degrades** — models perform worse with very long contexts (the "lost in the middle" problem)
- **Speed decreases** — longer contexts mean slower responses
- **The crash is worse** — when it finally comes, there's MORE context to lose

## The Real Problem: No Memory Between Sessions

Even if context never filled up, agents still start fresh every session. Close the terminal, open it again, and the agent knows nothing about what you did yesterday.

This means:
- Re-explaining your project structure every session
- Re-stating your preferences every session
- Re-building context about decisions you already made
- Losing lessons learned from previous failures

The combination of within-session context death and between-session amnesia is why working with AI agents feels like training a new employee every day.

## What the Immortal Agent Solves

1. **Within-session:** The brain stays light by delegating heavy work, so context fills slowly or not at all
2. **Between-session:** Continuous memory triage saves decisions and context to persistent files that survive any session
3. **Compression:** Context compression becomes "sleep" — a harmless reset because important stuff is already saved
4. **Recovery:** New sessions start by reading saved notes, not by re-explaining from scratch
