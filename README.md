# CodeTrellis

> A way to plan, watch, and keep AI coding agents on track — and a
> way to keep yourself on track too, even when no agent is involved.

[![Latest release](https://img.shields.io/github/v/release/lionroseway/codetrellis-releases?label=latest&color=blue)](https://github.com/lionroseway/codetrellis-releases/releases/latest)
[![License](https://img.shields.io/badge/license-Apache%202.0-green)](LICENSE)
[![Source](https://img.shields.io/badge/source-private%20%28for%20now%29-lightgrey)](#source)

---

## ⬇️ Download

| Platform | File |
|---|---|
| **macOS — Apple Silicon** | [`CodeTrellis-0.1.0-arm64.dmg`](https://github.com/lionroseway/codetrellis-releases/releases/latest/download/CodeTrellis-0.1.0-arm64.dmg) |
| **macOS — Intel** | [`CodeTrellis-0.1.0-x64.dmg`](https://github.com/lionroseway/codetrellis-releases/releases/latest/download/CodeTrellis-0.1.0-x64.dmg) |
| **Windows — installer** | [`CodeTrellis-Setup-0.1.0.exe`](https://github.com/lionroseway/codetrellis-releases/releases/latest/download/CodeTrellis-Setup-0.1.0.exe) |
| **Windows — portable** | [`CodeTrellis-Portable-0.1.0.exe`](https://github.com/lionroseway/codetrellis-releases/releases/latest/download/CodeTrellis-Portable-0.1.0.exe) |
| **Linux — x64** | [`CodeTrellis-0.1.0.AppImage`](https://github.com/lionroseway/codetrellis-releases/releases/latest/download/CodeTrellis-0.1.0.AppImage) |
| **Linux — ARM** | [`CodeTrellis-0.1.0-arm64.AppImage`](https://github.com/lionroseway/codetrellis-releases/releases/latest/download/CodeTrellis-0.1.0-arm64.AppImage) |

All builds + release notes live on the **[Releases page →](https://github.com/lionroseway/codetrellis-releases/releases/latest)**

### First-launch warnings

The builds aren't yet code-signed, so the OS will warn you the first
time. This is expected — bypass it once and the warning won't
repeat.

- **macOS** — right-click `CodeTrellis.app` → **Open** → **Open** in the dialog. (Or System Settings → Privacy & Security → "Open Anyway".)
- **Windows** — SmartScreen blocks unsigned installers — click **More info** → **Run anyway**.
- **Linux** — `chmod +x CodeTrellis-0.1.0.AppImage && ./CodeTrellis-0.1.0.AppImage`. Works on Debian, Ubuntu, Fedora, RHEL, Arch — no install needed.

### Linux AppImage on Ubuntu 24.04+

Ubuntu 24.04 tightened AppArmor's unprivileged user-namespace policy, which breaks Chromium's setuid sandbox in AppImages. If you see:

```
FATAL:setuid_sandbox_host.cc(...) The SUID sandbox helper binary
was found, but is not configured correctly.
```

…the workaround is to launch with `--no-sandbox`:

```bash
./CodeTrellis-0.1.0.AppImage --no-sandbox
```

This is the same workaround Cursor, Obsidian, and most other Electron AppImages use on modern Linux. For a local dev tool loading your own bundled HTML, the practical risk is negligible. **From v0.1.1 onwards** the desktop app does this automatically when launched from an AppImage — so the workaround only applies to v0.1.0.

---

## Why I built it

I prefer to focus on architecture and conformity. When I started
working with AI coding agents I noticed two things really fast:

1. The sessions where I got the cleanest output were the ones where
   I'd put serious effort into the **plan first** — defining the
   CRUD blocks, mapping how things connected, writing the executive
   summary, the architecture doc, the UX journey, the testing
   parameters, the success metrics. The more I scaffolded up front,
   the less the agent drifted.
2. Even with a great plan, the agent would still wander — picking up
   weird side-quests, forgetting earlier decisions, occasionally
   undoing what it had just built.

So I started building CodeTrellis as an internal tool to track the
plans I was making and watch what the AI was doing in real time. If
I asked it to centralise a service or refactor a module, I wanted to
know it was actually still on that plan and not somewhere else.

That grew into what's here now.

The "AI agent harness" idea has been picking up. CodeTrellis is my
own take on it — one that's simple, gets out of the way, and works
**with or without an AI agent**. If you're not doing AI-assisted
development at all, it's still useful as a way to track your own
work against a plan and see what's actually changing in your
codebase.

## What it does

- **Visualises your codebase** as a dependency graph — packages,
  files, and symbols (functions, classes, methods), with cross-system
  edges where one service calls another over HTTP/SQL.
- **Lets you write plans** that scale from a one-line "do this thing"
  to multi-phase migrations with spec docs, acceptance criteria,
  prerequisites, and templates. As simple or as complex as you want.
- **Hosts a local MCP server** so any MCP-capable AI agent — Claude
  Code, Codex, Cursor, aider, anything that speaks MCP — can read
  the plan, ask questions about your architecture, and report what
  it's doing.
- **Watches your repo via git** and shows you exactly what changed,
  diffed against any commit you pick. The whole core ethos is built
  on version control — you can be as high-level or low-level as you
  want.
- **Surfaces drift** in real time — if the agent wrote a file that's
  not in the plan, or the plan said "create function X" and that
  function still doesn't exist, you see it.

## How I actually use it

These are real workflows that have shifted my hit-rate with AI
agents. Your mileage will vary, but they're the shape of what's
possible.

- **Re-running a plan with a different agent.** I run a plan with one
  agent, don't love the output, then point a different agent at the
  same plan and see how it does. The plan stays put; the executor
  changes.
- **Splitting work across agents.** Claude for the heavy refactor,
  Codex for the test scaffolding, Cursor for the UI tweaks — each
  agent owning specific parts of the plan. Useful for picking the
  best tool per job, and for working around per-agent usage limits.
- **Recursive runs.** I set up an agent to work the plan, then let
  it loop until it hits a stop condition. Every tool call lands in
  the timeline so I can review the run after the fact.
- **High-level monitoring.** When an agent is mid-build I keep the
  graph open. If I see the blast radius spreading somewhere it
  shouldn't, I can interrupt, give feedback, and steer it back —
  this has saved me from a lot of "now I'm in too deep" moments.
- **Context refresh.** When an agent's context starts to thrash, I
  clear it out and have it re-ingest the plan from MCP. Same for
  switching machines — the plan is on disk, not in some browser
  tab, so I can pick up on a different device and an agent there
  reads the same source of truth.

## Privacy & cost

This is the part I want to be very direct about:

- **The app sends no data anywhere.** It scans your local repo,
  writes to a local SQLite file, and runs a local MCP server. No
  telemetry, no cloud, no analytics, nothing leaves your machine.
- **All AI features are powered by your AI agent**, not CodeTrellis.
  The agent connects to CodeTrellis over MCP locally; the AI
  processing happens inside whatever agent you're using.
- **AI costs come out of your existing AI usage.** Because CodeTrellis
  uses MCP, the agent calls the local MCP server to build plans,
  get architecture context, address drift — all of that traffic
  stays between you and your agent. **There is no TOS violation** —
  you're using your own agent the way you already do, just with
  more structure.
- **Data concerns** — manage them where you already manage them: in
  the agent. CodeTrellis is just a view.

## Requirements

- **Git** installed on your machine (the diffing engine relies on it).
- **An MCP-capable AI agent** if you want the AI features (Claude
  Code, Codex, Cursor, aider, etc.). **Optional** — if you're not
  using an AI agent the app still works fine for hand-authoring
  plans and watching your own changes.

## Source

The source repository is **currently private**. I'm collecting
feedback before opening it up — bug reports, "this confused me"
moments, missing use cases, all welcome. In an ideal world the
source goes public sooner rather than later; the gate is just
hardening the rough edges based on what people hit.

Things I'd especially like feedback on:

- Are there workflows you tried that didn't fit cleanly?
- Anything that crashed or behaved weirdly?
- Plan templates you wish were built in?
- Features you assumed would be there and weren't?

[Open an issue here](https://github.com/lionroseway/codetrellis-releases/issues/new) — even a one-liner helps shape the public release.

## License

[Apache License 2.0](LICENSE).
