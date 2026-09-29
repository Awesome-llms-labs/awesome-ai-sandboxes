# Awesome AI Sandboxes [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> The comprehensive, up-to-date directory of **AI sandboxes / coding agent sandboxes** — sandboxed environments where AI agents can safely execute code, run tools, browse the web, and do real work.

The sandbox is the agent's computer: an isolated, ephemeral (or persistent) environment with a filesystem, shell, and network, purpose-built for running untrusted AI-generated code. This list tracks every notable product in the space as of **September 2026**.

**Tags:** `agent-first` = explicitly built for AI agents · `OSS` = open source / self-hostable · `browser` = browser automation

## Contents

- [Managed Code Sandboxes](#managed-code-sandboxes) — cloud sandboxes purpose-built (or widely used) for AI agents
- [Open-Source & Self-Hosted Runtimes](#open-source--self-hosted-runtimes) — build your own sandbox layer
- [Browser Sandboxes](#browser-sandboxes) — cloud browsers for web-browsing agents
- [Adjacent: Cloud Dev Environments](#adjacent-cloud-dev-environments) — dev environments positioned for agents
- [Status Changes](#status-changes) — acquisitions, shutdowns, pivots
- [Guides](#guides)
- [Related Lists](#related-lists)
- [Contributing](#contributing)
- [License](#license)

---

## Managed Code Sandboxes

Cloud services that give your agent an isolated computer on demand.

- [E2B](https://e2b.dev) `agent-first` `OSS` — Cloud sandboxes for AI agents on Firecracker microVMs; sub-200ms starts, custom templates, desktop (computer-use) sandboxes, 24h sessions. Open-core: runtime Apache-2.0 ([e2b-dev/E2B](https://github.com/e2b-dev/E2B), ~14k stars). Hobby free + $100 credit; Pro $150/mo + per-second usage. $21M Series A (Insight, 2025). Customers: Hugging Face, Meta, Manus, Groq, Lindy, Genspark, Gumloop, LMArena.
- [Daytona](https://daytona.io) `agent-first` — "Composable computers for AI agents": sub-90ms creation, sandbox fork/snapshots, git/LSP/file APIs, ComputerUse interface, MCP server, Docker-in-Docker, GPU. Python + TypeScript SDKs. $24M Series A (FirstMark, Feb 2026). Customers: LangChain, Turing, Writer, SambaNova, Mintlify. ⚠️ Production codebase went closed-source Jun 2026 (was AGPL).
- [Modal](https://modal.com) — Serverless cloud for AI workloads; sandboxes give agents isolated code execution alongside GPU autoscaling (0→1000+ GPUs). gVisor-on-KVM isolation, per-second billing. $355M Series C at $4.65B (May 2026); ~$300M ARR with sandboxes >1/3 of revenue. Customers: DoorDash, Cognition, Suno, Runway, Lovable, Quora, Ramp.
- [Vercel Sandbox](https://vercel.com/docs/vercel-sandbox) `agent-first` — Firecracker microVMs for running untrusted/AI-generated code, native to Vercel. Millisecond starts, persistent sandboxes, snapshots, live preview URLs, credential-brokering firewall. SDK open source ([vercel/sandbox](https://github.com/vercel/sandbox)). Active-CPU pricing + memory; GA Jan 2026.
- [Cloudflare Sandbox SDK](https://developers.cloudflare.com/sandbox) `agent-first` `OSS` — "A full computer for AI agents": stateful code execution on Cloudflare's network — shell/filesystem/background processes, snapshots to R2, PTY terminal, live preview URLs, per-sandbox egress credential tokens. SDK open source ([cloudflare/sandbox-sdk](https://github.com/cloudflare/sandbox-sdk)). Billed on Workers/Containers usage; sleeps when idle.
- [Runloop](https://runloop.ai) `agent-first` — Enterprise-grade devbox infra for AI coding agents: custom-hypervisor microVMs, sub-2s startup for 10GB images, 10k+ parallel sandboxes, snapshot/branch ("Git for agent state"), suspend/resume, Public Benchmarks (SWE-bench), Repository Connect. Python + TypeScript SDKs. $7M seed (2025); founders ex-Stripe.
- [Blaxel](https://blaxel.ai) `agent-first` — "AWS for AI agents": perpetual microVM sandboxes with ~25ms suspend/resume at $0 standby cost, 50k+ concurrent, Agent Drive distributed filesystem, MCP co-hosting. $7.3M seed (First Round, YC S25). Customers: Webflow, Shortwave, Strapi, Sapiom. 🔀 **Acquired by Baseten, Sep 2026** — Sandboxes become a Baseten primitive.
- [Together Code Sandbox](https://codesandbox.io) (ex-CodeSandbox) `agent-first` — MicroVM cloud sandboxes with hibernate/resume/fork, VM cloning in <2s ("git branch for VMs"), preview URLs. TypeScript SDK. 🔀 **Acquired by Together AI**; repositioned from browser IDE to agent sandbox infra.
- [Deno Sandbox](https://deno.com) — Programmatic JS/TS sandbox hosting on Deno Deploy's subhosting API: V8-isolate execution, `@deno/sandbox` TS SDK + `deno-sandbox` Python SDK. ⚠️ Subhosting v1 shut down Jul 20, 2026; v2 API is current.
- [Sprites](https://sprites.dev) (Fly.io) — Persistent, hardware-isolated Linux computers on Fly.io's Firecracker fleet: live checkpoints (~300ms copy-on-write), dynamic resources to 8 CPU/16GB, per-Sprite HTTPS URLs, L3 egress policies. JS/Go SDKs, CLI, REST. $0.07/CPU-hr.
- [Northflank](https://northflank.com) — Full-stack AI infra with microVM sandboxes on Northflank cloud **or your own cloud (BYOC)**: selectable Kata/Firecracker/gVisor isolation, any OCI image, GPU sandboxes (L4/A100/H100), preview environments. TS/Python/REST/CLI. Customers: Sentry, Writer, Weights.
- [Beam](https://beam.cloud) `agent-first` `OSS` — Open-source GPU sandboxes with checkpoint restore for agents and RL workloads: Docker-in-Docker, durable task queues, per-second billing. AGPL-3.0 ([beam-cloud](https://github.com/beam-cloud)). ~$3.6M seed (Tiger Global, YC).
- [Freestyle](https://freestyle.sh) `agent-first` — Full Linux VMs for AI agents with sub-600ms provisioning, live fork (clone a running VM without pausing), hibernation (storage-only billing while paused), nested KVM, multi-tenant Git, custom domains. Investors: Floodgate, Y Combinator. Customers: Onlook, Wordware, Rork.
- [Riza](https://riza.io) `agent-first` — AI-first code-execution API on a sandboxed WebAssembly runtime: code runs <10ms after POST, per-request env/network config, no cold starts; Python/TypeScript/Go SDKs; self-host option. Pay-per-call. $2.7M funding; founders ex-Twilio/Stripe/Retool.
- [Val Town](https://val.town) — Serverless TypeScript "vals" on V8 isolates: <100ms execution, persistent code+data, HTTP endpoints, cron. Widely used as a quick agent-script runtime. Free tier + usage-based.
- [Upstash Box](https://upstash.com) `agent-first` — Container sandboxes billed on active CPU only (memory free): ~2.5s create / ~0.4s resume, filesystem+env+git state preserved, Claude Code/Codex/OpenCode/Cursor preinstalled.
- [Baponi](https://baponi.ai) `agent-first` — Per-execution sandboxes with zero idle cost: nsjail isolation, sessions resume days/weeks later, your S3/GCS/Azure bucket as filesystem, per-sandbox kernel network policies, MCP + REST + Python SDK, LangChain/OpenAI/Anthropic integrations. Free 1,000 credits/mo; Pro $97/mo; enterprise self-hosted.
- [Tensorlake](https://tensorlake.ai) `agent-first` — "Lightspeed AI-native sandboxes": Firecracker/Cloud Hypervisor microVMs, <300ms startup, snapshot/clone/replicate running sandboxes, durable orchestration (fan-out/retries/queues), 10k+ concurrent RL envs. SOC 2 Type II + HIPAA; BYOC. Customers: SIXT, Reliant AI.
- [Islo](https://islo.dev) `agent-first` — Long-running AI sandboxes for coding agents with gateway security controls: network policies, credential injection, LLM-as-judge filters, AWS IAM assume-role, GitHub/Slack/Linear/Jira integrations, dedicated microVMs, GPU. Python/TypeScript/Go/Rust SDKs. BYOC.
- [Morph](https://morph.so) `agent-first` — Cloud infra for AI agents: full VM instances, instant environment branching + snapshot/restore, millisecond deploys. Used for SWE-bench, RL rollouts, computer-use agents. Python + TypeScript SDKs.
- [Leap0](https://leap0.dev) `agent-first` — Firecracker microVMs in ~100ms with desktop/computer-use and LSP; BYOC/on-prem. Free in preview.
- [Novita AI Agent Sandbox](https://novita.ai) `agent-first` — Fast cloud sandboxes + browser/desktop use, with **E2B-compatible SDKs** for drop-in migration. Per-second usage.
- [InstaVM](https://instavm.io) `agent-first` — MicroVM platform for code execution, browser automation, and app previews on Firecracker. Python/TS/CLI/REST. Free $50 credits; BYOC/self-host.
- [Declaw](https://declaw.ai) `agent-first` — Firecracker sandboxes plus a 6-stage security pipeline (PII redaction, prompt-injection defense, TLS interception, audit). Python/TS/Go/CLI. $300 free credits; self-host on AWS/GCP.
- [Tenki Sandbox](https://tenki.cloud) `agent-first` — Disposable hardware-isolated Linux VMs for coding agents; BYO-agent (Claude Code, Codex). TS/Python/Go SDKs. Starter free ($10/mo credits); Team $200/mo.
- [Runtime](https://withruntime.com) `agent-first` — Firecracker microVM per SDK call with pause/wake memory persistence; **E2B SDK compatible**. TS/Python/Go/Java/Ruby SDKs.
- [Box by ascii.dev](https://box.ascii.dev) `agent-first` — Simple, affordable full-VM sandboxes (EU regions): dedicated Ubuntu VMs, agent-friendly CLI with JSONL output, SSH/SCP, fork, stop-to-pause-billing, 60fps desktop streaming, built-in Claude Code/Codex harness. From $20/mo, per-second.
- [OpenComputer](https://opencomputer.dev) `agent-first` — Persistent cloud VMs for AI agents that hibernate when idle and wake in seconds: instant checkpoints (snapshot/fork/rollback), works with the Claude Agent SDK. Pay-per-minute.
- [Qbox](https://qbox.sh) `agent-first` — Self-hostable Firecracker microVM sandbox orchestrator for AI agents: runs on your own Linux hosts, persistent volumes, HTTPS preview port-forwarding, browser sessions over CDP, templates from any OCI image. Free to self-host.
- [Docker Sandboxes](https://www.docker.com) `agent-first` — MicroVM-based execution environments for AI agents with Docker AI Governance (MCP governance + org policy enforcement). Announced Aug 2026.
- [Superserve](https://www.superserve.ai) `agent-first` `OSS` — Persistent, secure Firecracker sandboxes: <200ms startup, unlimited sessions, credentials broker, versioned filesystem with snapshot/rollback. Apache-2.0, TS + Python SDKs.
- [OpenAI Code Interpreter / Sandbox Agents](https://platform.openai.com) — Built-in Python code execution for assistants/agents. "Sandbox Agents" (Apr 2026) lets the runtime target third-party sandboxes: Blaxel, Cloudflare, Daytona, E2B, Modal, Runloop, Vercel — a good proxy for the category's center of gravity.

## Open-Source & Self-Hosted Runtimes

The building blocks underneath most managed sandboxes — run your own.

| Runtime | Maintainer | Isolation | License | Notes |
|---|---|---|---|---|
| [Firecracker](https://github.com/firecracker-microvm/firecracker) | AWS | KVM microVMs (~150ms boot) | Apache-2.0 | Purpose-built for serverless; powers E2B, Vercel Sandbox, Sprites, most startups |
| [gVisor](https://github.com/google/gvisor) | Google | User-space application kernel + seccomp | Apache-2.0 | Powers Modal, Beam, Northflank option |
| [Kata Containers](https://github.com/kata-containers) | OpenInfra Foundation | Lightweight VMs, OCI-compatible | Apache-2.0 | QEMU/Cloud Hypervisor/Firecracker backends; powers Northflank, Daytona VM classes |
| [nsjail](https://github.com/google/nsjail) | Google | Namespaces + seccomp-bpf, zero caps | Apache-2.0 | Lighter than full VMs; powers Baponi |
| [bubblewrap](https://github.com/containers/bubblewrap) | containers org | User namespaces + seccomp | LGPL-2.1 | Flatpak heritage; common in OSS agent harnesses |
| [isolate](https://github.com/ioi/isolate) | IOI | Namespaces + cgroups + seccomp | GPL-2.0 | Competitive-programming judge standard |
| [microsandbox](https://microsandbox.dev) | microsandbox | libkrun microVMs (KVM/Hypervisor.framework/WSL2) | Apache-2.0 | Programmable microVMs, local-first; managed cloud in private beta |
| [OpenSandbox](https://open-sandbox.ai) | Alibaba | Docker/Kubernetes runtimes | Apache-2.0 | Production-grade runtime for coding agents, GUI agents, eval, RL training |
| [SmolVM](https://celesto.ai) | Celesto AI | QEMU or Firecracker | OSS | Ubuntu/Windows guests, snapshots, Python SDK + CLI |
| [Minimal](https://minimal.dev) | minimal | libkrun microVM (macOS); user namespaces (Linux) | Apache-2.0 | CLI for sandboxed dev envs + coding agents; MCP server, GitHub Action |
| [E2B runtime](https://github.com/e2b-dev/E2B) | E2B | Firecracker microVMs | Apache-2.0 | Self-host the E2B stack; BYOC/on-prem supported |
| [Beam runtime](https://github.com/beam-cloud) | Beam Cloud | gVisor or runc | AGPL-3.0 | OSS GPU sandbox runtime (managed cloud at beam.cloud) |
| [OpenHands runtime](https://github.com/All-Hands-AI/OpenHands) | All-Hands AI | Docker containers (default) | MIT | Reference OSS coding-agent execution runtime ([openhands.dev](https://openhands.dev)); Daytona partnership for elastic sandboxes |
| [AgentBox](https://github.com/topics/agent-sandbox) | community | Docker+FUSE overlay (local), microVM (cloud) | MIT | Agent sandbox from the 2026 provider comparisons |
| [h5i](https://github.com/topics/agent-sandbox) | community | Git worktrees (file/branch/port isolation) | Apache-2.0 | Rust CLI running multiple coding agents in sealed git-worktree sandboxes |
| [bashkit4j](https://github.com/tersePrompts/bashkit4j) | tersePrompts | In-process interpreter (no syscalls) | MIT | In-JVM bash sandbox for AI agents: 160+ commands in Rust, in-memory VFS, network denied by default, zero infra |
| [ComputeSDK](https://www.computesdk.com) | ComputeSDK | Provider-agnostic | — | One API over 30+ sandbox providers + a public TTI benchmark leaderboard — a router/benchmark layer, not a runtime |

> Community rows (AgentBox, h5i) are tracked via the [agent-sandbox topic](https://github.com/topics/agent-sandbox) — star the repos that look alive before depending on them.

## Browser Sandboxes

`browser` — cloud browsers for agents that need to click, scroll, and fill forms on the real web.

- [Browserbase](https://www.browserbase.com) `browser` `agent-first` — Headless browsers for scripts + AI agents, serverless: thousands of browsers in ms, Stealth (Cloudflare-verified fingerprints), managed CAPTCHA solving, Contexts API (persistent auth), Live View + Session Replay, Director (NL→code). Puppeteer/Selenium/Playwright/Stagehand/CDP. $40M Series B (Notable Capital) at $300M.
- [Steel](https://steel.dev) `browser` `agent-first` `OSS` — "Humans use Chrome, Agents use Steel": OSS browser API ([steel-dev/steel-browser](https://github.com/steel-dev/steel-browser), Apache-2.0, ~7.6k stars). Sessions to 24h, proxies, stealth, auto CAPTCHA solving, live viewers + replays, persistent cookies, computer-use integrations. Self-host with `docker run` or use the cloud.
- [Anchor Browser](https://anchorbrowser.io) `browser` `agent-first` — Cloud browsers on a custom "humanized Chromium" fork: 50k concurrent/customer, Cloudflare Verified bot status, b0.dev (NL→deterministic workflows), SOC 2/ISO 27001/HIPAA/GDPR. $6M seed (Blumberg, Gradient). Customers: Groq, Unify, browser-use.
- [Kernel](https://www.kernel.sh) `browser` `agent-first` — Unikernel-based browser cloud: <325ms cold starts (Unikraft unikernels), agent auth platform, hosted MCP server, session persistence. Playwright/CDP/WebDriver BiDi. $22M Series A (Accel).
- [Browserless](https://www.browserless.io) `browser` — Veteran hosted/self-hosted headless Chrome (since 2017): Docker self-host, Live View. Puppeteer/Playwright/Selenium/CDP. Source-available (SSPL-1.0). General automation, widely adopted by agent stacks.
- [Hyperbrowser](https://hyperbrowser.ai) `browser` `agent-first` — Cloud browsers and sandboxes for AI automation: sessions + scraping/crawl APIs. Playwright/Puppeteer/CDP.
- [Airtop](https://www.airtop.ai) `browser` `agent-first` — Agent Builder: natural-language workflows compiled to deterministic agents on cloud browsers. Authenticated sessions, password vault, residential proxies, CAPTCHA handling, human-in-the-loop Live View, n8n/Zapier/Make/Claude Code/Codex integrations. SOC 2 II + HIPAA. 🔀 Pivoted from Switchboard (remote collaboration, $25M Series A 2022).
- [BrowserStation](https://github.com/ReinforceNow/browserstation) `browser` `agent-first` `OSS` — OSS K8s-native Browserbase alternative: Chrome sidecars exposing CDP, Ray orchestration. MIT (~166 stars).
- [Cloudflare Browser Run](https://developers.cloudflare.com/browser-rendering/) `browser` — Headless Chrome on Cloudflare's network: Puppeteer/Playwright/CDP/Stagehand, REST screenshot/PDF/markdown. Workers pricing.
- [Bright Data Browser.ai](https://brightdata.com/ai/agent-browser) `browser` — Serverless browsing with built-in unblocking: 155M+ residential IPs, CAPTCHA solving, fingerprinting. Playwright/Puppeteer/Selenium. $9.50/GB + $0.10/hr PAYG.
- [Lightpanda](https://github.com/lightpanda-io/browser) `browser` `OSS` — Headless browser written from scratch (Zig) for machines, not humans. AGPL-3.0 (~34.4k stars); beta with partial web-API coverage.

## Adjacent: Cloud Dev Environments

Not sandboxes per se, but cloud dev environments genuinely positioned for (or widely used by) coding agents.

- [GitHub Codespaces](https://github.com/features/codespaces) — Devcontainers-as-VMs used by coding agents (Cursor et al.); free 120 core-hrs/mo.
- [Coder](https://coder.com) `OSS` — Governed workspaces for human + AI-agent hybrid teams: Agent Boundaries, AI Bridge, Coder Tasks; air-gapped/DoD ready; Terraform-provisioned on customer infra. OSS ([coder/coder](https://github.com/coder/coder)). $90M Series C (KKR, Apr 2026); 300% YoY bookings.
- [Ona](https://ona.com) (ex-Gitpod) — Pivoted Sep 2025 to an AI agent platform: sandboxed ephemeral remote envs, command deny list, audit logs. 🔀 **Acquired by OpenAI, Jun 2026** (team joined the Codex group). Gitpod Classic PAYG sunset Oct 2025.
- [DevPod](https://devpod.sh) `OSS` — Local-first devcontainers in any cloud/K8s. OSS ([loft-sh/devpod](https://github.com/loft-sh/devpod)); agent-adjacent.
- [Okteto](https://okteto.com) — Remote K8s dev environments; added "Agentic Workflows" docs. OSS CLI. Independent (no acquisition as of Sep 2026).
- [Replit](https://replit.com) — Replit Agent 4 (vibe-coding agent), one-click deploy, built-in DB/auth on cloud containers/VMs. $250M (Sep 2025) + $400M Series D (Mar 2026, Georgian) at **$9B**; 50M+ users; customers Zillow, Databricks, PayPal, Adobe.
- [StackBlitz WebContainers](https://stackblitz.com) — In-browser Node.js runtime (WASM); used for agent demos/playgrounds.
- [Hugging Face Spaces](https://huggingface.co/spaces) — Hosted Gradio/Streamlit/Docker apps; common for agent demos, not marketed as a sandbox. 🔀 **NVIDIA agreed to acquire Hugging Face for $12.9B, Sep 2026.**

## Status Changes

The market is consolidating fast. Full log: [docs/status-changes.md](docs/status-changes.md).

| Product | Status | Detail |
|---|---|---|
| Blaxel | 🔀 Acquired | Baseten acquired Blaxel (~Sep 10, 2026); Sandboxes become a Baseten primitive |
| CodeSandbox | 🔀 Acquired | Acquired by Together AI → "Together Code Sandbox" |
| Gitpod → Ona | 🔀 Rebranded, then acquired | Rebranded to Ona (Sep 2025, AI-agent pivot); OpenAI acquiring Ona (Jun 2026) |
| Hugging Face | 🔀 Being acquired | NVIDIA agreed to acquire for $12.9B (Sep 2026) |
| Daytona | ⚠️ Closed-sourced | Pivoted 2024 to agent infra; production codebase closed-source Jun 2026 (was AGPL) |
| Deno Subhosting v1 | 🛑 Sunset | v1 API + Deploy Classic shut down Jul 20, 2026; replaced by v2 API + `@deno/sandbox` |
| Switchboard → Airtop | 🔀 Pivoted | Remote-collaboration Switchboard pivoted to AI browser automation as Airtop |
| Modal | 💰 Fundraising | Reportedly in talks to raise at ~$15B (Sep 2026), 4 months after $4.65B Series C |

## Guides

- [Choosing a sandbox](docs/choosing-a-sandbox.md) — decision framework: isolation level, latency, session length, BYOC, GPU, browser, pricing model
- [Isolation technologies](docs/isolation-technologies.md) — Firecracker vs gVisor vs Kata vs nsjail vs WASM isolates vs full VMs
- [Status changes](docs/status-changes.md) — acquisitions, shutdowns, and pivots log
- [Glossary](docs/glossary.md) — terms you'll meet (microVM, checkpoint, snapshot/fork, egress, BYOC…)

Machine-readable: [`data/sandboxes.json`](data/sandboxes.json) — every entry, kept in sync with this README.

## Related Lists

- [tizkovatereza/awesome-ai-sandboxes](https://github.com/tizkovatereza/awesome-ai-sandboxes) — curated, officially-sourced list (updated Sep 2026)
- [msyvr/awesome-agent-sandboxes](https://github.com/msyvr/awesome-agent-sandboxes) — sandboxes reference docs
- [data-advantage/vibereference — code execution sandbox providers](https://github.com/data-advantage/vibereference/blob/HEAD/content/ai-development/code-execution-sandbox-providers.md) (updated Sep 2026)
- [feder-cr/aihawk — browserbase alternatives](https://github.com/feder-cr/aihawk/blob/HEAD/docs/browserbase-alternatives.md) & [cloud browser infrastructure for AI agents](https://github.com/feder-cr/aihawk/blob/HEAD/docs/cloud-browser-infrastructure-for-ai-agents.md)
- [Upstash — AI agent sandbox providers compared (2026)](https://upstash.com/blog/ai-agent-sandbox-providers-compared-2026) — vendor-authored 15-provider comparison; treat cost claims as vendor-framed

## Contributing

PRs welcome! See [CONTRIBUTING.md](CONTRIBUTING.md). Every entry should link the official site and, where claimed, an independent source. The list is refreshed against the market — if a product pivots, shuts down, or gets acquired, open a PR updating its entry and the [status changes log](docs/status-changes.md).

## License

[MIT](LICENSE) © 2026. Facts (names, prices, funding) are cited from public sources as of September 2026; treat pricing as list prices at read time.
