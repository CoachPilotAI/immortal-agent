# FAQ

## General

### Does this only work with Claude Code?

The architecture is designed for Claude Code but the patterns are universal. Any AI coding tool that supports:
- Persistent files (memory files the agent reads at session start)
- Sub-agent spawning (delegating tasks to child processes)
- Tool restrictions (limiting what the brain can do)

...can implement this pattern. The templates are markdown files — they work anywhere.

### How is this different from just using CLAUDE.md or MEMORY.md?

CLAUDE.md and MEMORY.md are static context files. They help with session start but don't solve:
- Context death from heavy operations mid-session
- Continuous saving of decisions as they happen
- Delegation of heavy work to preserve brain context
- Identity drift in long sessions

The Immortal Agent builds ON TOP of those files. It adds the behavioral layer (routing, triage, checkpoints) that makes the memory system actually persistent.

### Is this actually "immortal" or is that marketing?

The brain agent's context stays light because it delegates heavy work. In practice, this means the brain can run for very long sessions without hitting context limits. When it does eventually compress, the continuous saves mean it picks up seamlessly.

"Immortal" means the brain's knowledge and context survive indefinitely through persistent files. The running process still has limits — but the memory doesn't.

## Architecture

### What if the brain needs to read a large file?

Spawn an explorer agent. The explorer reads the file in its own context and returns a summary. The brain sees the summary (small), not the file (large).

Rule of thumb: if the file is under 100 lines, the brain can read it directly. Over 100 lines, delegate.

### What if I need real-time communication between agents?

This architecture is async and file-based. Agents communicate through memory files, not messages. If you need real-time agent-to-agent communication, look at LangGraph or CrewAI.

For most solo founder and small team use cases, async file-based communication is sufficient and dramatically simpler.

### Can the brain write code if it really needs to?

No. The constraint is absolute. If the brain can write code "just this once," it will write code every time. The urge to build (training bias toward direct action) always wins over instructions to delegate.

This is the core insight: constraints work because they're unconditional. Rules work only when the agent feels like following them.

### How do workers know what to do?

Each worker has a persistent identity file (like `memory/builder.md`) that contains:
- Their role and responsibilities
- Patterns and preferences
- Project context
- Rules they follow

When the brain spawns a worker, it tells them to read their identity file first. The worker orients from the file, then executes the task.

### What happens when a worker fails?

The worker returns a summary including the failure: "Attempted to deploy but got error X. Possible causes: A, B, C. Need human decision."

The brain triages: save the failure and the possible causes. Discuss with the human. Spawn a new worker with the fix.

Workers are disposable. Failure is expected and handled.

## Memory

### Won't session files get huge over time?

Yes, if you don't consolidate. The architecture includes optional weekly consolidation:
- Sessions older than 30 days get compressed into monthly archives
- Duplicate knowledge entries get merged
- Stale decisions get flagged

Run consolidation manually when files feel bloated. You'll know because session start gets slower (too much to read).

### What if the brain saves something wrong?

Session notes are just markdown files. Open them in any editor and fix them. There's no database, no API, no schema to worry about.

### How do I search past sessions?

**Simple approach:** Grep the session files. They're just text.
**Advanced approach:** Use an embedding-based search layer (Supabase pgvector, local model). This is an optional enhancement, not a core requirement.

## Practical

### How many workers do I need?

Start with one (Builder). Add more when you hit tasks your Builder can't handle well.

Common progression:
1. Builder (code implementation)
2. QA (testing and verification)
3. Specialist (domain-specific work)
4. Architect (complex multi-file analysis)

### How long does setup take?

30 minutes for the basic setup:
1. Copy templates to your project (5 min)
2. Customize the brain identity file (10 min)
3. Customize the memory file (10 min)
4. Write your rules (5 min)
5. Test with a simple delegation task (5 min)

### What if I'm not using Claude Code?

The templates are plain markdown. Adapt them for your tool:
- **ChatGPT:** Use Custom Instructions for the brain identity, paste memory context manually
- **Cursor:** Use .cursorrules for the brain identity, project files for memory
- **Aider:** Use conventions file for the brain identity
- **Any tool with file access:** Put memory files in the project and instruct the agent to read them
