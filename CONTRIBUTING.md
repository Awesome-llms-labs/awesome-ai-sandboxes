# Contributing

Thanks for helping keep this list the most current directory of AI sandboxes!

## Adding a product

1. **Check it fits:** a sandbox (code execution, browser automation, or dev environment) that an AI agent can realistically use. General serverless platforms only qualify if they're positioned for agent code execution.
2. **Add to the right section** of `README.md` (alphabetical-ish order within section is fine, keep categories pure):
   - Managed code sandboxes → cloud services with an API/SDK
   - Open-source & self-hosted runtimes → table format (name, maintainer, isolation, license, notes)
   - Browser sandboxes → cloud browser automation for agents
   - Adjacent → dev environments genuinely positioned for agents
3. **One entry = one line** (managed/browser/adjacent) or one table row (OSS). Format:
   `- [Name](https://example.com) ` + optional tags (`agent-first`, `OSS`, `browser`) + ` — ` + one-line description + 1–2 key facts (isolation tech, pricing, funding, SDKs). (Shown as an unlinked code example above — use the real official site.)
4. **Add the matching record** to `data/sandboxes.json` (fields: `name`, `url`, `category` ∈ managed|oss|browser|adjacent, `description`, `isolation`, `oss` bool, `agent_first` bool, `status` ∈ active|acquired|shutdown|pivoted).
5. **Status changes:** if a product is acquired, shuts down, pivots, or changes license, update its README entry *and* add a row (newest-first) to `docs/status-changes.md`.

## Style rules

- Link the **official site** (homepage or docs), never a blog post or reseller.
- Facts that can change (pricing, funding, star counts) get "as of" context in prose or are omitted — link the source instead of hard-coding numbers that rot.
- Vendor claims stay labeled as vendor claims ("vendor claims", "per vendor").
- Keep descriptions to one line in the README; put depth in `docs/`.

## CI

Every PR runs:
- **Link check** (lychee) over all markdown files — no dead links.
- **JSON validation** — `data/sandboxes.json` must parse and every record must have the required fields with a valid `category`/`status`.

Run locally before pushing:

```bash
python3 -c "import json; [print('ok') for _ in [json.load(open('data/sandboxes.json'))]]"
```
