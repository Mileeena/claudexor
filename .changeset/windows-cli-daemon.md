---
"@claudexor/core": minor
"@claudexor/util": minor
"@claudexor/cli": minor
"@claudexor/daemon": patch
"@claudexor/journal": patch
"@claudexor/workspace": patch
"@claudexor/harness-codex": patch
---

Run the CLI and daemon on Windows 10/11 x64. Identity guards no longer compare `stat.dev` between a descriptor and a path on win32, where libuv's path stat reports 0 on Windows 11 24H2 with Node 22 and every owned-root check failed. A default `npm install -g` vendor CLI now resolves and runs: a recognized npm cmd-shim is launched as `process.execPath <script>` (or its direct `.exe`) without a shell (#191). Harness children stay attached with a hidden console instead of `DETACHED_PROCESS`, so a vendor's console grandchildren no longer open windows. The harness PATH drops POSIX drive-root folders on win32 and reads a `Path`-cased copy, git children get `core.longpaths` through env-scoped config so deep worktrees clone past MAX_PATH, and the daemon survives a stderr write after its launcher drops the pipe. The journal compaction cases skipped for #190 run on the Windows lane again, which now also runs the canary stories.
