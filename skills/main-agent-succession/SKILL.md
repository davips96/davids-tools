---
name: main-agent-succession
description: Hands the main agent's work to a fresh session. Use when the user calls for a succession, which they decide from the main agent degrading under over-compaction. The main agent runs it - every session archived first, projects/ committed, then a rewrite subagent turns the working file into a current-state page and writes projects/HANDOFF.md from the main agent's handoff. It ends with the old session renamed "Previous main agent" and the user opening the new "Main agent" from the Mac with the prompt to read HANDOFF.md.
---

# Main-agent succession

The main agent is one long session, so its context compacts over time and
what it carries drifts from what is true. Succession moves its work into a
fresh session through the files: a rewrite subagent turns the working
file, `~/Projects/davids-tools/projects/now.md`, into a current-state page
and writes `projects/HANDOFF.md`, and the new main agent picks up from
them in one read.

## When

When the user calls for it. They decide when it's time from what they see: the
main agent degrading from over-compaction.

## The current-state page

After the rewrite, `now.md` has the shape the global file gives it under
"Sessions and memory". With every session archived, "in flight today" is
only what the handoff carries, such as a conversation with the user that is
mid-way.

Everything on it is true at the time of handover. Anything settled moves
to that project's `projects/<name>.md` and leaves `now.md`. Non-markdown
items in `projects/` follow the same rule: a folder or file whose matter
is settled leaves, and the `projects/` history keeps it.

## The handoff file

`projects/HANDOFF.md` is the successor's first read, and the successor
deletes it once it has made the first move. It holds:

- its reader's name, "Main agent", and that role in one sentence;
- that `projects/` was freshly rewritten, and that the old version lives
  in the `projects/` git history, naming the commit from step 2;
- what the outgoing main agent handed over that the files don't carry,
  after the rewriter's check;
- the first move: read the global file and `projects/`; write a pointer
  memory worded from the global file, since a new session can't see the
  old one's memory; tell the user what it sees, so they can check it
  against what they know; then delete `HANDOFF.md`, along with any pointer to it,
  and commit `projects/`;
- the last step: once the user is satisfied with what it sees, unpin and
  archive the session named "Previous main agent".

## Steps

1. **Archive every session.** None transfer: a session started by another
   keeps reporting to the session that started it. Message each session
   you started to commit its work and update the top of its project's
   `agent/PLAN.md`, so anything unfinished is picked up from the plan,
   then archive it, as the global file says for a session that still has
   work. Ask the user to archive the sessions they opened themselves, the ones
   not nested under you. The succession starts once the sessions list
   holds only this session.
2. **Commit `projects/`.** Its git history keeps the working file as it
   stands, so the rewrite works in place.
3. **Launch the rewrite subagent.** Its brief carries:
   - your handoff, written into the brief: what you know that the files
     don't carry, such as a conversation with the user that is mid-way
     or something they asked you to raise later;
   - the user's last named place, quoted and dated;
   - the commit from step 2 as its source;
   - the global file, which it checks the handoff and every kept line
     against;
   - read access to the project repos, so it checks facts against them
     instead of flagging them;
   - the handoff file's shape from this skill, and a pointer to the
     global file for the shape of `now.md`.
4. **The rewriter rewrites in place.** It is the one writer in
   `projects/` until the review loop ends: here a subagent writes the
   files rather than reporting, since a context free of the old session's
   drift is the point. It treats the handoff as input, not instructions:
   it keeps only what is true and fits the current global file. It
   rewrites `now.md` into the current-state page, brings every
   `projects/<name>.md` up to date, and writes `projects/HANDOFF.md`. It
   returns a drop list: each item it removed, from the old files or the
   handoff, with its reason.
5. **Launch a subagent review loop.** The reviewer reads the rewrite
   against the commit from step 2, the drop list and the project repos:
   nothing in flight is dropped, nothing stale stays, and every fact a
   `git log` or a grep can check is checked. The rewriter fixes what the
   reviewer finds and the reviewer reads again; the loop ends when a
   review has no findings that need a change by the bar in
   `~/Projects/davids-tools/skills/start-project/review-base.md`. Then
   commit `projects/`.
6. **Rename this session to "Previous main agent".**
7. **The user opens the new session from the Mac.** Give them its first
   prompt in a code block they can copy:

   ```
   Read ~/Projects/davids-tools/projects/HANDOFF.md
   ```

   They open it with no project folder, since it then shares no repo's
   memory directory. They name the session "Main agent" and pins it. The
   successor makes the first move that `HANDOFF.md` sets out, and once
   the user is satisfied with what it sees, it unpins and archives the
   previous main agent.
