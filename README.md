<p align="center">
  <img src="docs/logo.svg" alt="Reasonix" width="640"/>
</p>

<p align="center">
  <strong>English</strong>
  &nbsp;·&nbsp;
  <a href="./README.zh-CN.md">简体中文</a>
  &nbsp;·&nbsp;
  <a href="./docs/GUIDE.md">Guide</a>
  &nbsp;·&nbsp;
  <a href="./docs/ACP.md">ACP</a>
  &nbsp;·&nbsp;
  <a href="./docs/EXTENSIONS.md">Extensions</a>
  &nbsp;·&nbsp;
  <a href="./docs/SPEC.md">Spec</a>
  &nbsp;·&nbsp;
  <a href="https://esengine.github.io/DeepSeek-Reasonix/">Website</a>
  &nbsp;·&nbsp;
  <strong><a href="https://discord.gg/XF78rEME2D">Discord</a></strong>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/reasonix"><img src="https://img.shields.io/npm/v/reasonix.svg?style=flat-square&color=cb3837&labelColor=161b22&logo=npm&logoColor=white" alt="npm version"/></a>
  <a href="https://github.com/esengine/DeepSeek-Reasonix/actions/workflows/ci.yml"><img src="https://img.shields.io/github/actions/workflow/status/esengine/DeepSeek-Reasonix/ci.yml?style=flat-square&label=ci&labelColor=161b22&logo=githubactions&logoColor=white" alt="CI"/></a>
  <a href="./LICENSE"><img src="https://img.shields.io/npm/l/reasonix.svg?style=flat-square&color=8b949e&labelColor=161b22" alt="license"/></a>
  <a href="https://www.npmjs.com/package/reasonix"><img src="https://img.shields.io/npm/dm/reasonix.svg?style=flat-square&color=3fb950&labelColor=161b22&label=downloads" alt="downloads"/></a>
  <a href="https://github.com/esengine/DeepSeek-Reasonix/stargazers"><img src="https://img.shields.io/github/stars/esengine/DeepSeek-Reasonix.svg?style=flat-square&color=dbab09&labelColor=161b22&logo=github&logoColor=white" alt="GitHub stars"/></a>
  <a href="https://atomgit.com/esengine/DeepSeek-Reasonix"><img src="https://atomgit.com/esengine/DeepSeek-Reasonix/star/badge.svg" alt="AtomGit stars"/></a>
  <a href="https://github.com/esengine/DeepSeek-Reasonix/graphs/contributors"><img src="https://img.shields.io/github/contributors/esengine/DeepSeek-Reasonix.svg?style=flat-square&color=bc8cff&labelColor=161b22&logo=github&logoColor=white" alt="contributors"/></a>
  <a href="https://github.com/esengine/DeepSeek-Reasonix/discussions"><img src="https://img.shields.io/github/discussions/esengine/DeepSeek-Reasonix.svg?style=flat-square&color=58a6ff&labelColor=161b22&logo=github&logoColor=white" alt="Discussions"/></a>
  <a href="https://discord.gg/XF78rEME2D"><img src="https://img.shields.io/badge/discord-join-5865F2.svg?style=flat-square&labelColor=161b22&logo=discord&logoColor=white" alt="Discord"/></a>
</p>

<p align="center">
  <a href="https://trendshift.io/repositories/27020?utm_source=trendshift-badge&amp;utm_medium=badge&amp;utm_campaign=badge-trendshift-27020" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/trendshift/repositories/27020/monthly?language=Go" alt="esengine/DeepSeek-Reasonix | Trendshift" width="250" height="55"/></a>
  <a href="https://trendshift.io/repositories/27020?utm_source=repository-badge&amp;utm_medium=badge&amp;utm_campaign=badge-repository-27020" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/repositories/27020" alt="esengine/DeepSeek-Reasonix | Trendshift" width="250" height="55"/></a>
</p>

<br/>

<h3 align="center">A DeepSeek-native AI coding agent for your terminal.</h3>
<p align="center">A config- and plugin-driven harness — a single static Go binary, tuned around DeepSeek's prefix cache so token costs stay low across long sessions.</p>

<br/>

> [!IMPORTANT]
> **Community · 加入社区** — bilingual Discord for setup help (`#help` / `#求助`), workflow showcases, and feature ideas. → **<https://discord.gg/XF78rEME2D>**

