# River Agents

Ready-to-use AI agents for Claude and other LLM platforms. Each agent folder contains everything you need: a system prompt, memory templates, a guided setup conversation, and a runnable task prompt.

## Agents

| Agent | What it does |
|---|---|
| [auto-responder](./auto-responder/) | Reads your inbox on a schedule, sends replies for questions covered by your knowledge base, and drafts the rest |

## How these work

Each agent is a set of markdown files you load into a **Claude Project** (or equivalent context system on other platforms). There are no special tools or integrations required beyond what Claude provides natively.

- `system-prompt.md`: paste into your Project's Custom Instructions
- `memory/`: fill in once, upload to Project Knowledge; the agent reads them on every run
- `prompts/setup.md`: run once in a new chat to walk through initial configuration
- `prompts/scan-and-respond.md` (or equivalent): paste to trigger the agent's main task

Want the fully automated version with Gmail integration and a 4-hour background cron? These agents are also available as one-click River spaces at [rivereditor.com](https://rivereditor.com).
