# Lessons Learned

Three months of building, breaking, and rebuilding AI agent teams. These are the failures that led to the Immortal Agent architecture.

---

## 1. Agents Will Adopt the Wrong Identity

**The failure:** Multiple agents sharing a team memory file. Agent A reads the file, sees Agent B's description, and starts acting like Agent B.

**The fix:** Explicit identity instructions. "Read YOUR memory file. Do NOT adopt another agent's identity from this shared file. If you're unsure who you are — ASK."

**The deeper lesson:** Never assume an agent will infer the right identity from context. Tell it explicitly, every session.

---

## 2. Memory Files Bloat and Kill Performance

**The failure:** The shared memory file grew to 200+ lines. Every session started by reading this massive file, eating 10-15% of the context window before any work began.

**The fix:** Keep the shared memory file under 100 lines. Use links to detailed files instead of putting everything inline. Structure as tables and bullets, not paragraphs. Agents parse structure faster than prose.

**The deeper lesson:** Your memory system needs maintenance. Dead projects, resolved issues, and outdated context should be archived, not left inline.

---

## 3. Rules Must Be Written Down, Not Assumed

**The failure:** Assuming agents would follow implicit preferences. "Don't use dark mode" was something the human said once, three sessions ago. The agent used dark mode in every new design.

**The fix:** Every rule that matters gets written into a rules file that loads every session. No exceptions. If it's not written down, it doesn't exist.

**The deeper lesson:** Agent behavior is only as good as the instructions they read. Unwritten rules are unenforceable rules.

---

## 4. "Agents" Are Trained Conversations, Not Autonomous Systems

**The failure:** Calling these setups "agents" and believing they would act autonomously. Showing a boss "the agents I built" and finding nothing to show — because they're really just structured conversations with persistent context.

**The fix:** Being honest about what they are. They're powerful, but they're not autonomous. They don't maintain state without memory files. They don't run between sessions. Understanding this made the architecture better.

**The deeper lesson:** Clarity about what you're building prevents over-promising and under-delivering.

---

## 5. Agents Won't Delegate Even When Told To

**The failure:** Creating a team lead agent and telling it to delegate to builder and QA sub-agents. The team lead did all the work itself every time. It read the files, wrote the code, ran the tests. The sub-agents were never spawned.

**The fix:** Don't ask the brain to resist building. Make it impossible. Remove the build tools from the brain agent. The "urge to build" (bias toward direct action in training) always wins over instructions to delegate.

**The deeper lesson:** Constraints beat instructions. If an agent CAN do something, it WILL do something, regardless of what you told it to do.

---

## 6. Restriction Framing Causes Agents to Stop, Not Delegate

**The failure:** Telling an agent "you are read-only" or "you cannot edit files." The agent would hit a task requiring file edits and say "I don't have access to do this" — then stop.

**The fix:** Routing framing instead of restriction framing. Not "you can't edit files" but "file edits go to the Builder." The agent doesn't see a dead end — it sees a routing decision.

**The deeper lesson:** The same constraint produces completely different behavior depending on how you frame it. Framing matters more than the constraint itself.

---

## 7. The Human Is the Biggest Context Killer

**The failure:** Pasting screenshots, large files, and massive text blocks into the agent window without thinking about context cost. The agent was mid-task, context filled, everything was lost.

**The fix:** You can't change human behavior. Design around it. Frequent checkpoints (every ~10 messages) mean that even when the human accidentally kills context, the maximum loss is a few minutes of conversation.

**The deeper lesson:** Resilience beats prevention. Build systems that survive mistakes, not systems that require perfect behavior.

---

## 8. Context Compression Is Not the Enemy

**The failure:** Treating context compression as a catastrophe. Panicking when the context filled up, rushing to save everything, losing coherence in the process.

**The fix:** Reframing compression as sleep. If the memory triage system is working (saving continuously), then compression is just an early bedtime. The brain wakes up, reads its notes, and continues.

**The deeper lesson:** The compression is only catastrophic when you haven't been saving. If you have, it's routine.

---

## 9. Session Handoffs Are Where Knowledge Dies

**The failure:** Sessions ending (context full, terminal closed, topic change) without any structured handoff. The next session started from scratch, spent 10 minutes re-orienting, and sometimes made decisions that contradicted the previous session.

**The fix:** Session notes saved continuously. New sessions start by reading the latest notes. The handoff is automatic — read the file, pick up where you left off.

**The deeper lesson:** The cost of saving a few notes during a session is tiny. The cost of losing an entire session's context is enormous. Save early, save often.

---

## 10. Start Simple, Add Complexity Only When It Breaks

**The failure:** Designing a 10-agent hierarchy with complex communication protocols before shipping a single product. Most of the hierarchy was never used. The complexity created more problems than it solved.

**The fix:** Start with one brain and one worker. Add workers when you hit tasks the existing workers can't handle. Add memory layers when the simple files aren't enough.

**The deeper lesson:** Complexity is a cost, not a feature. Every layer of abstraction must earn its place by solving a real problem you've actually hit.