<br/>

## Fixed

### Sync policy

Upstream syncs land on `fork-dev` **commit by commit** (`git merge <c>` for each upstream commit in order), never as one batch merge. Conflicts are resolved per commit with the same rule: changes already adopted upstream yield to the upstream implementation; fork-unique changes are kept. This keeps every upstream change attributable and the project's evolution readable, at the cost of more work per sync.

Active fork patches on top of upstream `main-v2`:

- [`b3324cc`](https://github.com/GOGV/DeepSeek-Reasonix-Fork/commit/b3324cc) (2026-08-03) — Bash tool subprocesses now restore the OS account home as `HOME` when Reasonix itself runs with an overridden `HOME` (e.g. service launchers), so CLIs like `gh` / `arkcli` / `bl` find their credentials instead of reporting "not logged in". (upstream [issue #7331](https://github.com/esengine/DeepSeek-Reasonix/issues/7331))
- [`b481b07`](https://github.com/GOGV/DeepSeek-Reasonix-Fork/commit/b481b07a) (2026-08-04) — Provider credentials now fall back to `$HOME/.env` and then the OS account home's `.env` when the Reasonix-home `.env` is missing (e.g. `REASONIX_HOME` pointing elsewhere or a launcher overriding `HOME`), fixing `missing env X_API_KEY` / HTTP 401 in those deployments. Precedence: Reasonix credentials file > process env > `$HOME/.env` > account home `.env`; project `./.env` is still never imported. (upstream [PR #7354](https://github.com/esengine/DeepSeek-Reasonix/pull/7354))

Merged upstream — no longer carried by this fork:

- ~~[`78e1ac4`](https://github.com/GOGV/DeepSeek-Reasonix-Fork/commit/78e1ac4) (2026-08-03) — A missing or unreadable `system_prompt_file` no longer aborts startup; Reasonix warns and falls back to the inline/default system prompt.~~ → upstream [`2f16450e`](https://github.com/esengine/DeepSeek-Reasonix/commit/2f16450e399d2fc0bd6f6bb8bb9ecc858f2e124f)
- ~~[`9da8303`](https://github.com/GOGV/DeepSeek-Reasonix-Fork/commit/9da8303) (2026-08-03) — A relative `system_prompt_file` is now probed under the workspace root first (project override), then under the Reasonix home (global default); only when every location is missing does it fall back.~~ → upstream [`2f16450e`](https://github.com/esengine/DeepSeek-Reasonix/commit/2f16450e399d2fc0bd6f6bb8bb9ecc858f2e124f)
- ~~[`d0501e0`](https://github.com/GOGV/DeepSeek-Reasonix-Fork/commit/d0501e0) (2026-08-03) — When all probe locations miss, the warning names the configured value and lists every tried path.~~ → upstream [`2f16450e`](https://github.com/esengine/DeepSeek-Reasonix/commit/2f16450e399d2fc0bd6f6bb8bb9ecc858f2e124f)
- ~~[`88867aa`](https://github.com/GOGV/DeepSeek-Reasonix-Fork/commit/88867aa) (2026-08-03) — Session-title generation no longer sends `MaxTokens: 20` to reasoning models (empty titles, cache never filled, ~28s `GET /sessions`).~~ → upstream [`a3358ef8`](https://github.com/esengine/DeepSeek-Reasonix/commit/a3358ef8478c8e3ae8c1fba930c35d3df5e8f154)
- ~~[`61fa2c9`](https://github.com/GOGV/DeepSeek-Reasonix-Fork/commit/61fa2c9) (2026-08-03) — Session titles are sticky per session file instead of mtime-invalidated (no more per-poll title regeneration).~~ → upstream [`a3358ef8`](https://github.com/esengine/DeepSeek-Reasonix/commit/a3358ef8478c8e3ae8c1fba930c35d3df5e8f154)
- ~~[`e4482d8`](https://github.com/GOGV/DeepSeek-Reasonix-Fork/commit/e4482d86) (2026-08-03) — Session delete no longer fails silently: localized notice for the active session, server error text otherwise.~~ → upstream [`9549af08`](https://github.com/esengine/DeepSeek-Reasonix/commit/9549af0817a5c1f1c85491c5bed7ac8c5616547e) + [`8ddaad8b`](https://github.com/esengine/DeepSeek-Reasonix/commit/8ddaad8b9a49e8bae60502216fc47142f87b1765)

## Features

- **Config-driven.** Providers, the agent, enabled tools, and plugins are all
  declared in `reasonix.toml`. No hardcoded models.
- **Multi-model & composable.** DeepSeek ships as a preset; any
  OpenAI-compatible endpoint is a config entry, not new code. Optionally run
  two models together (executor + planner) in separate, cache-stable sessions.
- **Plugin-driven.** MCP servers contribute tools, prompts, and resources;
  Extension Protocol v1 sidecars can also intercept runtime events, contribute
  Providers and structured UI, and ship versioned plugin packages.
- **Cache-aware context maintenance.** Startup injects a small stable environment
  summary, stale tool output is snipped/pruned before summary compaction, and the
  built-in tool schema contract is documented for regression review.
- **Zero-friction distribution.** `CGO_ENABLED=0` single binary; cross-compile
  to six targets with one command. The only dependency is a TOML parser.

## Install

Choose the path that matches how you want to use Reasonix. The CLI/TUI,
desktop app, and VS Code extension all use the same local Reasonix engine.

### Path A: CLI / TUI

Install the native binary through npm on any supported platform, or use
Homebrew on macOS:

```sh
npm i -g reasonix                  # any OS; pulls the prebuilt native binary
brew install esengine/reasonix/reasonix   # macOS
```

Prebuilt archives (`darwin|linux|windows × amd64|arm64`) and `SHA256SUMS` are on
every [GitHub release](https://github.com/esengine/DeepSeek-Reasonix/releases).

### Path B: Desktop app

Use the [official download page](https://reasonix.io/?download=desktop#start)
for the latest desktop build.

| Platform | Package | Architecture |
| --- | --- | --- |
| macOS | Universal `.dmg` or `.zip` | Apple Silicon / Intel |
| Windows | Installer `.exe` or portable `.zip` | x64 / ARM64 |
| Linux | `.deb` or `.tar.gz` | x64 |

Windows installers are code-signed through [SignPath.io](https://signpath.io/)
with a free certificate provided by the [SignPath Foundation](https://signpath.org/).

### Path C: VS Code extension

Complete Path A first. The extension does not bundle the CLI; it starts your
local `reasonix acp` backend and adds native chat, editor context, tool-call
approvals, model selection, and workspace sessions.

- **VS Code:** [install from Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=SivanLiu.reasonix-agent)
- **VSCodium / Eclipse Theia:** [install from Open VSX Registry](https://open-vsx.org/extension/SivanLiu/reasonix-agent)
- **Extension ID:** `SivanLiu.reasonix-agent` · [source and usage guide](https://github.com/SivanCola/reasonix-vscode)

### Path D: Build from source

```sh
git clone https://github.com/esengine/DeepSeek-Reasonix.git
cd DeepSeek-Reasonix
make build      # -> bin/reasonix(.exe)
make cross      # -> dist/ (darwin|linux|windows × amd64|arm64)
```

## Quick start

### CLI / TUI

These commands are for the CLI/TUI installed through Path A:

```sh
reasonix setup                      # configure a provider and model
reasonix                            # start an interactive session
reasonix run "implement the TODOs in main.go"
```

In an interactive session, run `/init` when you want Reasonix to create project
instructions.

### Desktop app

Download the installer for your platform from the
[official download page](https://reasonix.io/?download=desktop#start), install
and launch Reasonix, then configure a provider and model in the app. The CLI
commands above are not required for the desktop app.

For advanced CLI usage and configuration, see the **[CLI reference](./docs/CLI.md)**,
**[Guide](./docs/GUIDE.md)**, and
**[configuration paths](./docs/CONFIG_PATHS.md)**.

## Documentation

- **Getting started:** [Guide](./docs/GUIDE.md) · [CLI reference](./docs/CLI.md) ·
  [Configuration paths](./docs/CONFIG_PATHS.md) · [ACP editor integration](./docs/ACP.md)
- **Features & troubleshooting:** [Subagent profiles](./docs/SUBAGENT_PROFILES.md) ·
  [Context Engine v2](./docs/SESSION_MEMORY_RETRIEVAL.md) ·
  [Capability diagnostics](./docs/CAPABILITY_DIAGNOSTICS.md) ·
  [Recovery and updates](./docs/RECOVERY.md) · [Bot guide](./docs/BOT_GUIDE.md) ·
  [Checkpoints & rewind](./docs/CHECKPOINTS.md)
- **Engineering & migration:** [Spec](./docs/SPEC.md) ·
  [Task contracts & pause policy](./docs/TASK_CONTRACT.md) ·
  [Tool contract](./docs/TOOL_CONTRACT.md) · [Migrating from 0.x](./docs/MIGRATING.md)
- **Extension development:** [Extensions](./docs/EXTENSIONS.md) ·
  [Plugin packages and Manifest v1](./docs/PLUGIN_PACKAGES.md) ·
  [Extension Protocol](./docs/EXTENSION_PROTOCOL.md) ·
  [Go SDK and starter](./sdk/go/README.md)

## Star History

<a href="https://www.star-history.com/?repos=esengine%2FDeepSeek-Reasonix&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/esengine/DeepSeek-Reasonix/star-history/assets/star-history/star-history-dark.svg" />
   <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/esengine/DeepSeek-Reasonix/star-history/assets/star-history/star-history-light.svg" />
   <img alt="Star History Chart" src="https://raw.githubusercontent.com/esengine/DeepSeek-Reasonix/star-history/assets/star-history/star-history-light.svg" />
 </picture>
</a>

<br/>

## Acknowledgments

A small list of folks whose work has shaped Reasonix the most — the current top
20 contributors by commit count. The full contributor graph is on
[GitHub](https://github.com/esengine/DeepSeek-Reasonix/graphs/contributors?all=1).

<!-- reasonix-top-contributors:start -->
| Contributor | Contributor | Contributor | Contributor |
| --- | --- | --- | --- |
| [**SivanCola**](https://github.com/SivanCola) | [**esengine**](https://github.com/esengine) | [**ttmouse**](https://github.com/ttmouse) | [**lifu963**](https://github.com/lifu963) |
| **reasonix** (anonymous) | [**HUQIANTAO**](https://github.com/HUQIANTAO) | [**GTC2080**](https://github.com/GTC2080) | [**light-front-theory**](https://github.com/light-front-theory) |
| **merge-order-check** (anonymous) | [**Li-Charles-One**](https://github.com/Li-Charles-One) | [**eghrhegpe**](https://github.com/eghrhegpe) | **wufengfan** (anonymous) |
| [**CVEngineer66**](https://github.com/CVEngineer66) | [**dependabot\[bot\]**](https://github.com/apps/dependabot) | [**lanshi17**](https://github.com/lanshi17) | [**SuMuxi66**](https://github.com/SuMuxi66) |
| [**CnsMaple**](https://github.com/CnsMaple) | [**cyq1017**](https://github.com/cyq1017) | [**JesonChou**](https://github.com/JesonChou) | [**XTLine**](https://github.com/XTLine) |
<!-- reasonix-top-contributors:end -->

Also a separate thank-you to [**Bernardxu123**](https://github.com/Bernardxu123)
for designing the project logo, and to
[AIGC Link](https://xhslink.com/m/80ngts127cA) for promoting the project on XiaoHongShu.

<p align="center">
  <a href="https://github.com/esengine/DeepSeek-Reasonix/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=esengine/DeepSeek-Reasonix&max=100&columns=12" alt="Contributors to esengine/DeepSeek-Reasonix" width="860"/>
  </a>
</p>

<br/>

---

<p align="center">
  <sub>MIT — see <a href="./LICENSE">LICENSE</a></sub>
  <br/>
  <sub>Built by the community at <a href="https://github.com/esengine/DeepSeek-Reasonix/graphs/contributors">esengine/DeepSeek-Reasonix</a></sub>
</p>

---

<p align="center"><sub><strong>Support this project</strong></sub></p>

If Reasonix has been useful and you'd like to say thanks, you can. It stays a
coffee, not a contract — donations don't buy feature priority or change how
issues get triaged.

- **International** — PayPal: [paypal.me/yuhuahui](https://paypal.me/yuhuahui)
- **国内** — 微信支付（扫码）

<p align="center">
  <img src=".github/sponsor/wechat-pay.jpg" alt="WeChat Pay QR code" width="180"/>
</p>
