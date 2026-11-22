# macOS quirks

What holds on any Mac. Facts about the user's own machine (hardware,
identities, settings, installed tools) are in the private
`global/MACHINE.md`; a project's own quirks stay in that project's docs.

- **Signing with the login keychain can wait on an invisible prompt.**
  macOS asks whether `codesign` may use the signing key, so an unattended
  `xcodebuild`, or anything else that signs, can wait forever. Give such a
  run a time limit (macOS has no `timeout` command; the Bash tool's
  timeout works), and treat signing as needing the user at the Mac. The
  prompt has no "Always Allow" option: it asks for their password each
  time signing runs. `security find-identity -v -p codesigning` lists the
  signing identities.
- **Attaching a debugger waits on a password prompt too** while developer
  mode is off (`DevToolsSecurity -status`). Running or attaching `lldb`
  to a process shows a "Developer Tools Access" Touch ID or password
  prompt. Give such a run a time limit and treat it as needing the user
  at the Mac. When one times out, end the orphaned `debugserver`
  (`pkill -x debugserver`), since it keeps the prompt on screen. Turning
  developer mode on (`DevToolsSecurity -enable`) is the user's call.
- **Shell.** zsh's `=` quirk is in the global file's "The machine".
  `sed` is BSD sed (`-i ''`, no GNU extensions). In Claude Code's Bash,
  `grep` is a wrapper over ugrep that skips `.git` and ignored files;
  `command grep` is the system grep. To change a running shell script,
  write a new file or `mv` a new one into place: zsh and bash read a
  script as it runs, so copying or editing over it makes it go on with
  the new bytes.
- **A locked screen composites nothing,** so windowed runs and
  measurements stop when it locks. The screen locks when the display
  sleeps; `pmset -g custom` shows the display-sleep settings on power and
  on battery. A closed lid sleeps the Mac.
- **Resize images with `sips`,** which ships with macOS:
  `sips -Z 1200 in.png --out out.png` fits the longest side to 1200
  pixels.
- **iCloud Drive** is mounted at
  `~/Library/Mobile Documents/com~apple~CloudDocs/`.
