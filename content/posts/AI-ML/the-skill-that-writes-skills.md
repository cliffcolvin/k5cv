+++
title = 'The Skill That Writes Skills'
date = 2026-07-16
draft = false
+++

*On teaching Claude to turn its own mistakes into standing rules*

In my last post I argued that the quality of what you get out of an AI is mostly a function of what you put in. Stop auditing the tool for failures, start auditing what you're feeding it. Give it the context that lives in your hands and never made it into words.

Fair enough. But there's an obvious problem with that advice, and a friend put his finger on it almost immediately: that sounds like a lot of typing. If I have to hand-feed this thing every constraint I've ever internalized, every time, forever, where exactly is my four hours?

So here's the follow-up. You don't have to be the only one writing the context down. You can teach the machine to write it for itself.

## The skill that writes skills

A while back I taught Claude a skill whose entire job is to reflect on a session after the work is done and ask: what happened here that will happen again?

The framing I gave it was something I actually believe about learning, for people as much as for models:

> You are the one in control of your learning. The key to learning is recognizing patterns you do or see, then learning both how to recognize when to use that pattern again, and how to execute it again in the future.

Read that carefully, because there are two halves and most people only ship the first. *Recognizing when* to apply a pattern is a separate skill from *knowing how* to apply it. A session that solves a problem once produced an answer. A session that also encodes the pattern produced a capability. That difference is the whole ballgame.

So at the end of a session, the reflection skill runs and asks whether any of this happened:

