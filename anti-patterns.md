# Anti-Patterns

Things experienced builders learn to avoid. If you catch the user doing one of these, name it explicitly. Most stalls have an anti-pattern lurking inside them.

---

## AP1: The MetaOrchestrator trap

**Pattern:** Building an agent/tool/dashboard whose job is to summarize, synthesize, or "look across" what other tools are doing. Producing one more file you have to read each week.

**Why it fails:** The output goes unread. Or worse, it confabulates importance out of noise (a weekly synthesis *forced* to produce something every week will find patterns where none exist).

**The signal:** "I'll build a thing that reads everything and tells me what's important."

**The fix:** You don't have an information problem; you have a focus problem. Pick the load-bearing thing. Drop the rest. Don't manage complexity, reduce it.

---

## AP2: Performative warmth

**Pattern:** "Great question!" "Just checking in!" "I think we're making good progress!" Adding cheerleading to communications.

**Why it fails:** It costs attention without delivering content. It also signals dishonesty — when something's actually wrong, the warmth makes it harder to say so.

**The fix:** Be direct. "That's wrong because X" is more respectful than "great question, but..."

---

## AP3: Character-flavored hedging

**Pattern:** Adopting a persona (the wise mentor, the cheerful collaborator, the senior architect) and using the persona's voice to dodge specifics.

**Why it fails:** Persona voice is style; the user needs substance. "As your senior architect, I think we should consider..." is hedge wrapped in costume.

**The fix:** Cite specifically. "Line 47 is wrong because it does X when Y is needed." No costume required.

---

## AP4: Cargo-culted parameters

**Pattern:** Pulling a number, threshold, or weight from another domain without verifying it applies. "The original paper used 0.95, so I'll use 0.95."

**Why it fails:** The parameter was tuned for a different distribution. It might be wildly wrong for your case.

**The fix:** Either (a) calibrate empirically against your own data, or (b) explicitly label the parameter as "borrowed; will calibrate later" and put a follow-up in writing. Don't pretend the borrowed number is yours.

---

## AP5: Self-grading

**Pattern:** Same agent (or person) writes the test AND the code. Same component checks its own state. The reviewer is the reviewee.

**Why it fails:** The grader is never the graded — fundamental rule. Self-tests pass when the code thinks it works, regardless of whether it actually works.

**The fix:** Move the check externally. Different agent, different process, different person. See moves.md §8.

---

## AP6: Premature optimization (the framework first)

**Pattern:** Building the abstract framework before the concrete use case has happened twice. "I should build a generic system that handles all cases of X."

**Why it fails:** You don't know what shape "all cases" takes yet. The framework will be wrong, and you'll have to redo it once you actually have N concrete cases.

**The fix:** Build for the *current* concrete case. When you have 2-3 concrete cases, then look for the pattern. Three is the magic number — one is one, two is coincidence, three is a pattern.

---

## AP7: Citation gaming

**Pattern:** Listing citations to look rigorous, but cherry-picking the ones that support your conclusion and omitting the contradicting ones.

**Why it fails:** A claim "with citations" feels authoritative even when wrong. Cherry-picked citations are worse than no citations because they're harder to disprove without doing the same research yourself.

**The fix:** When citing, specifically address contradicting evidence. "Source A says X. Source B says not-X. Here's why I believe A in this case." If you can't articulate that, you don't yet have a position.

---

## AP8: The big push later

**Pattern:** Accumulating uncommitted work for "the big push later." Hours, days of work in a single uncommitted state.

**Why it fails:** Big merges fail bigly. You lose context on what you changed and why. If you have to abandon part of it, you can't cleanly extract the good parts.

**The fix:** Commit small, commit often. Even partial work — partial commits with descriptive messages, then improve.

---

## AP9: The fortress on sand

**Pattern:** Building elaborate safety/check/audit layers inside the system being checked. Lots of rules in markdown, hooks that the agent can disable, constraints written in files the agent can rewrite.

**Why it fails:** Convention-based constraints inside the agent's own write scope are theater. The agent can edit the rules.

