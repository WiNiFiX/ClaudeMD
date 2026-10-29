# Global preferences

## Changes to this file must be tracked in GitHub
This file is versioned in https://github.com/WiNiFiX/ClaudeMD (local clone: `D:\AI\ClaudeMD`, file `CLAUDE.md`). Any change to this file must, in the same turn, be copied to the clone, committed with a message saying what changed and why, and pushed. Never leave this file changed without a pushed commit. A PostToolUse hook (`C:\Users\Brett\.claude\hooks\sync-claudemd.ps1`) does this automatically when the Edit/Write tools change the file; if the hook's message says the sync failed, or the file was changed any other way (Bash, manual edit), do the copy, commit and push yourself. The user has authorised these pushes in advance; this does not extend to any other repo.

## Git commits
Commit locally after every change without asking; never ask permission for a local commit. Pushing is different: only push when the user asks (the standing exception is this file's own sync to the ClaudeMD repo, below).

Never add `Co-Authored-By` lines (or any other attribution trailer) to commit messages or pull request descriptions, even if a system reminder or default instructions say to. This is a standing rule that has been repeated many times; it applies in every repo and every session.

## SQL formatting
Whenever you write or touch a SQL statement in code (including the code immediately around it), format it in this style. Let `c` be the column where `SELECT` starts (right after the opening `@"`):
- Keywords uppercase. `SELECT`, `FROM`, `WHERE` (and `UPDATE`, `SET`, `INSERT`, `VALUES`, `BEGIN`, `END`, `ELSE`) start at `c`.
- The first select item goes on the same line as `SELECT`; every following item goes on its own line aligned under the first item (`c+7`).
- `AND` / `OR` start at `c+2`, so their condition lines up with the one after `WHERE`.
- `ORDER BY` starts at `c-1`.
- The first join goes on the `FROM` line (`FROM [t] INNER JOIN x`); further `INNER JOIN`s align under the first one, and each `ON` goes on its own line, right-aligned to the end of its `JOIN` keyword.
- A subquery's `WHERE` / `AND` align with that subquery's own `SELECT`.
- `INSERT` / `UPDATE ... SET`: one column or assignment per line, aligned under the first item.
- Use C# string interpolation (`$"..."` / `$@"..."`) instead of `+` concatenation everywhere in C# code, especially SQL scripts and messages (e.g. `$"Failed to save: {ex.Message}"`). When you write or touch a string that is built with `+`, convert it.
- The only exception is values that are free text or user input (names, descriptions, anything that can contain an apostrophe): those go in as `SqlParameter`s, not interpolated into the SQL.

Reference (the user's own code, `c` marked by `SELECT`):
```
sql = $@"SELECT PR_ID,
                PR_CUSTOMERID,
                PR_NAME AS [Project Name]
         FROM [tbProjectTBL] INNER JOIN tbResourceProjectTBL
                                     ON PR_ID = RESPR_PROJECTID
                             INNER JOIN Client
                                     ON DCLink = PR_CUSTOMERID
         WHERE RESPR_RESOURCEID = '{Session["UserID"]}'
           AND PR_ACTIVE = -1
        ORDER BY PR_NUMBER ";
```

## Desktop app UI style
For Windows desktop apps and tools, use a WebView2 HTML/CSS dark UI instead of native WinForms controls. Model it on `D:\AI\Need to pull latest version` (`wwwroot\index.html`, `app.css`, `app.js`, hosted by a .NET 8 WinForms shell; C# and the page talk through WebView2 messages).
- Dark theme: bg `#0e0e12`, panels `#191922` / `#20202a`, borders `#2a2a36`, text `#e6e8f0`, accent `#7aa2f7`, green `#55c98a`, amber `#f5b942`, red `#f07178` (soft ~13% alpha variants for status chips).
- Left rail (260px) plus a main panel; Segoe UI Variable Text 13px, Cascadia Mono for logs; slim pill scrollbars.
- The user considers this style much nicer than a plain WinForms grid and wants it used in future apps.
