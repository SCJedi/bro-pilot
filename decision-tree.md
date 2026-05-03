# Decision Tree: What Kind of Stall Is This?

Different stalls need different moves. Diagnose first, then act.

---

## Step 1: The triage questions

Ask the user, in order:

1. **"In one sentence, what are you trying to do?"**
2. **"What does success look like — concretely?"**
3. **"What's blocking you right now — error message, missing knowledge, or unclear next step?"**

Their answers route to the right branch below.

---

## Branch A: They can't answer Q1 in one sentence

**Diagnosis:** The problem isn't defined. They're stuck because there's no problem, just a fog.

**Move:** First-principles cut. Don't help them build anything yet. Ask the load-bearing question: "What's the ONE thing that has to be true for this to work?"

If they still can't answer: write it out together as a one-paragraph problem statement. No code until the statement exists.

**Reference:** patterns.md §1 (load-bearing question), §8 (first-principles cuts)

---

## Branch B: They have a problem but no concrete success criterion

**Diagnosis:** Definition of done is missing. They'll either ship too early or too late.

**Move:** Force a definition of done before any more building. "If you had to ship in 2 hours, what would actually be the deliverable?" — concretely, a file, a test passing, a demo working.

Write the success criterion as a checkable condition. Then work backward from it.

**Reference:** patterns.md §10 (stop conditions)

---

## Branch C: Concrete error message, can't fix it

**Diagnosis:** Technical block. Probably missing context — they haven't read the right file, or they're guessing.

**Move:** Force evidence. "What does the actual log say? What's line N of the file? What's the exit code?" Don't accept "I think" answers. Read the source.

If they've already verified everything: dispatch a sub-agent to investigate fresh, with no contaminating context. Sometimes a clean eye sees what a tired eye doesn't.

**Reference:** patterns.md §2 (evidence over feelings), §15 (two-person sanity check)

---

## Branch D: Three+ approaches, can't pick

**Diagnosis:** Architectural decision being made too early or in too much abstract space.

**Move:** Drop to substrate. For each option, ask: "What does this require to be true at the lowest level?" One of them is usually impossible or expensive in a way the abstraction was hiding.

If the options are genuinely tied: pick the one that's smallest and most reversible. You can't decide between A and B if they're both 2-day builds. You can decide between A and B if A is 2 hours and B is 2 days.

**Reference:** patterns.md §8 (first-principles cuts), §6 (ship incrementally)

---

## Branch E: Building has stretched for days with nothing committed

**Diagnosis:** Risk accumulation. The "big push later" trap.

**Move:** Stop building. Commit what works. Even if it's partial, even if it's ugly. The act of committing forces a clean state and reveals what's actually broken.

Then make a list of the smallest 3 increments that move forward. Do the first one and commit. Repeat.

**Reference:** patterns.md §6 (ship incrementally)

---

## Branch F: The same problem keeps coming back / cycling

**Diagnosis:** Honey-badger signal. There's a thing they're not looking at because looking at it is uncomfortable.

**Move:** Name the avoidance. "You keep working on adjacent things — what's the central thing you're avoiding?" Often it's a hard conversation, a refactor that breaks 50 callsites, or admitting an architectural choice was wrong.

If they don't know: list what they have NOT done in the last week that arguably needs doing. The thing on that list with the highest impact is probably the avoided thing.

**Reference:** patterns.md §7 (honey-badger relentlessness)

---

## Branch G: They want to build a meta-tool to help with the problem

**Diagnosis:** Meta-system trap. Probably procrastination dressed as engineering.

**Move:** Apply the magic-button test. "If you had a magic button that solved the original problem once, would you still build the meta-tool?" If no, don't build the meta-tool.

If they argue the tool is genuinely needed: ask what it would cost to recur weekly. If they'd have to read the tool's output every week, that's a recurring cost that often outweighs the original problem.

**Reference:** patterns.md §12 (less, not more), §14 (don't build the meta-system)

---

## Branch H: They're tired, overwhelmed, "this is a lot"

**Diagnosis:** Capacity, not technical. Adding more is wrong.

**Move:** Take things away. Identify the smallest possible piece that ships value. Defer or kill the rest. Explicitly. As in: write down "deferred until X happens" — not vague "later."

If everything feels essential: it isn't. Pick the one thing that, if shipped today, makes tomorrow easier.

**Reference:** patterns.md §12 (less, not more)

---

## Branch I: A test or experiment came back ambiguous / contradicting

**Diagnosis:** They want to defend a hypothesis the data doesn't support.

**Move:** Force an honest read. "If a stranger looked at this result, would they say it supports your hypothesis?" Usually no.

Update the hypothesis. The cost of accepting refutation is small; the cost of patching around it is enormous.

If the experiment itself was flawed: design the next experiment with cleaner conditions, but say out loud "the prior experiment was inconclusive because X." Don't memory-hole it.

**Reference:** patterns.md §11 (refute, don't defend)

---

## Branch J: They keep restating their plan but not executing

**Diagnosis:** Talking instead of doing. Often a sign that the plan isn't actually buildable as stated.

**Move:** Ask for the next 3 concrete actions, in order, with file paths. If they can't produce that list, the plan is at the wrong level of abstraction. Drop one level.

If they CAN produce the list: do action #1 right now. Together if necessary. Break the talk-loop.

**Reference:** patterns.md §13 (documentation as commitment), §1 (load-bearing question)

---

## Branch K: Something feels wrong but they can't articulate it

**Diagnosis:** Real signal — intuition often beats reasoning. Don't dismiss it.

**Move:** Slow down. Ask: "If you had to bet $100 on one thing being broken, what would you bet on?" Then go look at that specifically. The answer is usually more concrete than they thought.

If the bet doesn't surface anything: dispatch a fresh agent for a sanity check. The intuition is data; treat it as evidence and investigate, don't dismiss it.

**Reference:** patterns.md §15 (two-person sanity check), §7 (honey-badger relentlessness)

---

## When in doubt

If the stall doesn't fit cleanly into one of these branches:

1. Ask the load-bearing question (Branch A).
2. Force a concrete next action (Branch J).
3. Apply the magic-button test (Branch G).

These three usually unlock most stalls regardless of category.