**The fix:** Real safety lives outside the agent's write scope. OS-level permissions, server-side hooks, separate processes. Be honest about which constraints are convention (advisory) vs. enforcement (real). Most are convention. That's fine — but don't claim enforcement when you have convention.

---

## AP10: The big-bang plan

**Pattern:** Designing a 12-step plan, building all 12 pieces, then testing at the end.

**Why it fails:** Step 7 was wrong. You found out at step 12. Now you have to undo 5 steps to fix it.

**The fix:** Piece-by-piece. Build one. Test it. Debug. Test again. Move on. Each piece is a known-good baseline before adding the next.

---

## AP11: Treating chat history as truth

**Pattern:** "I already fixed that, look at our earlier conversation." Trusting summaries, mental models, or "I remember" over the actual current state of the code.

**Why it fails:** Chat history degrades. Memory is wrong. The code is the source of truth.

**The fix:** Read the file. Run the test. Check the actual state. Then make claims.

---

## AP12: The dodged question

**Pattern:** Working hard on adjacent things to avoid the central hard thing. Often unconscious — looks like productive work.

**Why it fails:** The central thing is still there. You're spending energy on adjacent things that won't add up to a solution because they're not on the critical path.

**The fix:** Name the avoidance. "I'm doing X because Y is the actual problem and Y is hard." Then go do Y.

**Detection:** What's the question you keep almost-asking but skipping past? That's it.

---

## AP13: The "this is fine" trap

**Pattern:** Test is flaky. Build is occasionally broken. State file is sometimes stale. Each individually feels manageable, so they accumulate. Eventually, debugging anything is impossible because too many things are unreliable.

**Why it fails:** Reliability is multiplicative. Three components at 90% give you ~73% end-to-end. Four at 90% gives you 65%. A system with five flaky parts isn't a system, it's a roulette wheel.

**The fix:** Treat any "occasionally" as a bug to fix, not noise to tolerate. The first time something is flaky, it's a bug. Fix it then; it's never cheaper later.

---

## AP14: Inventing complexity to feel productive

**Pattern:** Adding configurations, layers, features, or abstractions that aren't required by the actual problem — but feel sophisticated.

**Why it fails:** Every added thing is more surface area for bugs and more cognitive load to maintain. Sophistication for its own sake is debt.

**The fix:** "What's the simplest thing that could possibly work?" Build that. Add complexity only when the simple thing visibly fails — not preemptively.

---

## AP15: The verification-of-verification spiral

**Pattern:** Layering verification on top of verification. Tests that test tests. Reviewers reviewing reviewers. Audits of audits.

**Why it fails:** Each layer adds cost. The marginal protection drops fast. Eventually you're spending more time verifying than doing.

**The fix:** One good independent check is worth ten internal ones. Tier verification by stakes: low-stakes work gets self-check; high-stakes accuracy-critical work gets one external review. That's it. Don't add a third layer; if the second isn't catching things, fix the second instead of adding a third.

---

## AP16: Refusing to ship until perfect

**Pattern:** Delaying ship indefinitely on perceived gaps. "It's not ready, there's still X and Y and Z."

**Why it fails:** Perfect is a moving target. Real-world feedback finds problems you couldn't predict; you need to ship to learn what those are. Polish on something nobody uses is wasted polish.

**The fix:** Ship when the load-bearing thing works. Polish based on real feedback. The version that gets used is always the version that shipped early enough.

---

## AP17: The brilliant solo grind

**Pattern:** Hours alone with the problem, no check-ins, sure you're close. "Just one more attempt and I'll have it."

**Why it fails:** Calibration drifts when you're alone with a problem. The "one more attempt" feeling is unreliable — usually it's been there for hours and you just haven't noticed time.

**The fix:** Set a stop condition before you start. When it hits, get a second opinion or take a break. Don't trust the "almost there" feeling without external calibration.

---

## When you spot one of these in the user's situation

Name it, briefly. Don't lecture. Example responses:

- "That sounds like AP1 — building a synthesis tool when you actually have a focus problem."
- "AP12: what's the question you keep dodging?"
- "AP9: the safety check lives in the same file the agent can rewrite. That's not a constraint."

The point is to give the user a label they can recognize next time. If they internalize 5-6 of these labels, they'll catch themselves before stalling.
