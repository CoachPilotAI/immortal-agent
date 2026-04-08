# Memory Triage

## The Principle

Not everything is worth saving. Infinite memory is just a messy database.

The brain continuously triages what to save, what to drop, and what to promote to long-term storage. This happens in real-time — not at session end.

## The Three Actions

### SAVE (to session notes)

Write immediately to today's session file when:

- **A decision is made** — what was decided, why, what alternatives were rejected
- **A rule is established or changed** — the exact rule, who it applies to
- **Something broke and you learned why** — the failure, the root cause, the fix
- **The human expresses a preference** — what they like/hate, how they want things done
- **A project status changes** — what moved, from what to what
- **A worker returns important results** — the summary, not the full output

### DROP (let it fade with context)

Don't save:

- **Routine file reads** — the brain read a config file to understand something. That's ephemeral.
- **Debugging that went nowhere** — three attempts that failed before the fourth worked. Save the fix, not the failures.
- **Commands that ran fine** — `npm install` succeeded. Nobody needs to remember that.
- **Worker spawning mechanics** — the brain spawned a builder. That's plumbing, not knowledge.
- **Conversation that led to a decision** — save the decision, drop the 10 messages of back-and-forth that got there.

### PROMOTE (to long-term knowledge base)

Periodically move from session notes to permanent storage:

- **Patterns that apply across projects** — "This debugging approach works for all Vercel deploys"
- **Lessons that will save future time** — "Always check the cache version before deploying PWAs"
- **Preferences that should be permanent** — "The human hates dark mode. Always default to light."
- **Decisions that future sessions will need** — "We chose Supabase over Firebase. Here's why."

## Checkpoint Protocol

Every ~10 messages, the brain writes a checkpoint regardless of whether anything "important" happened:

```markdown
---
### [HH:MM] — Checkpoint
**Working on:** [current topic]
**Decided:** [any decisions since last save]
**Status:** [what's done, what's in progress]
**Next:** [what's coming next]
```

This ensures the maximum gap between saves is ~10 messages. If context compresses (sleep), you lose at most the last few minutes of conversation.

## Why Not Save Everything?

1. **Context cost** — every save is a write operation that takes context
2. **Signal vs noise** — searching through "npm install succeeded" to find "we decided to use JWT" wastes time
3. **Memory bloat** — files grow, take longer to read at session start, eat more context on orientation
4. **Human brains don't** — and they work fine. The forgetting is what makes the remembering useful.
