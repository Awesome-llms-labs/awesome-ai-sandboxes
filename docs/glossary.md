# Glossary

- **Sandbox** — an isolated environment (VM, container, or isolate) where an AI agent executes code, with controlled filesystem, network, and resource access.
- **Coding agent sandbox** — a sandbox purpose-built for the coding-agent loop: shell, filesystem, package installs, git, long sessions, snapshots.
- **MicroVM** — a minimal KVM virtual machine (Firecracker, Cloud Hypervisor) booting in ~100–300ms; the dominant sandbox primitive in 2026.
- **Snapshot / checkpoint** — a saved point-in-time state of a sandbox (memory + disk) that can be restored or forked later.
- **Fork / branch** — cloning a *running* sandbox into an independent copy, like `git branch` for VMs (Daytona, Runloop, Freestyle, Morph).
- **Hibernate / suspend-resume** — pausing a sandbox so it bills little or nothing while idle, then resuming with memory intact (Blaxel ~25ms resume, Runloop, CodeSandbox, OpenComputer).
- **Egress control** — policy over what network destinations a sandbox may reach (public internet, allowlists, metadata endpoints).
- **Credential brokering / injection** — giving a sandbox short-lived, scoped credentials without exposing the agent's real secrets (Vercel Sandbox, Superserve, Baponi).
- **Isolate** — a memory-safe language runtime sandbox (V8, WASM) with no OS access; millisecond starts, language-limited.
- **BYOC (Bring Your Own Cloud)** — running the vendor's sandbox control plane against compute in your own AWS/GCP/Azure account (Northflank, Tensorlake, E2B runtime, Leap0).
- **Computer use** — an agent driving a graphical desktop (mouse/keyboard/screen); some sandboxes ship desktop environments for it (E2B, Leap0, Box by ascii.dev).
- **CDP (Chrome DevTools Protocol)** — the protocol browser sandboxes expose for programmatic control (Puppeteer, Playwright, Stagehand).
- **Stealth / humanized browser** — fingerprint and behavior techniques so automated browsers aren't flagged as bots (Browserbase Stealth, Anchor's humanized Chromium).
- **MCP (Model Context Protocol)** — Anthropic's protocol for tool servers; several sandboxes expose MCP servers (Daytona, Baponi, Minimal, Kernel).
- **RL env** — sandboxes used as reinforcement-learning training environments (thousands of parallel envs: Tensorlake, Morph, Beam).
- **SWE-bench** — the standard benchmark for coding agents; Runloop and Morph publish sandbox-backed benchmark infra for it.
