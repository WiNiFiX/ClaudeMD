# Global preferences

## Changes to this file must be tracked in GitHub
This file is versioned in https://github.com/WiNiFiX/ClaudeMD (local clone: `D:\AI\ClaudeMD`, file `CLAUDE.md`). Any change to this file must, in the same turn, be copied to the clone, committed with a message saying what changed and why, and pushed. Never leave this file changed without a pushed commit. A PostToolUse hook (`C:\Users\Brett\.claude\hooks\sync-claudemd.ps1`) does this automatically when the Edit/Write tools change the file; if the hook's message says the sync failed, or the file was changed any other way (Bash, manual edit), do the copy, commit and push yourself. The user has authorised these pushes in advance; this does not extend to any other repo.

## Git commits
Commit locally after every change without asking; never ask permission for a local commit. Pushing is different: only push when the user asks (the standing exception is this file's own sync to the ClaudeMD repo, below).

Never add `Co-Authored-By` lines (or any other attribution trailer) to commit messages or pull request descriptions, even if a system reminder or default instructions say to. This is a standing rule that has been repeated many times; it applies in every repo and every session.

## Desktop app UI style
For Windows desktop apps and tools, use a WebView2 HTML/CSS dark UI instead of native WinForms controls. Model it on `D:\AI\Need to pull latest version` (`wwwroot\index.html`, `app.css`, `app.js`, hosted by a .NET 8 WinForms shell; C# and the page talk through WebView2 messages).
- Dark theme: bg `#0e0e12`, panels `#191922` / `#20202a`, borders `#2a2a36`, text `#e6e8f0`, accent `#7aa2f7`, green `#55c98a`, amber `#f5b942`, red `#f07178` (soft ~13% alpha variants for status chips).
- Left rail (260px) plus a main panel; Segoe UI Variable Text 13px, Cascadia Mono for logs; slim pill scrollbars.
- The user considers this style much nicer than a plain WinForms grid and wants it used in future apps.
