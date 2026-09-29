# Choosing a Sandbox

A decision framework for picking an AI sandbox. Answer these questions in order; each one eliminates half the list.

## 1. What does your agent need to *do*?

| Workload | Start with |
|---|---|
| Run untrusted AI-generated code snippets (Python/JS) | [Riza](https://riza.io), [E2B](https://e2b.dev), [Vercel Sandbox](https://vercel.com/docs/vercel-sandbox) |
| Full coding-agent loop: shell, filesystem, git, long sessions | [Daytona](https://daytona.io), [Runloop](https://runloop.ai), [E2B](https://e2b.dev), [Modal](https://modal.com), [Freestyle](https://freestyle.sh) |
| GPU work: training, RL, inference | [Modal](https://modal.com), [Beam](https://beam.cloud), [Northflank](https://northflank.com) |
| Browse the real web (click/scroll/forms) | [Browserbase](https://www.browserbase.com), [Steel](https://steel.dev), [Anchor Browser](https://anchorbrowser.io) |
| Quick script-as-agent execution (TS/JS) | [Val Town](https://val.town), [Deno Sandbox](https://deno.com) |
| Desktop / computer-use | [E2B desktop sandboxes](https://e2b.dev), [Leap0](https://leap0.dev), [Box by ascii.dev](https://box.ascii.dev) |

## 2. How strong must the isolation be?

- **Running code you don't trust at all** (arbitrary user code, jailbreak attempts): prefer hardware isolation — **Firecracker microVMs** (E2B, Vercel Sandbox, Sprites, Superserve) or **gVisor** (Modal, Beam). See [isolation technologies](isolation-technologies.md).
- **Running your own agent's code with secrets**: network egress controls and credential brokering matter more than the hypervisor — look at Vercel Sandbox's firewall, Baponi's per-sandbox network policies, Islo's gateway profiles.
- **Enterprise/compliance** (SOC 2, HIPAA): E2B, Modal, Tensorlake, Anchor Browser, Airtop advertise these; verify current attestations on their sites.

## 3. Session shape

- **Short bursts** (<1 min): per-execution billing wins — Baponi, Riza, Val Town (V8 isolates).
- **Long coding sessions** (hours): you want snapshot/resume so you don't pay for idle time — Blaxel (25ms resume), Runloop (suspend/resume), CodeSandbox (hibernate), OpenComputer (hibernate/wake).
- **Stateful loops** (RL, evals): snapshot/clone/fork running sandboxes — Daytona, Runloop, Tensorlake, Morph, Freestyle (live fork).

## 4. Latency budget

Sub-second cold starts are table stakes now; the spread is roughly: V8/WASM isolates (Riza <10ms, Val Town <100ms) < Firecracker microVMs (~100–300ms: E2B, Leap0, Superserve) < containers (~0.4–2.5s resume: Upstash Box) < full VMs (~600ms–2s: Freestyle, Runloop for 10GB images). Measure your own workload — vendor numbers are best-case.

## 5. Where does it run?

- **Their cloud** (fastest to start): everything in [Managed Code Sandboxes](../README.md#managed-code-sandboxes).
- **Your cloud (BYOC)** or on-prem: Northflank, Tensorlake, Baponi (enterprise), E2B runtime, Qbox, Leap0. BYOC keeps data in your VPC and usually cuts unit cost.
- **Fully self-hosted OSS**: [Open-Source & Self-Hosted Runtimes](../README.md#open-source--self-hosted-runtimes) — Firecracker + E2B's open runtime is the most agent-ready combo.

## 6. Price model

- **Per-second active compute** is the norm (E2B, Daytona, Modal, Vercel Sandbox…).
- **Per-execution** suits bursty workloads (Baponi, Riza).
- **$0-at-idle / standby** changes the math for persistent agents (Blaxel, Upstash Box active-CPU-only).
- Watch the fine print: session length caps (e.g. Hobby tiers), concurrency limits, and egress/data-transfer fees. All prices in this repo are list prices as of Sep 2026.

## 7. Ecosystem lock-in

- OpenAI's **Sandbox Agents** (Apr 2026) natively targets Blaxel, Cloudflare, Daytona, E2B, Modal, Runloop, Vercel — if you're building on OpenAI's agent stack, one of those seven is the path of least resistance.
- **E2B-compatible SDKs** (Novita, Runtime/withruntime) let you switch providers without rewriting agent code — prefer compatible APIs when you're not sure you'll stay.

## Quick picks

- **Default for coding agents:** E2B or Daytona.
- **GPU-heavy agents:** Modal or Beam.
- **Cheapest bursty execution:** Riza or Val Town.
- **Self-hosted:** Firecracker + E2B runtime, or Qbox.
- **Web-browsing agents:** Browserbase, or Steel if you want OSS.
- **Enterprise governance:** Coder (workspaces) or Islo / Baponi (sandboxes).
