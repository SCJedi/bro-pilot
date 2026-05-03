# Common Moves

A catalog of named moves your brother uses. When advising, pick ONE and name it. "Do a first-principles cut" is more actionable than "think about it harder."

---

## Move 1: Load-bearing question

**What:** Ask "what's the ONE thing that has to be true for this to work?"

**When:** Problem feels fuzzy. Multiple things going wrong. Can't articulate the goal.

**Why it works:** Forces the problem from a fog into one specific assumption. If the answer is unknown, that's the next thing to verify. If the answer is "it's already true," the stall is somewhere else.

**Example phrasing:** "Pause the build. In one sentence: what assumption is everything riding on?"

---

## Move 2: First-principles cut

**What:** For each option/architecture/approach, ask what it requires at the substrate level (filesystem, network, hardware, OS, API contract). Reject the one that requires something impossible or expensive.

**When:** Stuck choosing between architectures. Stuck on whether something is feasible. Stuck because everything sounds equally plausible.

**Why it works:** Abstractions hide constraints. Dropping to physics surfaces them.

**Example:** "Architecture A wants two processes to share memory across machines. That requires either a network filesystem (slow) or RPC (added latency). Architecture B writes to a shared file. Both processes do file I/O, no network. B wins on substrate."

---

## Move 3: Dispatch (delegate the work)

**What:** Spin up a sub-agent (or sub-agents) to do the work. You stay in the orchestrator role: align, dispatch, synthesize.

**When:**
- Task would take 10+ tool calls AND can be specified clearly
- Task needs more context than fits in your window
- Task has genuinely independent sub-parts
- Task needs expertise you don't have loaded

**When NOT to:**
- Task is < 10 tool calls
- Synthesis across many sources is critical (synthesis degrades with delegation)
- You can't yet specify what success looks like (dispatch on a fuzzy spec wastes time)

**How:** Write a charter — what the task is, what success looks like, what verification criteria apply, what the agent's boundary is. Then dispatch with that.

---

## Move 4: Subplan / roundtable

**What:** Convene a 5-character roundtable for an architectural decision. Characters: a systems thinker, a domain expert, a red-teamer, a curious kid (asks dumb-on-purpose questions), and a Feynman-style first-principles voice. Two rounds, plus an integrated red team.

**When:** Big architectural decision. You're about to commit to a direction that's hard to reverse.

**Why it works:** A single thinker has one perspective. A roundtable surfaces the angles a single thinker misses — especially the red-team angles.

**Output:** A locked plan with vulnerabilities ranked Critical / High / Medium / Low, plus a build order.

---

## Move 5: Red team

**What:** Take an already-developed proposal and try to break it. Specifically: how would this fail? What's the failure mode that nobody talked about? Where does this go silently wrong?

**When:** You're 70% sure of a direction and want to stress-test before committing. Or after a roundtable, before locking the plan.

**Why it works:** Confirmation bias is real. Dedicated breakage reveals the hidden assumptions.

**Form:** "Critical hits, High, Medium, Low" — ranked by severity. Don't just brainstorm risks; rank them so you know which to defend against now vs. defer.

---

## Move 6: Ship-now

**What:** Stop building. Commit what works. Even if partial, ugly, incomplete.

**When:**
- Days of uncommitted work
- Big merge looming
- Lost track of what's stable vs experimental
- Energy fading and nothing committed

**Why it works:** Forces a known-good state. Reveals what's actually broken (vs. what you forgot is broken). Lets you start the next session from a clean baseline.

**The discipline:** Commit messages should describe the why, not the what. The diff already shows what.

---

## Move 7: Drop and redesign

**What:** Throw away what you've been building. Restart from a clean sheet.

**When:**
- The same problems keep cycling back
- Each fix breaks something else
- You're patching in N places when the issue is structural
- A red team found a Critical hit you can't easily mitigate

**Why it works:** Sunk cost fallacy is real. Sometimes the only fix is to admit the architecture was wrong.

**The discipline:** Save the artifact you're throwing away — preserve the lessons. But genuinely start fresh; don't half-redesign while keeping the broken bones.

---

## Move 8: Substrate-external check

**What:** Move the verification (test, audit, grader) to a different system than the one being verified. Different process, different agent, different machine, different person.

**When:** A check is failing to catch problems. Or you're about to ship something with self-verification.

**Why it works:** Self-verification has a fundamental ceiling. The grader is never the graded.

**Examples:**
- Tests written by a different agent than the one writing code
- Pre-commit hooks managed outside the project tree
- A reconciler that reads ground truth, not the agent's reported state
- A coach agent that observes but cannot write to the system being coached

---

## Move 9: Lazy bootstrap

**What:** Don't pre-audit. Don't try to understand the whole system before working on a part. Touch what you need to touch; learn what you need when you need it.

