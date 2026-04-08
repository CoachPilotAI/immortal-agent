# Example: Routing Decisions

These examples show how the brain routes different types of requests.

---

## Example 1: "Fix the bug in the login form"

**Brain's decision tree:**
- Is this a decision/plan/conversation? NO
- Does it require editing files? YES → Route to Builder

**Brain's action:**
1. Ask the human for details about the bug (brain work — conversation)
2. Read the login form file for context (brain work — under 3 files)
3. Spawn Builder with: "Fix [specific bug]. The login form is at src/components/Login.tsx. The issue is [description from human + what brain saw in the file]."
4. Builder returns summary: "Fixed null check on email validation. Changed 1 file."
5. Brain saves: "Login bug fixed — null check on email validation"

**Context cost to brain:** Minimal — one file read + conversation + summary.

---

## Example 2: "What's the status of the mobile app?"

**Brain's decision tree:**
- Is this a decision/plan/conversation? YES → Handle directly

**Brain's action:**
1. Read the project memory file (1 file, lightweight)
2. Answer from memory: "Mobile app is at v2.1. Last session we finished the settings page. Auth is working. Push notifications are next."

**Context cost to brain:** One small file read.

---

## Example 3: "Refactor the entire auth module to use JWT"

**Brain's decision tree:**
- Is this a decision/plan/conversation? Partially — needs planning first
- Does it require editing files? YES (eventually)
- Does it require reading many files? YES

**Brain's action:**
1. Discuss approach with human (brain work — conversation)
2. Spawn Explorer to map all auth-related files
3. Explorer returns: "8 files touch auth. Here's the list."
4. Brain plans the refactor approach (brain work)
5. Human approves approach
6. Brain saves: "Decision — refactoring auth to JWT. Approach: [summary]"
7. Spawn Builder with full plan: "Refactor these 8 files from session auth to JWT. Here's the approach: [plan]."
8. Builder returns: "Refactored 8 files. All tests pass. One breaking change in the API — middleware now expects Bearer token."
9. Brain saves: "Auth refactored to JWT. Breaking change: Bearer token required."

**Context cost to brain:** Conversation + two small summaries. The heavy 8-file refactor happened entirely in the Builder's context.

---

## Example 4: "Here's a screenshot of the bug" [image attached]

**Brain's decision tree:**
- Human sent an image — save checkpoint FIRST
- Then process minimally

**Brain's action:**
1. **Immediately** write checkpoint: "Working on [current topic]. Status: [current state]."
2. Acknowledge the image: "I see the screenshot. Looks like [brief description]."
3. Spawn a worker to analyze and fix: "The user reported a visual bug. Here's the context: [description]. Investigate and fix."
4. Worker returns summary.
5. Brain triages and saves if needed.

**Why checkpoint first:** Images are expensive context. If this triggers compression, the checkpoint ensures nothing important is lost.
