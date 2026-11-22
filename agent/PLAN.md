# Plan

## Where things stand

The toolkit is in use: the main agent starts work sessions nested under
itself, projects run on the `agent/` files, and the lessons from use are
folded into the global file and the skills. The repo is ready to share:
the user's profile, their machine notes and `projects/` are private and
git-ignored, the tracked files name no person or project, and the
`setup-toolkit` skill sets up a newcomer.

The next session starts on "Later" below, or on whatever lesson the main
agent has queued for this repo.

## Phase 1: the first write (done)

- [x] Global file written around the sessions, the named parts of
  `agent/`, how projects run, and what needs the user's approval.
- [x] `start-project` skill with three ways in and the review base.
- [x] `projects/` git-ignored; project-specific machine facts kept there.
- [x] This repo's intent and plan in the shape every project uses.

## Phase 2: first use (done)

- [x] Two onboardings of existing projects, tracked by the main agent.
  Done when both have `agent/INTENT.md` read back to the user and a fresh
  session in each finds "what's next" in `agent/PLAN.md`.
- [x] Fold what the onboardings taught into the global file and
  `start-project`.
- [x] Drop standing project owners: the main agent starts work sessions
  nested under itself, with one writer per project at a time.
  Note: an owner can't start sessions when another session messages it,
  and the repo files already carry a project's context, so a standing
  owner added a hop and gave nothing for it.
- [x] Make Claude Code's built-in `/code-review high` each phase's final
  check, and add `tech-debt-pass` for reviews of existing code on request.
  Note: run automatically whenever work went idle, a tech-debt pass
  looped, so it runs only when the user asks.
- [x] `main-agent-succession`, for handing the main agent's work to a
  fresh session when its context has drifted.

## Phase 3: ready to share (done)

- [x] Split the global file: the user's profile moves to the private
  `global/USER.md`, which the global file imports; `global/USER.example.md`
  is its template.
- [x] Split the machine notes: `global/MACOS.md` holds what is true on any
  Mac, the private `global/MACHINE.md` the user's own machine, with
  `global/MACHINE.example.md` as its template.
- [x] Every tracked file says "the user" and names no project.
- [x] `README.md` for a newcomer and their agent, and the `setup-toolkit`
  skill.

## Later

- A new project started from an empty folder, to exercise the new-project
  way in.
- A cutting pass on the global file once it has been used across projects.
- This repo has no `CLAUDE.md` or review skill of its own. It needs a
  conversation with the user about what bar an instructions repo wants.
- The paths in the tracked files assume the clone lives at
  `~/Projects/davids-tools`. A clone elsewhere, or a rename, means
  replacing that path across the repo.

## Set aside

Nothing.
