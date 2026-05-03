# Bro-Pilot

> 📺  **AS SEEN ON THE INTERNET**
>
> Like GitHub Copilot? Then you'll **LOVE** Bro-Pilot.* From the people who brought you *typing things into terminals* and *staring at your own code at 2 a.m.*, comes a revolutionary new way to be told what your brother would do — without having to interrupt your brother.
>
> | | 🤖 GitHub Copilot | 👊 SCJedi Bro-Pilot |
> |---|:---:|:---:|
> | Autocompletes your code | ✅ | ❌ (use Copilot for that, dummy) |
> | Tells you the *next move* | ❌ | ✅ |
> | Calls you out when you're avoiding the hard thing | ❌ | ✅✅✅ |
> | Will be polite about your bad ideas | ✅ | ❌ |
> | Costs $19/month | 💸 | 🆓 |
> | Comes with **48 distilled life heuristics** | ❌ | ✅ |
> | Knows when to tell you to **just ship it already** | ❌ | ✅ |
> | Has a brother named Eric | 😢 ❌ | 😎 ✅ |
> | Will judge you *(lovingly)* | ❌ | ✅ |
> | Replaces your therapist | 🚫 LOL no | 🚫 also no |
>
> **CALL NOW!** ~~Operators are standing by.~~ Actually just type `git clone` and leave us alone.
>
> 🔥 **First 1,000,000 users get Bro-Pilot 100% FREE!** *Limited-time offer ends never.* 🔥
>
> ⚠️ *\* Bro-Pilot is not a substitute for a real brother. If symptoms of stall persist longer than 4 hours, consult an actual brother. Bro-Pilot does not assume liability for shipped code, abandoned side projects, or sudden urges to commit and push. Heuristics may vary by builder. Past performance does not guarantee future stallouts. Not available in stores. Some assembly required (it's a folder; you copy it).*

---

A pocket advisor for when you're stuck mid-build. *"What would my brother do right now?"* — without having to interrupt him.

It's a [Claude Code](https://docs.claude.com/en/docs/claude-code) skill that channels an experienced systems-thinking builder. When you're cycling on a problem, can't pick a next move, or have been at it for hours and aren't sure you're thinking clearly anymore, you type one command and Claude walks you through a structured response: diagnose what kind of stall this is, name one concrete next move, cite the principle behind it, flag the trap you're about to fall into.

It's not magic. It's heuristics distilled from one builder's working patterns — about 48 of them — packaged so they show up exactly when you need them.

---

## What you need before installing

1. **Claude Code installed.** It's Anthropic's official command-line tool. If you don't have it: [docs.claude.com/en/docs/claude-code](https://docs.claude.com/en/docs/claude-code). Install takes a few minutes.
2. **A terminal you're comfortable with.** macOS Terminal, Windows PowerShell, Linux shell — any of them work.
3. **About 30 seconds** for installation.

That's it. No paid accounts beyond what Claude Code already needs, no API keys to wrangle, no config to fight.

---

## Install (pick your OS)

### macOS / Linux

```bash
git clone https://github.com/SCJedi/bro-pilot.git
mkdir -p ~/.claude/skills
cp -r bro-pilot ~/.claude/skills/
```

### Windows (PowerShell)

```powershell
git clone https://github.com/SCJedi/bro-pilot.git
$skills = "$env:USERPROFILE\.claude\skills"
if (-not (Test-Path $skills)) { New-Item -ItemType Directory -Path $skills | Out-Null }
Copy-Item -Recurse bro-pilot $skills
```

### Don't have git? Download the zip

1. Go to **[github.com/SCJedi/bro-pilot](https://github.com/SCJedi/bro-pilot)**
2. Click the green **Code** button → **Download ZIP**
3. Unzip it
4. Copy the `bro-pilot` folder into:
   - macOS / Linux: `~/.claude/skills/`
   - Windows: `C:\Users\<your-username>\.claude\skills\`
5. (If the `.claude/skills/` folder doesn't exist yet, create it.)

After copying, **restart Claude Code** (close and reopen the terminal session) so it picks up the new skill.

---

## Your first time using it

Open Claude Code in any project directory. You can use bro-pilot two ways:

### Way 1 — invoke directly with a slash command

Type:

```
/bro-pilot
```

Claude responds with two or three short triage questions. Answer them honestly. Bro-pilot diagnoses the stall and gives you one concrete next move.

### Way 2 — just describe what's wrong

You don't have to remember the slash command. If you describe a stall, Claude often picks up that bro-pilot applies. For example:

```
I've been at this for two hours and I keep going back and forth between
two architectural options. I can't tell which is right.
```

Claude (with bro-pilot loaded) replies in a specific shape:

> **What's actually happening here**
> You're stuck because you don't have a load-bearing question yet. "Which option is right" can't be answered without naming what each one has to be true for.
>
> **What your brother would do**
> Pick the option that's reversible. Build the smallest version of it that you can throw away. Ship it tomorrow. The other option becomes a fork in the road, not a deliberation.
>
> **Why**
> Reversibility beats correctness for first attempts. You can't tell which architecture is "right" until you've tried one. (See `patterns.md` — Pattern 03: Reversibility tax.)
>
> **Watch out for**
> The version you build isn't allowed to be the "real" one. The moment you're tempted to polish it, stop. It's a learning-build, not a shipping-build.
>
> **If that doesn't work**
> Spend 15 minutes writing what each option would look like at one-month scale. Drift in the writing tells you which one you actually believe in.

That's the shape every response takes. One diagnosis, one move, one principle, one warning, one fallback. Under 250 words. Designed to get you moving, not start a meeting.

---

## When to use it

- You can't pick between two or three options
- You've been building for days without committing
- The same bug keeps coming back
- You want to build a meta-tool to manage all your projects (this is a famous trap — bro-pilot will probably tell you to stop)
- You're overwhelmed by too much work in flight
- Your tests pass but the user says it's broken
- You've been alone with the problem for hours and can't tell if you're thinking clearly anymore

## When NOT to use it

- You have a specific bug — just ask Claude normally
- You want to chat or vent (it'll force a framework on you)
- You're one tool call from done — just finish

---

## What's inside

| File | What it does |
|---|---|
| `SKILL.md` | The trigger and main prompt. Claude reads this when bro-pilot activates. |
| `patterns.md` | 15 core principles — the worldview the advice comes from. |
| `decision-tree.md` | A diagnostic walkthrough: what kind of stall is this? |
| `moves.md` | Catalog of 16 named moves: dispatch, subplan, first-principles, red-team, ship-now, etc. |
| `anti-patterns.md` | 17 traps to avoid. Things experienced builders learn the hard way. |

You can read these directly. They're written to be human-readable, not just LLM-readable.

---

## Customizing it

The skill is yours to modify. Common tweaks:

- **Add patterns from your own experience.** Edit `patterns.md`, number the new entry sequentially.
- **Add moves you find yourself using.** Edit `moves.md`, keep entries concrete.
- **Adjust the tone.** Edit `SKILL.md` — that's where the voice is set. Want it warmer, more verbose, more terse — change it there.
- **Change the trigger name.** Edit the `name:` field at the top of `SKILL.md` and the slash command changes.

The most load-bearing file is `decision-tree.md` — it routes the diagnosis. Touch it carefully.

---

## Troubleshooting

**"I typed `/bro-pilot` and Claude says it doesn't know that skill."**
- The skill folder needs to be in `~/.claude/skills/bro-pilot/` (or `.claude/skills/bro-pilot/` for project-scoped use).
- Check the folder is named exactly `bro-pilot`.
- Restart Claude Code (close and reopen the terminal session) — sometimes it caches the skill list.

**"It works but the advice is too generic."**
- You probably skipped the triage questions. Bro-pilot is designed around them. If you describe the stall in 1-2 sentences and answer the questions, the response is much sharper.

**"The tone feels too direct."**
- That's the design. Edit `SKILL.md` (the Tone section) if you want softer phrasing.

**"It pushed me toward a move that didn't fit my situation."**
- Heuristics aren't laws. Ignore them when they don't apply. The README's one-line caveat: "If a move feels wrong for your situation, it probably is."

---

## The one-line caveat

This is heuristic advice from one builder's style — not the only way to think. Adapt what's useful, ignore what isn't.

## License

MIT. Use it, fork it, modify it, share it. See `LICENSE`.

## Credits

Heuristics distilled from observing one experienced systems-thinking builder over a few weeks of mid-stall recovery. Names redacted; patterns kept.
