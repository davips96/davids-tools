# davids-tools

A way of working with Claude Code: you talk a project through with Claude,
then Claude plans it, builds it, checks it and reviews it while you are
away, and you steer from what you see. This repo is what every session
carries into every project to make that work: one global instructions
file, a few skills, and a shape for each project's planning files.

It grew out of real projects, and the lessons those projects taught are
written into the files. It assumes Claude Code's **desktop app on a Mac**:
the main agent starts, messages and archives other sessions through the
app's session tools, and the machine notes are about macOS.

**If you are an agent reading this for a newcomer:** read this file, then
run the setup skill in `.claude/skills/setup-toolkit/SKILL.md` with them.
Don't make the symlinks or write their profile before that conversation.

## How the work runs

- **The main agent** is one pinned session, not tied to any project,
  that you talk to about all your projects. It starts a **work session**
  in a project's folder for each piece of work, with a brief that quotes
  you. Each work session reports back to it at the end of every turn; it
  checks the report, keeps its own notes, and tells you what needs you.
  Its own context stays thin: deeper reading goes to subagents and
  sessions.
- **Work sessions** do the work inside projects: they dig into docs, plan,
  or build. A building session runs a build, check and review loop with a
  reviewer subagent, and keeps going across tasks until something needs
  you. One session writes in a project at a time.
- **You talk to a project's session directly** to start a project (the
  `start-project` skill) and for design conversations that change what
  gets built. Everything else goes through the main agent.

The global file's "Sessions and memory" section has the details: where
you are (at the Mac or on your phone over Remote Control), which turns
can start sessions, and how the main agent keeps its notes.

## The files

### The shared side (tracked, the same for everyone)

```
global/CLAUDE.md          the global file: how to work with the user, what needs their
                          approval, sessions and memory, the agent/ files, how projects
                          run, the writing standard. ~/.claude/CLAUDE.md links here.
global/MACOS.md           macOS quirks that hold on any Mac (signing prompts, debugger
                          prompts, BSD sed, zsh, locked screens)
global/USER.example.md    the template for your profile
global/MACHINE.example.md the template for your machine notes
skills/                   ~/.claude/skills links here, so each is /<name> everywhere
.claude/skills/setup-toolkit/   the setup skill, available in this repo only
agent/                    this repo's own intent and plan, in the shape every project uses
```

The global file says "the user" throughout and never names a person or a
project, so the repo can be shared as it is.

### The private side (git-ignored, yours alone)

```
global/USER.md      your profile: who you are, in your own words. The global file
                    imports it, so every session reads it at start.
global/MACHINE.md   facts about your machine: hardware, signing identities, which
                    tools are installed, how it behaves while you are away
projects/           the main agent's own local git repo: one file per project with
                    its view of it, and its working file now.md
```

Your words stay as quotes in your profile: sessions quote it rather than
paraphrase it, since a paraphrase loses what you mean. Where the profile
and the global file differ about you, the profile wins.

### In each of your projects

Every project gets the same named parts under `agent/`, so you and any
session know where to look:

- `agent/INTENT.md`: what the product is for, who it is for, how it looks
  and feels, the MVP and what is out of scope. It changes only with your
  agreement.
- `agent/PLAN.md`: the phases, with the MVP marked. Its top says where
  things stand and where the next session starts.
- `agent/reports/`: one file per bug or change you report, in your words.
- specs and design files when the plan needs them.

Plus the project's own `CLAUDE.md` (how to build, run and check it) and its
review skill in `.claude/skills/review/`. `start-project` writes all of
these from a conversation with you; this repo's own `agent/` shows the
shape.

## Skills

| Skill | Source | What it does |
|---|---|---|
| `setup-toolkit` | this repo | Explains the toolkit, interviews you for your profile and machine notes, and makes the symlinks. Run it from this repo's folder. |
| `start-project` | this repo | The conversation that starts, extends or onboards a project; ends with the intent read back, the project's `CLAUDE.md`, its review skill and its plan |
| `main-agent-succession` | this repo | Hands the main agent's work to a fresh session when its context has drifted from long use |
| `tech-debt-pass` | this repo | A review of one area of existing code, run only when you ask: real issues go into the plan, small ones are built right away |

## Install

The paths in the files assume the clone lives at `~/Projects/davids-tools`.
Clone it there, open Claude Code in that folder, and run `/setup-toolkit`.
It walks you through everything below, starting with what you already have
in `~/.claude`.

By hand, the install is below. First, if `~/.claude/CLAUDE.md` or
`~/.claude/skills` already exists as a real file or folder, move it aside
(for example to `~/.claude/CLAUDE.md.before-toolkit`) and fold what you
want to keep into your profile and into `skills/`: the links replace them,
and `ln -s` onto an existing folder puts the link inside it instead.
`skills/` is tracked, so add a skill you keep private to `.gitignore`.

```bash
git clone <this-repo> ~/Projects/davids-tools
```

```bash
cp ~/Projects/davids-tools/global/USER.example.md ~/Projects/davids-tools/global/USER.md
```

```bash
cp ~/Projects/davids-tools/global/MACHINE.example.md ~/Projects/davids-tools/global/MACHINE.md
```

```bash
ln -s ~/Projects/davids-tools/global/CLAUDE.md ~/.claude/CLAUDE.md
```

```bash
ln -s ~/Projects/davids-tools/skills ~/.claude/skills
```

```bash
mkdir -p ~/Projects/davids-tools/projects && git -C ~/Projects/davids-tools/projects init
```

Then fill in the two private files.

Sessions read the global file when they start, so a session that was
already open keeps the old one; open a new session to see the change.

## Starting the main agent

Open a new session in the desktop app with no project folder, name it
"Main agent", and pin it. Its first prompt:

```
You are my main agent. Read ~/.claude/CLAUDE.md, "Sessions and memory" above all, then set up ~/Projects/davids-tools/projects/ with a now.md in the shape it describes, and commit it.
```

Then tell it what you want to build.

## License

MIT, in `LICENSE`.
