---
"@claudexor/core": minor
"@claudexor/util": minor
"@claudexor/cli": minor
"@claudexor/daemon": patch
"@claudexor/journal": patch
"@claudexor/workspace": patch
"@claudexor/harness-codex": patch
---

Run the CLI and daemon on Windows 10/11 x64. Identity guards no longer compare `stat.dev` between a descriptor and a path on win32, where libuv's path stat reports 0 on Windows 11 24H2 with Node 22 and every owned-root check failed. A default `npm install -g` vendor CLI now resolves and runs: a recognized npm cmd-shim (current, legacy/corepack, or Node's own npm.cmd shape) is launched as `process.execPath <script>` (or its direct `.exe`) without a shell (#191), which also lets `npm test`-style gates run; `clean` child envs on win32 now keep the OS runtime keys (`COMSPEC`, `PATHEXT`, temp and profile roots) that a cmd.exe-run package script needs. Harness children stay attached with a hidden console instead of `DETACHED_PROCESS`, so a vendor's console grandchildren no longer open windows. On win32 the harness PATH keeps the user's own order first (preferred dirs only back-fill), drops POSIX drive-root folders and reads a `Path`-cased copy; the run-owned artifact subtree is a `/`-separated pathspec so browser artifacts stay out of candidate diffs; git children get `core.longpaths` through env-scoped config so deep worktrees clone past MAX_PATH, and the daemon survives a stderr write after its launcher drops the pipe. The journal compaction cases skipped for #190 run on the Windows lane again, which now also runs the canary stories.
