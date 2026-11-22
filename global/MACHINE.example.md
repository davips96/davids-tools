# [Name]'s machine

Private: git ignores this file. Facts about the computer every project
runs on. macOS quirks that hold on any Mac are in `global/MACOS.md`; a
project's own quirks stay in that project's docs; what is true in every
project is here.

<!--
This is the template. The setup-toolkit skill copies it to
global/MACHINE.md and fills it in, mostly by checking the machine itself
(system_profiler, sw_vers, security find-identity, pmset, which). Replace
every bracket; drop a line that doesn't apply.
-->

- **[Chip], [RAM], macOS [version].** [What that bounds: native
  architecture, which local models run well.]
- **Code signing: [identities, or none].** [What they allow: local signing,
  notarized distribution.]
- **Developer mode is [on/off]** (`DevToolsSecurity -status`).
- **Claude Code runs in [the desktop app / a terminal]**[, and the user
  follows sessions from their phone over Remote Control].
- **During away sessions the Mac [stays awake on its own / needs a
  keep-awake].** [Charger, lid, Claude Desktop's keep-awake setting.]
- **The display [stays on / sleeps after N minutes] on power** (`pmset -g
  custom`). [On battery: …]
- **Shell: [zsh/bash].**
- **Repos live in `~/Projects/`.** This toolkit is at
  `~/Projects/davids-tools`; `~/.claude/CLAUDE.md` and `~/.claude/skills`
  are symlinks into it.
- **[Language runtimes and their gaps, for example: Python has no PIL.]**
- **[Docker, Xcode and the iOS simulator, other tools installed.]**
- Tools and paths that serve one project are in that project's
  `CLAUDE.md`.
