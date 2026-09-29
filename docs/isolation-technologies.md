# Isolation Technologies

How sandboxes keep untrusted AI-generated code from escaping. Ordered roughly from strongest to weakest isolation.

## MicroVMs (Firecracker / Cloud Hypervisor)

Tiny KVM-based virtual machines (~150ms boot, minimal guest kernel) — hardware-enforced isolation with near-container density. The dominant technology for agent sandboxes in 2026.

- **Used by:** E2B, Vercel Sandbox, Sprites, Superserve, Leap0, InstaVM, Declaw, Tensorlake, Qbox, Northflank (option), most startups.
- **Strengths:** hardware boundary; fast boot; mature tooling.
- **Weaknesses:** full guest OS per sandbox = more memory than isolates; kernel exploits are rare but catastrophic.
- **Read:** [Firecracker](https://github.com/firecracker-microvm/firecracker) (Apache-2.0), [Cloud Hypervisor](https://github.com/cloud-hypervisor/cloud-hypervisor) (Apache-2.0).

## Kata Containers

Lightweight VMs with an OCI/container interface — "VMs that feel like containers."

- **Used by:** Northflank (selectable), Daytona (VM classes).
- **Strengths:** Docker-compatible workflows with a VM boundary; multiple hypervisor backends (QEMU, Cloud Hypervisor, Firecracker).
- **Read:** [Kata Containers](https://github.com/kata-containers) (Apache-2.0).

## Full VMs (KVM)

Traditional virtual machines, sometimes with live migration and memory-preserving hibernate.

- **Used by:** Runloop (custom hypervisor), Freestyle, Morph, OpenComputer, Box by ascii.dev.
- **Strengths:** strongest isolation story; nested virtualization; long-lived state.
- **Weaknesses:** slowest starts (sub-second to seconds); heaviest per-sandbox footprint.

## gVisor (runsc)

A user-space application kernel that intercepts syscalls — containers with a much smaller attack surface than sharing the host kernel.

- **Used by:** Modal, Beam, Northflank (option).
- **Strengths:** container density + strong syscall filtering; no guest OS.
- **Weaknesses:** syscall-compatibility gaps for exotic workloads; performance overhead on syscall-heavy code.
- **Read:** [gVisor](https://github.com/google/gvisor) (Apache-2.0).

## nsjail / bubblewrap (namespaces + seccomp)

Linux namespaces, cgroups, and seccomp-bpf filters around a plain process — the lightest "real" sandbox.

- **Used by:** Baponi (nsjail); bubblewrap is common in OSS agent harnesses; IOI's `isolate` is the competitive-programming standard.
- **Strengths:** near-zero overhead; fine-grained per-syscall policy.
- **Weaknesses:** shares the host kernel — a kernel exploit escapes; policy authoring is expert work.
- **Read:** [nsjail](https://github.com/google/nsjail) (Apache-2.0), [bubblewrap](https://github.com/containers/bubblewrap) (LGPL-2.1), [isolate](https://github.com/ioi/isolate) (GPL-2.0).

## V8 / WASM isolates

Language-level sandboxes: JS/TS (or WASM-compiled languages) running in a memory-safe isolate with no OS access.

- **Used by:** Riza (WASM), Val Town (V8), Deno Sandbox (V8).
- **Strengths:** millisecond starts; enormous density (thousands per host); no cold starts.
- **Weaknesses:** limited to supported languages; no shell/filesystem semantics; side-channel concerns at extreme multi-tenancy.
- **Read:** [V8](https://v8.dev), [WASI](https://wasi.dev).

## In-process interpreters

Bash/Python reimplemented inside the agent's own process with a virtual filesystem and no syscalls (e.g. `bashkit4j`).

- **Strengths:** zero infrastructure; deterministic.
- **Weaknesses:** only as safe as the interpreter's completeness; no real OS semantics.

## Browser sandboxes

Dockerized Chromium (Steel) or custom Chromium forks (Anchor) driven over CDP — isolation is about the *web* (fingerprints, CAPTCHAs, proxies), not the OS.

## What actually matters for agents

1. **Escape resistance** — microVM ≥ full VM > gVisor/Kata > nsjail > isolates for hostile code.
2. **Egress control** — can the sandbox reach your secrets, metadata endpoints, or the open internet? Per-sandbox network policy (Baponi, Islo) and credential brokering (Vercel Sandbox, Superserve) matter more than the hypervisor for most agent threat models.
3. **Snapshot/fork** — for agentic loops, the ability to checkpoint and branch state (Daytona, Runloop, Tensorlake) is a bigger productivity lever than shaving 100ms off boot.
4. **Auditability** — command deny lists, audit logs, LLM-as-judge filters (Ona, Declaw, Islo) for regulated environments.