- A multi-step workflow got figured out by trial and error (wrong turns taken, a tool's quirks discovered, a working sequence finally found).
- A gotcha cost real effort and would cost it again.
- The same *shape* of task has now shown up twice.
- I said something like "this is worth remembering."

If yes, it writes a new file: a skill. If no, it does nothing, which matters just as much. You do not want a system that manufactures wisdom out of trivia.

## What actually goes in the file

A skill is not documentation. Documentation explains what something is. A skill has to make a cold session, with no memory of the original work, succeed on the first try. Mine have four parts:

1. **Trigger conditions.** The recognition half. Written so a future agent scanning the list knows *when* this applies, not just what it does. This is the part people skip and it's the part that makes the whole thing work.
2. **The working procedure.** Exact commands, exact order, exact waits. Not a summary of the approach. The approach.
3. **The gotchas.** Everything that went wrong this time. These are almost always the most valuable lines in the file.
4. **Interpretation guidance.** How to read the output, not just how to get it.

There's a companion question the reflection asks too: separate from patterns, what durable *facts* did we learn? Those go somewhere different. Patterns become skills; facts become memory. Blurring the two gives you a pile of files that are neither.

## The miss

None of this would be worth a blog post if it only ever caught tidy little workflow gotchas. Here's the one that changed my mind about what this is for.

I had Claude migrating one of my side projects from one cloud provider to another, working fairly autonomously. Part of that migration involved swapping out an embedding model. If you haven't worked with vector search: an embedding model turns text into a list of numbers, and every model produces a list of a specific length. The old model produced 1024 numbers. The new one produced 384.

That number is a contract. It is welded into the database collections you already built, into any place a developer typed the number in by hand, into config that only ever made sense for the old backend. Claude changed the model, deployed, and took the site down.

The failure was not exotic. Somewhere in the codebase a constant still said 1024. A grep would have found it in about four seconds.

I was annoyed, and I asked the question I always ask, the one my last post was entirely about: how could I have given you better context here?

## The honest version

Here's what came back, and it's the reason I'm writing this:

> I saved it to memory as a standing rule, and it earned its keep within the hour: the same "enumerate consumers first" check is exactly what caught that deleting a shared component would have broken every user's connector. The rule I wrote down: a change to a shared contract isn't local. Grep the old constant, list every producer and consumer, migrate them together.
>
> Worth noting the honest version though: this wasn't a context gap on your end. The codebase had everything; I just didn't run the audit.

I want to sit on that last line, because I think it's the most interesting sentence any tool has ever produced for me.

I offered it an excuse. A very reasonable excuse, one I had spent a whole essay constructing the intellectual scaffolding for. *You didn't have the context.* And it declined. It went and checked, and the context had been there the entire time. What was missing wasn't information. It was a procedure that it failed to run.

That distinction is not a small one. "I lacked context" and "I lacked discipline" are different diagnoses with different treatments, and only one of them is my problem to fix. If it had accepted my excuse, I would have gone off and written more documentation that nobody needed, and the same bug would have shipped again next month.

Instead it wrote itself a rule. And then, within the hour, that rule stopped it from deleting a component that would have quietly broken every user's integration. It taught itself to chase down dependencies before touching production, and then it used the lesson while the ink was still wet.

## What this means for the last post

I need to amend my own argument, which is a nice problem to have.

Context is necessary. It is not sufficient. There is a second failure mode that has nothing to do with what you fed the machine and everything to do with what it did with it, and you cannot prompt your way out of that one. You need something the model runs *as procedure*, not something it merely knows.

That's what a skill is. A prompt is what you say. A skill is what it does without being told.

And the reflection skill is how those get written without you having to sit down and imagine, in advance, every rule you'll ever need. You won't imagine them. That's the point. The rules worth having are the ones the failures teach you, and the failures haven't happened yet.

## How to actually do this

If you want to try it, the shape is simple enough to steal. Here is the reflection skill itself, stripped down to the portable parts. In Claude Code this lives at `.claude/skills/skill-extraction/SKILL.md`, but there's nothing magic about the location; it's a Markdown file with a bit of frontmatter, and the `description` is what tells the model when to reach for it.

```markdown
---
name: skill-extraction
description: At the end of any session, recognize repeatable patterns in the
  work just done and encode them as new skills, including when to trigger them
  and how to execute them. Use automatically whenever a session involved a
  multi-step workflow, a hard-won gotcha, or anything we would plausibly do
  again. Not just when explicitly asked.
---

# Skill Extraction (how this setup learns)

## Philosophy

You are the one in control of your learning. The key to learning is
recognizing patterns you do or see, then learning both how to recognize when
to use that pattern again and how to execute it again in the future.

A session that solves a problem once produced an answer. A session that also
encodes the pattern produced a capability. This skill is the encoding step.

## When to trigger

Run this review at the end of any session where at least one of these
happened:

- A multi-step workflow was figured out by trial and error (wrong turns
  taken, tool quirks discovered, a working sequence finally found).
- A gotcha cost real effort and would cost it again.
- The same shape of task has now appeared twice across sessions.
- I said anything like "this is worth remembering," "we'll do this again," or
  "this should be a skill."

Do not extract from one-off trivia or things a fresh session would trivially
rediscover. "Nothing to extract" is a valid and common outcome.

## Patterns and facts are different things

Each review asks two questions:

- What patterns did we run? Those become skills (procedures).
- What durable knowledge did we gain? Those become memory (facts about me,
  about how an external system actually behaves, about cross-cutting
  context).

Keep them in separate buckets. Prefer updating an existing file over creating
a near-duplicate.

## What a good extraction contains

1. Trigger conditions. The recognition half. Write the description so a
   future session knows WHEN this applies, not just what it does.
2. The working procedure. Exact commands, tool names, order of operations.
   Write it so a cold session succeeds on the first try.
3. The gotchas. Everything that went wrong this time, so it never goes wrong
   again. Usually the most valuable lines in the file.
4. Interpretation guidance. How to read the output, not just how to get it.

## Procedure

1. Review the session and list candidate patterns.
2. For each, decide: new skill, or fold into an existing one? Check what
   already exists first.
3. Write the file following the four sections above.
4. Flag unresolved design choices as open questions in the file rather than
   guessing. Surface them the first time the skill is used.
5. Tell me what was extracted and why, in a sentence or two each. I learn
   from the same patterns, so the recognition reasoning matters more than the
   file list.
```

That's the whole thing. A few notes on why it's built that way:

**Start with a reflection habit, not a rulebook.** Notice that the file above contains no actual engineering rules. It doesn't know about vector dimensions or shared contracts or anything else I've learned the hard way. It's a machine for producing those, and it's the only piece you have to write by hand.

**Make it write triggers, not just steps.** "How to do X" is half a skill. "You are probably in a situation that needs X when you notice Y" is the half that makes it fire on its own.

**Keep patterns and facts in separate buckets.** Skills are procedures. Memory is facts. They rot at different rates and they get used at different moments.

**Let it say "nothing here."** A reflection step that always produces something is a reflection step that has learned to produce noise.

**Ask the diagnostic question honestly, and let it disagree with you.** When something breaks, "how could I have given you better context?" is a good question, but only if the answer is allowed to be "you couldn't have; I just didn't check." Most of the value I've gotten from this setup came from that answer.

**Stay the editor.** This is the part I won't hand over. It writes the draft rule; I decide whether it's a real rule or an overfit reaction to one bad afternoon. A system that promotes every stumble into permanent law becomes unusable in about a week. Something has to have taste, and that's still my job.

## Making sure it actually fires

There's a hole in everything I just told you, and it's the same hole as before.

Look again at that skill. Its trigger is "at the end of any session." That is a promise the model has to remember to keep. And it mostly does. But "mostly" is carrying an enormous amount of weight in that sentence, and it fails in precisely the worst place: the long, messy, six-hour session that generated the most lessons is also the one where the early instructions are furthest away and most likely to have been squeezed out. The sessions with the most to teach are the sessions most likely to skip the lesson.

Putting it in a project instructions file doesn't fix this. That's still context. You're still asking nicely.

The fix is to stop asking. Most of these tools have a lifecycle event that fires when the model tries to end its turn, and lets you refuse. In Claude Code it's a `Stop` hook: a script the harness runs, not something the model chooses to run. Refuse to let the turn end, and the model doesn't get a vote.

Which sounds easy, and my first version of it was wrong.

Here's the thing that makes end-of-session work genuinely hard: **the stop event fires at the end of every turn, not at the end of the session.** Every time the model finishes a task or comes up for air to ask you something, that's a stop. There is no "the session is over now" event you can hang work on. The one that fires when a session truly ends fires too late to ask the model for anything.

So my first hook fired on the first stop after the session had done real work. Which meant it reflected on a *half-finished session*, congratulated itself, marked itself done, and never looked at anything I did afterward. It wasn't too expensive. It was reflecting on the wrong session.

The fix is to notice that "the session ended" and "no more turns are coming" are the same statement, and the second one is measurable. Wait. If another turn shows up, this wasn't the end, so shut up and let the next one worry about it. If nothing shows up, everybody went home, and now you have the whole session to look at.

That's a debounce, and it's about eight lines:

```bash
#!/usr/bin/env bash
# Stop hook: reflect ONCE, when the session has actually gone idle.
input=$(cat)

session_id=$(printf '%s' "$input" \
  | sed -n 's/.*"session_id"[[:space:]]*:[[:space:]]*"\([^"]*\)".*/\1/p')
transcript=$(printf '%s' "$input" \
  | sed -n 's/.*"transcript_path"[[:space:]]*:[[:space:]]*"\([^"]*\)".*/\1/p')
[ -z "$session_id" ] && exit 0

state="${TMPDIR:-/tmp}/reflect"; mkdir -p "$state" || exit 0
done_marker="$state/$session_id.done"
gen_file="$state/$session_id.gen"

# Guard 1: at most one reflection per session.
[ -f "$done_marker" ] && exit 0

# Guard 2: only sessions that actually built something.
[ -f "$transcript" ] || exit 0
edits=$(grep -o '"name":"\(Edit\|Write\)"' "$transcript" 2>/dev/null | wc -l)
[ "${edits:-0}" -lt 4 ] && exit 0

# Guard 3: the debounce. Claim this turn, then wait.
stamp="$(date +%s)-$$"
printf '%s' "$stamp" > "$gen_file" || exit 0
sleep "${IDLE_SECS:-300}"

# Somebody stopped after me, so my turn wasn't the end. Their problem now.
[ "$(cat "$gen_file" 2>/dev/null)" = "$stamp" ] || exit 0

# Still the newest stop after five quiet minutes. Everyone's gone home.
touch "$done_marker"
cat <<'MSG'
The session has gone idle. Run the reflection over the WHOLE session, then
finish. Any repeatable pattern or costly gotcha worth writing up with
triggers, procedure, and gotchas? If nothing clears that bar, say so in one
line and finish. "Nothing to extract" is a valid and common answer.
MSG
exit 2
```

Every stop grabs a timestamp and goes to sleep. A newer stop overwrites it, so the older sleeper wakes up, sees it's been superseded, and quietly exits. Only the stop that's still the newest one after five quiet minutes concludes that the session is actually over. No turn counter, no bookkeeping, and it self-corrects if you come back from lunch and keep working.

The `exit 2` is the interesting part. This hook runs in the background (`"async": true, "asyncRewake": true` in the config), which means it never makes you wait. You get your answer the instant it's ready. Five minutes later, once you've wandered off, the thing wakes back up and does the filing.

Wire it up in `settings.json` and it runs whether anyone remembers it or not:

```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "bash \"$HOME/.claude/hooks/reflect.sh\"",
            "shell": "bash",
            "async": true,
            "asyncRewake": true,
            "timeout": 900,
            "statusMessage": "Arming reflection…"
          }
        ]
      }
    ]
  }
}
```

The `timeout` has to outlive the `sleep`, or the harness kills your patient little waiter before it ever wakes up.

Each guard is there because of a specific way this goes wrong, and I'd rather hand you the list than have you rediscover it. Without the first you reflect over and over on a session you already filed. Without the second it fires on "what does this error mean," which trains you to ignore it, which is worse than not having it. Without the third you're back to grading a half-finished session. And if you ever find yourself writing the naive version that just fires immediately, notice that you've built something that interrupts you at your busiest moment to ask what you've learned so far. The answer is "not yet, I'm working."

Two honest limitations. The sleeping waiter only survives as long as the session process does, so if you slam the terminal shut, the reflection never happens. And the five minutes is a number I made up.

But here's the part I keep chewing on. The hook cannot tell whether there's a lesson in the session. It has no idea. All it can do is guarantee the question gets *asked*, every time, whether or not anyone feels like asking it.

That turns out to be most of the value. Not the answer. The fact that the question is no longer optional.

## The compounding part

Here's why I think this is more than a productivity trick.

Every rule of thumb you have as an engineer was purchased with an outage. You know to check the thing because one time you didn't check the thing and your weekend evaporated. That knowledge is expensive and it is almost entirely trapped: it lives in your hands, it doesn't transfer to your teammates except by anecdote, and it leaves the building when you do.

What I'm describing is a way to make that scar tissue durable and portable. The 1024 lesson cost me a downed site exactly once. It is now a file. It will be read by every future session, including the ones where I'm not paying close attention, and including the ones running while I'm asleep.

Thamus worried that writing would let us stop knowing things. But he was watching the wrong ledger. Writing is also how a lesson learned once at real cost gets to be known forever, by everyone who comes after, without any of them having to pay for it again.

The machine just learned to take notes. That's the whole trick, and it's the oldest one we have.
