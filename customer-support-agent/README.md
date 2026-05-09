# Customer Support Agent

An AI agent that reads your support inbox, filters out noise, and drafts replies in your voice — one for each genuine customer support request it finds.

You review every draft before anything goes out. The agent never sends on its own.

---

## What it does

1. **Reads your inbox** — you paste in emails (or use Claude's Gmail connector), and the agent filters for genuine support requests: questions, bug reports, how-to requests, billing issues.
2. **Researches the answer** — searches your website, your GitHub repo, or draws from your FAQ list depending on what you configured.
3. **Drafts a reply** — writes in your configured voice and tone, closes with your sign-off line.
4. **Flags anything uncertain** — every output includes a "Worth flagging" section so you know what to double-check before sending.

---

## Requirements

- A [Claude.ai](https://claude.ai) account (Pro or Team recommended — Projects require Pro or higher)
- Optional: Claude's Gmail connector for native inbox reading (otherwise you paste emails manually)

---

## Quick start

### 1. Clone or download this folder

```bash
git clone https://github.com/river-labs-inc/agents.git
cd agents/customer-support-agent
```

Or download the folder directly from GitHub.

### 2. Create a Claude Project

In Claude.ai, create a new Project (sidebar → New Project). Give it a name like "Customer Support Agent".

### 3. Set the Custom Instructions

Open your Project settings → **Custom Instructions**. Paste the contents of [`system-prompt.md`](./system-prompt.md) in full.

### 4. Fill in your memory files

The three files in [`memory/`](./memory/) tell the agent who you are, how you want replies to sound, and what knowledge to draw from. You can fill them in two ways:

**Option A — guided setup (recommended):**
Open a new chat in the Project and paste the contents of [`prompts/setup.md`](./prompts/setup.md). The agent will ask you questions and output pre-filled versions of each memory file for you to copy in.

**Option B — fill them manually:**
Edit each file directly:
- [`memory/agent-memory.md`](./memory/agent-memory.md) — who you are and your company
- [`memory/tone-and-style.md`](./memory/tone-and-style.md) — voice, do/don't rules, sign-off
- [`memory/data-sources-faq.md`](./memory/data-sources-faq.md) — website/GitHub repo to search, or your FAQ Q&A pairs

Once filled in, upload all three to your Project's **Knowledge** (Project settings → Add Content).

### 5. Draft replies

Open a new chat in the Project. Paste the contents of [`prompts/scan-and-draft.md`](./prompts/scan-and-draft.md), then either:
- Paste the emails you want processed directly into the chat
- Or say "use Gmail connector" if you have it connected

The agent will output a reply draft and a summary for each support email it finds.

---

## Keeping context up to date

Edit the files in `memory/` any time your company, tone preference, or FAQ answers change. Re-upload the updated files to Project Knowledge — Claude will use the new version on the next run.

---

## File reference

```
customer-support-agent/
  README.md                   this file
  system-prompt.md            paste into Claude Project Custom Instructions
  memory/
    agent-memory.md           who you are + your company context
    tone-and-style.md         voice, do/don't rules, sign-off line
    data-sources-faq.md       website/GitHub to search, or FAQ Q&A pairs
  prompts/
    setup.md                  run once to walk through initial configuration
    scan-and-draft.md         paste to trigger a draft pass
```

---

## Use River instead

This repo gives you the raw files. If you'd prefer a version that:
- Runs automatically every 4 hours in the background
- Has Gmail wired up without manual copy-paste
- Notifies you in-app when a draft is ready

→ [Get started with River](https://river.so/customer-support-agent) — free to start, 5-minute setup.
