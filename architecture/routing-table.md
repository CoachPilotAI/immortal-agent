# Routing Table

## How the Brain Delegates

The brain maintains a routing table — a mapping from task types to worker agents. When a task arrives that requires building, the brain doesn't think about whether to delegate. It looks up who handles this type of work and spawns them.

## Example Routing Table

| Task Type | Route To | Worker Type |
|-----------|----------|-------------|
| Write code / edit files | Builder | Full-access general agent |
| Architecture / multi-file analysis | Architect | Full-access general agent |
| QA / testing / design | QA Agent | Full-access general agent |
| Quick file search | Explorer | Read-only explore agent |
| Bash commands / deploys | Ops Agent | Full-access general agent |
| Domain-specific work | Specialist | Full-access general agent |

## Spawn Template

When the brain spawns a worker, it provides:

```
You are [Worker Name]. Read memory/[worker-name].md for your identity and context.

Task: [specific description of what to do]

When done, return:
1. What you did (2-3 sentences)
2. What files changed
3. Any decisions needing approval
4. Any blockers
5. Any lessons worth saving
```

## The Summary Contract

Workers don't return their full output. They return a **summary** — 3-5 lines covering what happened. The brain triages the summary and saves what matters.

This is critical. If workers return full file contents or long logs, that defeats the purpose — the brain's context fills up from reading worker output.

**Good worker return:**
```
Created auth middleware in src/middleware/auth.js. Added JWT
validation with refresh token support. Need your decision on
token expiry — 1 hour or 24 hours? No blockers.
```

**Bad worker return:**
```
[200 lines of code]
[Full file contents]
[Every command I ran and its output]
```

## Customizing Your Routing Table

Your routing table should reflect your actual team:

1. **List your worker types** — What roles do you need? (Builder, QA, Designer, DevOps, etc.)
2. **Map task categories** — Which types of work go to which worker?
3. **Create identity files** — Each worker gets a persistent memory file with their role, patterns, and context
4. **Write spawn templates** — Pre-written prompts that the brain uses to spawn each worker type

Start with 2-3 workers. Add more only when you hit a task that none of your existing workers handle well.
