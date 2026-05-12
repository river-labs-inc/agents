# Auto Responder

An AI agent that reads your inbox and produces two kinds of output: replies that are ready to send (because the email matches an entry in your FAQ) and drafts for your review (because it doesn't).

You maintain one FAQ doc. The FAQ is the gate. What's in it gets a ready-to-send reply. What's not in it gets a draft.

---

## What it does

For each email in a batch:

1. **Reads it.** Filters out newsletters, automated mail, internal threads, and anything you've already replied to.
2. **Checks it against your FAQ.** If the question confidently maps to a Q&A pair you've added to `faq.md`, the reply is marked **READY TO SEND**, in your voice, with your sign-off.
3. **Otherwise, drafts it.** If the FAQ doesn't cover the question, the reply is marked **DRAFT (review before sending)**, with a "Worth flagging" note pointing out anything you should double-check.

You stay in control: nothing leaves your machine. The agent outputs text. You decide what to send and what to edit first.

---

## Requirements

- A [Claude.ai](https://claude.ai) account (Pro or Team recommended; Projects require Pro or higher)
- Optional: Claude's Gmail connector for native inbox reading (otherwise you paste emails into the chat)

---

## Quick start

### 1. Clone or download the repo

```bash
git clone https://github.com/river-labs-inc/agents.git
cd agents/auto-responder
```

Or download the repo as a zip from the [GitHub page](https://github.com/river-labs-inc/agents) (green **Code** button > **Download ZIP**) and unzip locally. You only need the files inside `auto-responder/`.

### 2. Create a Claude Project

In Claude.ai, create a new Project (sidebar > New Project). Give it a name like "Auto Responder".

### 3. Set the Custom Instructions

Open your Project settings > **Custom Instructions**. Paste the contents of [`system-prompt.md`](./system-prompt.md) in full.

### 4. Fill in your memory files

The three files in [`memory/`](./memory/) tell the agent who you are, how you want replies to sound, and which questions to handle automatically.

**Option A: guided setup (recommended).**
Open a new chat in the Project and paste the contents of [`prompts/setup.md`](./prompts/setup.md). The agent will ask you a few questions and output pre-filled versions of all three memory files for you to copy in.

**Option B: fill them manually.**
Edit each file directly:
- [`memory/agent-memory.md`](./memory/agent-memory.md): who you are and your company
- [`memory/tone-and-style.md`](./memory/tone-and-style.md): voice, do/don't rules, sign-off
- [`memory/faq.md`](./memory/faq.md): Q&A pairs that gate auto-replies

Once filled in, upload all three to your Project's **Knowledge** (Project settings > Add Content).

### 5. Run a scan

Open a new chat in the Project. Paste the contents of [`prompts/scan-and-respond.md`](./prompts/scan-and-respond.md), then either:
- Paste the emails you want processed directly into the chat
- Or say "use Gmail connector" if you have it connected

The agent will output a response for each email, marked either **READY TO SEND** (FAQ match) or **DRAFT** (review before sending).

---

## Growing the FAQ over time

Every time you find yourself editing a draft to give the same answer twice, that's a candidate for the FAQ. Open `memory/faq.md`, add a new Q&A pair, re-upload to Project Knowledge. The next scan will start handling that question as a ready-to-send reply.

If the answer depends on the customer's specific account, order, or something you'd need to look up, leave it out of the FAQ. Those should always be drafts.

---

## File reference

```
auto-responder/
  README.md                       this file
  system-prompt.md                paste into Claude Project Custom Instructions
  memory/
    agent-memory.md               who you are + your company context
    tone-and-style.md             voice, do/don't rules, sign-off line
    faq.md                        Q&A pairs that gate auto-replies
  prompts/
    setup.md                      run once to walk through initial configuration
    scan-and-respond.md           paste to trigger a scan pass
```

---

## Use River instead

This repo gives you the raw files for self-hosting in a Claude Project. If you'd prefer a version that:

- Runs automatically every 4 hours in the background
- Has Gmail wired up so auto-replies actually send and drafts land in Gmail Drafts
- Notifies you in-app whenever something is auto-sent or queued for review

[Get started with River](https://rivereditor.com/auto-responder). Free to start, 5-minute setup.
