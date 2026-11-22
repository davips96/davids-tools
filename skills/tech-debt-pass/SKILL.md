---
name: tech-debt-pass
description: A tech-debt pass over a project's existing code, run only when the user asks for one. Use when the user asks for a tech-debt pass, an optimization pass, or a review of a project's code outside a phase end. Step 1 reviews one area with /code-review high, has the project's reviewer filter the findings against its bar, and writes the real issues into agent/PLAN.md as small or big work items. Step 2 builds the small ones through the usual loop; the big ones wait in the plan. The pass never starts another pass.
---

# Tech-debt pass

A check of a project's existing code for what could be improved or
optimized, like the code freeze when developers get to work on tech debt.
The user asks for one when they know they won't be there and there is
capacity for it, since a review spends budget that a reason should
justify.

## When

- Run it when the user asks for one, in their own message or in a brief
  that quotes them.
- A session never starts one on its own, since a pass that follows from
  idle work loops: its fixes leave the work idle again.
- The phase-end `/code-review high <base>..HEAD` in the global file is a
  separate check and runs as before.

## Step 1: the pass

1. **Pick the area.** Take the one the brief names. When it names none,
   pick by risk: the code that changed most lately (`git log --stat`), code
   near one of the user's reports in `agent/reports/`, or code they are
   about to use (the plan's next items). One area per pass.
2. **Review it** with `/code-review high <path>`.
3. **Filter the findings.** Hand them to a reviewer subagent with the
   project's review skill. It checks each finding against the code and
   judges the area as if it were the change under review, so an
   **important** label marks a real issue, and everything else is a nit or
   not worth changing.
4. **Write the real issues into `agent/PLAN.md`** as work items, each sized:
   - **small**: a contained fix, built as one change;
   - **big**: a task of its own or more, placed in the plan's order where
     it fits.
5. **Mark the two exceptions** as you write them:
   - An item that would change the intent goes in as a discussion with
     the user, not a task, under the work set aside on a question for them.
   - An item that might change what the user sees or feels in the app is
     set aside on a question for them, and is built once they agree.
6. **Commit the plan**, so the findings outlast the session.

## Step 2: the work

- Build the small items right after the pass, each through the project's
  build, check and review loop. The reviewer reviews only the fix commits.
- The big items stay in the plan and are built later, in its normal order,
  like any task.
- Tick each item in the commit that finishes it.

## The pass never starts another pass

- The pass ends when its small items are built, or set aside on a question
  for the user.
- The fix commits get the loop's review and no `/code-review`, since that
  would be another pass.
- Then the session goes on with the rest of its brief. When everything left
  waits on the user, its recap says which area it reviewed and why, what it
  built, what waits in the plan and what waits on them, and it stops.
- Another pass runs when the user asks for another.
