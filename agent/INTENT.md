# Intent

What this toolkit is for. It changes only with the user's agreement, like
any project's `agent/INTENT.md`.

## The problem

The user wants to talk a project through with Claude and then have Claude
build it to their standards while they are away, without reading the
code. Two kinds of attempt showed where this breaks:

- **Alignment through documents is slow.** Capturing intent as claims for
  the user to review takes more of their time than the work it saves, and
  reviewing a draft invites accepting it without weighing it. A
  conversation, read back at the end, aligns faster.
- **Specifying everything isn't the lever.** A process that prescribes how
  every file is laid out grows faster than the work it governs. Claude
  organizes well on its own; what it lacks is knowledge (who the user is,
  what past projects taught) and tools (ways to check its own work).

## Who it is for

- **The user**, who directs: they set the parameters, have the final
  call, and steer from what they see.
- **Claude sessions** on their machine, which read the global file and
  load the skills.
- **Anyone the user shares it with.** The shared side names no person and
  no project, so another person clones it, runs `setup-toolkit`, and gets
  their own private side.

## What it is

- **A global file** (`global/CLAUDE.md`, symlinked as `~/.claude/CLAUDE.md`)
  with what every session in every project needs: how to work with the
  user, what needs their approval, the sessions and where memory lives,
  the named parts of a project's `agent/`, how projects run, and the
  writing standard.
- **The user's profile** (`global/USER.md`, private), which the global
  file imports: who the user is, in their own words.
- **Machine facts:** macOS quirks that hold on any Mac (`global/MACOS.md`)
  and the user's own machine (`global/MACHINE.md`, private).
- **Skills** (`skills/`, symlinked as `~/.claude/skills`), each carrying
  knowledge for one situation: `start-project` for the conversation that
  starts, extends or onboards a project, with the base for each project's
  review skill; `main-agent-succession` for handing the main agent's work
  to a fresh session; `tech-debt-pass` for a review of existing code when
  the user asks.
- **A setup skill** (`.claude/skills/setup-toolkit/`, run from this repo)
  that explains the toolkit, interviews the user for their profile and
  machine notes, and makes the symlinks.
- **A `projects/` directory, its own local git repo** that this repo
  ignores, where the main agent keeps one file per project and its working
  file.

## How it should feel to the user

They open their pinned main agent, say "spin up the X project", and get a
conversation with a partner: both suggest, Claude pushes back on
contradictions, and they have the final call. Then Claude runs the
project, asks only what only they can answer, and keeps captures of the
work for them to see when they ask. They work on every project through the
main agent. It starts the sessions that dig into a project, build it and
review it, and keeps its own context thin. They hear from it when work
starts and when it is done; the sessions are a black box they can open if
they go digging. They talk to a project's session directly to start a
project and for design conversations that change what gets built.

## Principles

- **Instructions carry knowledge and tools, not guardrails.** A rule earns
  its place when it holds something Claude can't know (the user, past
  lessons) or gives it a way to check its work.
- **Common names, flexible forms.** Every project has the same parts of
  `agent/`; how each is laid out inside is the writing session's call.
- **Checks before features, evidence over claims.** Each project's first
  phase builds its tests, lint and a way to see and capture the product.
- **Principles from outside practice, not its machinery.** Code review at
  large scale informs the review loop's bar, convergence and fixing at the
  source; its scale machinery stays out.
- **Fix at the source.** A lesson that repeats goes into the skill, lint
  rule or instruction file that would have prevented it, and a new skill is
  added when a pattern has proven itself across projects.
- **Shared and private stay apart.** What is about the user, their machine
  or their projects lives in git-ignored files; the tracked files hold
  only lessons, so the repo can be shared as it is.

## Out of scope

- Organizations of agents with roles and tiers.
- Unattended-session machinery: with a main agent starting the work, a
  session running without the user is the normal case.
- Prescribed file layouts for planning and reporting.

## Done looks like

The user starts the main agent, starts and onboards projects in
conversation with a project session, and builds through the main agent,
and the global file and `start-project` are enough for that without them
explaining the workflow. A newcomer gets there from a clone and one run of
`setup-toolkit`.
