# Review base

The start of every project's review skill. A project copies what applies,
adds its own code standards and its bar, and keeps the result in
`.claude/skills/review/SKILL.md`.

## The loop

- The implementer verifies its change with the project's checks first and
  hands the reviewer the evidence: test output, commands run, captures.
- The reviewer is a subagent with fresh context. The implementer messages
  the same reviewer for each later round; from the second round on, it
  reviews the diff since the commit it last reviewed.
- Each finding names the file and line and says why it matters. It is
  labelled **important** (the bar says it needs a change), **nit** (taste;
  noted, no new round) or **pre-existing** (older than the change; noted
  for the plan).
- The loop ends when a round has no important findings. After three
  rounds, the implementer rethinks the approach instead of patching on.
- A finding the reviewer makes again and again is fixed at its source: this
  skill, a lint rule, or the project's `CLAUDE.md`.

## Findings from `/code-review`

At each phase's end, and when reviewing existing code, the implementer
runs Claude Code's built-in `/code-review` and hands its findings to the
reviewer. That review runs nothing and doesn't know this bar, so the
reviewer checks each finding against the code and labels it as above.
Important ones go through the loop.

## The bar

A change needs another round when it:

- is wrong: a bug, a broken case, a test that doesn't test what it claims;
- breaks the project's code standards or its intent;
- opens a security or data-loss risk;
- lacks the evidence that it works.

Everything else is a nit.
