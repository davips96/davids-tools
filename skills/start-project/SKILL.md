---
name: start-project
description: The conversation with the user that starts a project, adds a major feature or rework, or onboards an existing project onto the agent/ files. Use when the user wants to start, spin up or begin a project, talk through a new feature or a rework, or onboard, convert or migrate a project that has no agent/ folder or an older one. Runs in a session in the project's folder that the user talks to directly, before any building, and ends with agent/INTENT.md read back to the user, the project's CLAUDE.md, its review skill and agent/PLAN.md.
---

# Starting a project

This is a conversation between partners about what the user wants to
build. Both of you suggest; they have the final call; you push back when
their decisions contradict each other or a step of logic doesn't hold. It
ends when you understand the product well enough to plan and build it
without asking them anything, and they have heard it read back.

It runs in a session in the project's folder (an empty one for a new
project) that the user talks to directly. Usually the main agent started
it; sometimes the user opened it themselves. When the folder isn't a git repo yet,
run `git init` first.

## Three ways in

- **A new project.** Nothing exists yet but the user's idea.
- **A new feature or a rework** of a project that already has `agent/`. The
  project and its `agent/INTENT.md` fill in the context; the conversation is
  about what changes.
- **Onboarding** a project without `agent/`, or with an older shape. See
  "Onboarding" below; the conversation comes first all the same.

## The conversation

- **Open on the problem.** When the user's opening doesn't say what
  problem the idea solves, ask that first: the friction behind an idea
  shows the limits they are working within, and later features are
  weighed against it. When the opening already says it, go to what is
  missing.
- **The user often opens with a lot.** Read what they gave you, and ask
  only about the gaps, in the order the conversation goes.
- **Ask a short numbered batch about one topic.** The user can answer in
  a numbered list, sometimes a few at a time: keep the unanswered ones open
  without reprinting them, and number new questions on from the last. A
  question card (the mid-turn kind, where they can also type their own
  answer) suits a single choice between clear options; leave your own
  pick unmarked, so it doesn't anchor them. A short scenario suits a
  complicated flow: build it from what the user has said they do, and
  offer the options rather than assuming their routine. Offer your ideas
  as options to weigh alongside theirs, and let them answer in their own
  words.
- **Look facts up instead of asking.** Machine facts are in
  `~/Projects/davids-tools/global/MACHINE.md`, and macOS quirks in
  `global/MACOS.md` beside it; when one is missing, check the machine and
  add it to the one it belongs in. Facts about the project and its data (how
  many records, what a codebase does) are checked during the conversation
  and recorded in the project; when onboarding, check them after the first
  conversation (see "Onboarding").
- **Show design.** When the product has a look, talk through the design
  intent and make mockups as you go: a private artifact page, or a
  screenshot when that shows it better. Settle a design language together;
  it becomes a section of the intent. When the user has no picture of the
  look yet, record that in the intent and settle the design language in
  the phase that first needs it.
- **Keep a running record.** Write `agent/INTENT.md` as you go, marked as a
  draft at the top, and commit after each answer, so the conversation
  survives across sessions.
- **Write a pace as step size, not a wait.** When the user asks for a pace
  such as "one playable step at a time", the intent records how big each
  step is, and the next step starts without waiting for them to try
  the last one: built work they haven't tried piles up by design (see the global
  file's "Working without the user").

## What to cover

Every product needs: the problem and who it is for; what people experience
using it; how it looks and feels; what it does; priorities; the MVP; what
is out of scope; constraints (platform, hosting, cost).

Past projects lost the most time on what surrounds the product, so cover
these too, when they apply:

- **Installing and updating.** How it gets onto the device and how updates
  land; signing identity; whether permissions survive an update.
- **The real data.** Which sources it reads and writes, and how much data
  there is: size changes which approach works.
- **Every action on every kind of item.** Read, create, edit, delete, send;
  which ones need the user's approval when the product acts.
- **Success examples.** Real things the user will do or ask, with what a
  right result looks like, in their words. They become acceptance tests.
  When they can't give them yet, they come later as reports.
- **Limits of the hardware and of any model it runs.** What wait is
  acceptable, measured.
- **Testing access.** Which accounts, devices and permissions you may use
  while building, and whether live tests (sending a real message) are fine.

**The plan test** decides when you're done: could you write the plan, and
the first phase with its design, without asking the user anything? Each "no"
is something still to cover. Some things only show up in use (what feels
relevant, what people undo); those come back as reports, so the
conversation doesn't chase them.

## The read-back

When the plan test passes, read the whole intent back to the user in the
conversation, in prose, and ask what is wrong or missing. For decisions
recorded long ago, ask "is this still true?", quoting the record with its
date. The read-back is where the biggest changes surface. Correct the
file, update any design or spec file that depends on what changed in the
same commit, remove the draft mark, and commit.

## After the read-back

- **The project's `CLAUDE.md`:** what the project is, how to build, run and
  check it, and a pointer to `agent/`.
- **Review standards:** propose the project's code standards and the bar a
  review holds changes to, from the stack and the project's existing
  practice, and tell the user what you chose. Write them as the project's
  review skill in `.claude/skills/review/SKILL.md`, starting from
  `review-base.md` in this skill's folder. Check with `git check-ignore`
  that the path is tracked: a local exclude can hide `.claude/`.
- **The plan:** write `agent/PLAN.md` without the user, as the global file's
  "How projects run" describes. Its first phase builds the checks.
- **Tell the main agent** that the project is set up, with where the plan
  starts. A session the main agent started tells it by ending its turn; a
  session the user opened sends it a message, as the global file's "Sessions
  and memory" describes.
- **Then carry on into the plan's first task.** The session that held the
  conversation is the one that builds. It starts without asking and keeps
  going until something waits on the user.

## Onboarding

The user's idea of the project and what the project is can differ;
onboarding reconciles them.

1. **Talk before reading.** Hold the conversation without reading the
   project first, so what exists doesn't anchor the user's answers. The
   project's `CLAUDE.md` and memory load on their own: say what you
   already know from them, and read nothing further until their first
   answers are in.
2. **Then read the project, through its tools first.** Run its build and
   checks for a factual baseline (in the background while the conversation
   goes on), read `git log`, then the docs and any process files. Process
   can live in code too: search tests and scripts.
3. **Talk through the differences.** For each place the project differs
   from what the user said, ask them which is right. When quoting their
   own recorded words, say where and when they were written, so they can
   weigh them.
4. **Write the intent and read it back.**
5. **Give every existing doc a home, section by section.** Rules for this
   project go to its `CLAUDE.md`, product decisions to the intent, design
   and specs to their files, where things stand to the plan, evidence to
   reports, cross-project lessons to the main agent. An
   existing design document stays a design document. A finished old plan
   whose item numbers the code or docs cite stays as a roadmap file rather
   than being summarized away. A process the old docs repeat (a bug-report
   session, a release routine) becomes a project skill. Ask the user before
   retiring a file that is theirs (their notes, an introduction they
   wrote): compare it with their profile (`global/USER.md`) first and
   keep what only it holds.
6. **Write the plan.** Work already in flight comes first.
7. **Migrate in one commit `git revert` can undo.** Search the whole repo
   (docs, skills, scripts, code comments) for the old file names, paths
   and item IDs and update each reference. Run the project's baseline
   check before and after; reduce the built-in memory index to a pointer.

It is done when a fresh read-only subagent in the project, asked "what's
next?", finds the answer in `agent/PLAN.md` without being told where to
look. Its answer also shows stale references the search missed.
