# CodeTrellis — Releases

Public installer downloads for **CodeTrellis** — a desktop app that
visualises your codebase architecture and monitors AI coding agents
(Claude Code, Codex, Cursor, aider, any MCP client) in real time.

The source repository is **currently private** while we collect
feedback and clean up before the public source release. Watch this
space — we'll announce when the source goes live.

## Download

Latest installers live on the **[Releases page](https://github.com/lionroseway/codetrellis-releases/releases/latest)**.

| Platform | File | Notes |
|---|---|---|
| macOS (Apple Silicon) | `CodeTrellis-<version>-arm64.dmg` | Drag to /Applications |
| macOS (Intel) | `CodeTrellis-<version>-x64.dmg` | Drag to /Applications |
| Windows installer | `CodeTrellis-Setup-<version>.exe` | NSIS — installs into Programs |
| Windows portable | `CodeTrellis-Portable-<version>.exe` | Run anywhere, no install |
| Linux (.deb) | `CodeTrellis-<version>.deb` | Debian, Ubuntu, Mint |
| Linux (AppImage) | `CodeTrellis-<version>.AppImage` | Fedora, RHEL, Arch — `chmod +x` then run |

### First-launch warnings

Builds are **not yet code-signed**, so the OS will warn you before
the first launch. This is expected — bypass it once and the warning
won't repeat.

- **macOS**: right-click `CodeTrellis.app` → **Open** → **Open** in the dialog. Or System Settings → Privacy & Security → "Open Anyway".
- **Windows**: SmartScreen blocks unsigned installers — click **More info** → **Run anyway**.
- **Linux (.deb)**: `sudo dpkg -i CodeTrellis-<version>.deb`
- **Linux (AppImage)**: `chmod +x CodeTrellis-<version>.AppImage && ./CodeTrellis-<version>.AppImage`

## What is CodeTrellis?

A desktop tool that sits alongside AI coding agents and gives you
real-time visibility into what they're doing to your codebase:

- **Dependency graph** — packages → files → classes/functions, with
  cross-system HTTP/SQL coupling overlaid
- **Plan rooms** — author multi-phase plans with spec docs, share
  them via MCP so the agent picks them up
- **Live agent monitoring** — every tool call from any MCP-connected
  agent shows up in the timeline with attribution
- **Architecture diffing** — see drift the moment the agent writes a
  file; flag deviations from the plan automatically
- **Multi-language** — TypeScript, JavaScript, Python, Rust, PHP, Java
  via tree-sitter

Learn more at [codetrellis.dev](https://codetrellis.dev).

## Feedback

The source repo isn't open yet, but we're actively collecting
feedback to harden the product. Please file issues on this repo
([new issue](https://github.com/lionroseway/codetrellis-releases/issues/new))
or reach out directly. Bug reports, feature requests, and
"this confused me" notes all welcome.

## License

CodeTrellis is licensed under the **Apache License 2.0**. The full
license text will be included in the source repo when it goes public.