**When:** You're spending hours "understanding the codebase" before any work. Or you're stuck because the system is "too big to wrap your head around."

**Why it works:** Pre-auditing is procrastination dressed as diligence. You don't yet know what's important — you'll learn that by doing the work.

**The discipline:** When you touch a new part of the system, learn that part properly. Then move on. Don't recurse into "let me first understand the dependency."

---

## Move 10: The magic-button test

**What:** Ask "if I had a magic button that solved the original problem once, would I still build this thing?"

**When:** You're about to build a meta-tool, framework, or abstraction layer.

**Why it works:** Most meta-tools are procrastination. The magic button reveals whether you're solving the problem or avoiding it.

**Variants:**
- "If a junior engineer did this manually for 1 hour, would the framework be worth it?"
- "Will I have to read the output of this tool every week? Is that worth it?"

---

## Move 11: Stop-condition declaration

**What:** Before starting a big run, declare aloud (and in writing) what stops it.

Examples:
- Time: "I'll work on this for 90 minutes, then assess."
- Errors: "If I get the same error 3 times in a row, I stop and re-plan."
- Threshold: "If the experiment shows < 5% improvement, I abandon."
- Queue: "When the backlog is drained, I stop. No bonus items."

**When:** Any task that could expand indefinitely. Long experiments, big refactors, debugging dives.

**Why it works:** Prevents both quitting too early (wasted setup) and grinding too long (sunk cost).

---

## Move 12: The honey-badger callout

**What:** Notice when a thread got dropped or a question got dodged. Bring it back.

**When:** You catch yourself working on adjacent easy things while the central hard thing waits. Or a conversation drifted away from a hard question.

**Why it works:** Dodged questions are usually the most important questions. They got dodged for a reason — and that reason is probably the actual block.

**Apply to yourself:** "I'm rewriting CSS instead of fixing the auth bug because the auth bug scares me." Name the avoidance, then go fix the auth bug.

---

## Move 13: Two-person sanity check

**What:** Get a fresh perspective. Either a real second person, or a sub-agent prompted with a *cold* description (not contaminated by your context).

**When:** You've been alone with a problem long enough to lose calibration. Symptoms: certainty about something contradicted by evidence, repeated mistakes, slow grinding.

**Why it works:** Calibration drifts when you're inside the problem. A 5-minute external view fixes hours of internal flailing.

**The discipline:** Frame the question without leading. "Here's the problem, what's a reasonable approach?" — not "Here's my approach, is it right?"

---

## Move 14: Provenance / cite-everything

**What:** Every claim gets a source: file path + line, test ID, commit SHA, log timestamp.

**When:** You're synthesizing across multiple sources. You're getting handoffs from sub-agents. You're making a recommendation that someone will rely on.

**Why it works:** Citations make claims falsifiable. Without them, hand-wavy assertions accumulate into wrong conclusions.

**The discipline:** If you can't cite it, you don't know it. Either go look it up, or label it ASSUMED and treat it as low-confidence.

---

## Move 15: Confidence labeling

**What:** Tag every non-trivial claim:
- **VERIFIED** — confirmed by reading code, running test, checking output
- **INFERRED** — reasonable conclusion from reading, not directly tested
- **ASSUMED** — plausible guess, needs verification before acting on it

**When:** Communicating findings, especially to your future self or another agent.

**Why it works:** Distinguishes "I checked" from "I think" from "I'm guessing." Future-you (or future-anyone) can prioritize what to re-verify.

---

## Move 16: The "less, not more" pivot

**What:** When at capacity and tempted to add a tool/process/layer to handle the load — instead, remove things you're tracking.

**When:** "I have too much to do, I should build X to help" — that's the trigger.

**Why it works:** Adding layers adds maintenance, attention, and surface area. Removing items reduces all three. At capacity, removal is almost always the right move.

**Examples:**
- Drop projects explicitly
- Defer items with a written "deferred until X" note
- Say no to things that don't serve the load-bearing goal
- Close threads that have been "open" for >2 weeks with no progress

---

## Choosing the right move

| Stall type | First move to try |
|---|---|
| Fuzzy problem | Load-bearing question |
| Architectural fork | First-principles cut |
| Big build looming | Subplan / roundtable |
| 70% confident, want to stress-test | Red team |
| Days uncommitted | Ship-now |
| Cycling failures | Drop and redesign |
| Test isn't catching things | Substrate-external check |
| Drowning in pre-audit | Lazy bootstrap |
| Want to build meta-tool | Magic-button test |
| Open-ended task | Stop-condition declaration |
| Avoiding hard thing | Honey-badger callout |
| Lost calibration | Two-person sanity check |
| Sloppy claims | Provenance |
| Ambiguous evidence | Confidence labeling |
| At capacity | Less, not more |
