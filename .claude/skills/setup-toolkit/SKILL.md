---
name: setup-toolkit
description: Sets up this toolkit for a new user, or redoes their private side. Use when someone has just cloned the repo, asks what it is or how to install it, wants to set it up, or wants to rewrite their profile or machine notes. Explains the repo, the main agent and how the files relate to the user, checks what is already in ~/.claude, interviews the user for their private profile (global/USER.md) and machine notes (global/MACHINE.md), makes the symlinks and the projects/ repo, and ends with how to start the main agent.
---

# Setting up the toolkit

A conversation with the person who just cloned this repo. It ends with
their profile and machine notes written in their words, `~/.claude`
pointing into the repo, and them knowing how to start their main agent.
`README.md` at the repo root is the reference; this skill is the order to
go through it in.

From here on, "the user" is the person you are setting it up for. Speak to
them as "you".

## 1. Check where things are

Before explaining anything, look, so the explanation fits what you find:

- **Where the clone is.** The tracked files name `~/Projects/davids-tools`
  in their paths. When the clone is elsewhere or renamed, say so: the
  simplest fix is moving the clone there; replacing the path across the
  repo is the other way, and it is the user's call.
- **What is in `~/.claude` already.** Check `~/.claude/CLAUDE.md` and
  `~/.claude/skills`: missing, a symlink (to where), or a real file or
  folder. Read what is there. The symlinks replace both, so their content
  needs a home first (step 5).
- **The private files.** Whether `global/USER.md` and `global/MACHINE.md`
  exist. When they do, this is a redo: read them, and in the interview ask
  only what the user wants to change.
- **The machine.** That it is a Mac, and whether Claude Code runs in the
  desktop app (`CLAUDE_CODE_ENTRYPOINT` and `CLAUDE_CODE_DESKTOP_APP_VERSION`
  in the environment say so). The main agent needs the desktop app's
  session tools; without them, say what that leaves: the global file, the
  skills and the `agent/` files still work, run by hand.

## 2. Explain the toolkit

In a few short paragraphs, in conversation, from `README.md`:

- **What it is:** a way of working where the user talks a project through
  with Claude, then Claude builds, checks and reviews it while they are
  away, and they steer from what they see.
- **The main agent and work sessions:** one pinned session the user talks
  to about every project; it starts a work session in a project's folder
  for each piece of work, and each reports back to it. The user talks to
  a project's session directly only to start a project and for design
  conversations.
- **How the files relate to the user:**
  - the global file is about working with "the user", whoever that is,
    and is the same for everyone who uses the toolkit;
  - their profile is about them, in their own words, and every session
    reads it at start, imported by the global file; it is private;
  - their machine notes are what sessions check before asking them a
    machine fact; private;
  - `projects/` is the main agent's own notebook about their projects,
    its own local git repo; private;
  - each project's `agent/` holds that project's intent, plan and their
    reports; the intent changes only with their agreement.
- **What needs them:** changing a project's intent, unrecoverable
  deletes, pushing to public repos, installing software. The rest Claude
  decides and tells them about.

Then ask whether they have questions before the interview, and answer
from the files.

## 3. Interview for the profile

The profile is the user's own words. Sessions quote it rather than
restate it, so collect quotes, not summaries.

- Work through `global/USER.example.md`'s sections in short numbered
  batches, one topic per batch. They can answer in a numbered list, a few
  at a time; keep the unanswered ones open and number new questions on
  from the last.
- The topics, in order:
  1. Their name and pronouns, and what they do: role, experience, what
     they build, what they would rather hand off.
  2. What they care about most in the work, and how they like to work day
     to day (GUI or terminal, how much code they want to read).
  3. When the work happens: whether they are away most of the time, and
     where they follow sessions from (only the Mac, or their phone over
     Remote Control too).
  4. Why they give agents the autonomy they do, in their words.
  5. What agents most often get wrong with them, in their words.
  6. What they want from Claude, in their words.
  7. Their view on built work piling up untried while they are away, and
     on when a tech-debt pass is worth its cost.
  8. Small things: the greeting they open a sitting with, whether they
     are glad to do small hands-on steps (start an app, record something,
     try a build).
- When an answer is in their words, keep it word for word in quotes.
  Write your own sentence around it only to say what to do with it.
- When their old `~/.claude/CLAUDE.md` holds things about them, offer
  those as the starting point for the matching section, quoted, and ask
  whether each still holds.
- Write `global/USER.md` from the template as the answers come in, keep
  the template's opening paragraph, drop its comment and every bracket,
  and use their pronouns throughout. Then read the whole profile back and
  ask what is wrong or missing.

## 4. Machine notes

Check before asking. From `global/MACHINE.example.md`, fill in what the
machine can tell you:

- `sw_vers`, `sysctl -n hw.memsize`, `sysctl -n machdep.cpu.brand_string`
- `security find-identity -v -p codesigning`
- `DevToolsSecurity -status`
- `pmset -g custom`
- `which docker xcodebuild python3 node`, and
  `python3 -c "import PIL"` for the image library

Then ask only what the machine can't say: whether it stays awake and on a
charger while they are away, and whether the lid stays open. Write
`global/MACHINE.md`, drop the template's comment and brackets, and read
it back.

## 5. Give the old `~/.claude` content a home

Only when step 1 found a real `~/.claude/CLAUDE.md` or `~/.claude/skills`:

- Sort what the old `CLAUDE.md` holds: things about the user go to their
  profile (most of it was folded in during step 3), facts about the
  machine to `global/MACHINE.md`, and rules about working that they want
  to keep to a "## Their own rules" section at the end of the profile,
  where they win over the global file. Show them the sort before writing.
- Move each skill folder from the old `~/.claude/skills` into the repo's
  `skills/`, unless the repo already has one of that name; ask about each
  clash.
- Moving or replacing files outside the repo needs the user's yes. Ask
  once, naming each path, then move the old ones aside rather than delete
  them: `~/.claude/CLAUDE.md.before-toolkit` and
  `~/.claude/skills.before-toolkit`.

Their own skills in the repo's `skills/` are tracked by its git. When they
are private, add them to `.gitignore` and say so.

## 6. Make the links

```bash
ln -s ~/Projects/davids-tools/global/CLAUDE.md ~/.claude/CLAUDE.md
```

```bash
ln -s ~/Projects/davids-tools/skills ~/.claude/skills
```

```bash
mkdir -p ~/Projects/davids-tools/projects && git -C ~/Projects/davids-tools/projects init
```

Check each with `ls -la ~/.claude` and `git -C ~/Projects/davids-tools
check-ignore global/USER.md global/MACHINE.md projects/now.md`, which
must list all three: the private side stays out of the repo.

## 7. Check it loads

This session read its instructions when it started, so it can't show the
change. Ask the user to open a new session in any folder and ask it: "What
is the heading of your user instructions, and who is the user?" The
answer names "Working with the user" and then them, from their profile.
When it doesn't name them, check that `~/.claude/CLAUDE.md` is the
symlink and that `global/USER.md` is where the import line in
`global/CLAUDE.md` says.

## 8. Starting the main agent

Tell them how, from `README.md`'s "Starting the main agent": a new
session with no project folder, named "Main agent", pinned, and the first
prompt from there in a code block they can copy. Then the setup is done:
recap what was written where, and that every private file stays out of
git.
