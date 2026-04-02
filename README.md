# Personal Agent Workspace

> A blueprint for building your own AI personal assistant with Claude Code — one that knows your work, remembers context, reads your emails, tracks every person you interact with, and helps you stay on top of everything without being asked.

---

## For Orenda Team Members — Start Here

This workspace is built for you. Whether you're an engineer, manager, lead, or in people ops — you can have your own personal assistant running in under an hour.

### Step 1 — Install Claude Code

Claude Code is the tool that runs your agent. It works in your terminal.

```bash
npm install -g @anthropic-ai/claude-code
```

Then open your terminal and type `claude` to sign in with your Anthropic account.

> **No terminal experience?** On Mac, press `Cmd + Space` and search "Terminal". On Windows, search "PowerShell". Type the commands above and press Enter.

### Step 2 — Create your workspace

```bash
# Clone this repo to get the templates
git clone https://github.com/Orenda-Project/personal-agent-workspace
cd personal-agent-workspace

# Create your own workspace folder (anywhere on your computer)
mkdir ~/my-agent-workspace
cd ~/my-agent-workspace

# Set up the folder structure
mkdir -p memory agents domains/projects domains/team domains/communications domains/contacts/people logs skills/daily-standup plans
```

### Step 3 — Copy the starter templates from spec.md

Open [spec.md](spec.md) and go to **Part 7 — Starter Kit**. It has copy-paste templates for every file you need:

| Template | What to name it | Where to put it |
|----------|----------------|-----------------|
| `CLAUDE.md` template | `CLAUDE.md` | Root of your workspace |
| `MEMORY.md` template | `MEMORY.md` | Root of your workspace |
| `STANDUP.md` template | `STANDUP.md` | Root of your workspace |
| `memory/profile.md` template | `memory/profile.md` | Fill in your role + goals |
| `memory/context.md` template | `memory/context.md` | Fill in your current priorities |
| `skills/daily-standup/SKILL.md` template | `skills/daily-standup/SKILL.md` | The standup skill |

### Step 4 — Fill in your details

Open `memory/profile.md` and write a few lines about yourself:
- Your role and what you're responsible for
- Your current top priorities
- Key people you work with

The more you put in, the better your agent will know you. Even 10 bullet points is enough to start.

### Step 5 — Connect Gmail (optional but recommended)

Connecting Gmail means your agent reads your emails at the start of every session, tracks everyone who contacts you, and drafts replies for your approval.

See **Part 3 — Step 7** in [spec.md](spec.md) for setup instructions.

### Step 6 — Open your workspace

```bash
cd ~/my-agent-workspace
claude
```

Your agent will greet you, read your context, check for emails, and ask what you want to work on.

---

### Which parts of spec.md are most useful for your role?

| Your Role | Go to |
|-----------|-------|
| Manager | Part 4 — Example A |
| Tech / Product Lead | Part 4 — Example B |
| People Ops / HR | Part 4 — Example C |
| Engineer | Part 3 (full setup) + connect Jira MCP |
| Any role | Part 7 — Starter Kit (copy-paste templates) |

---

## How to Use This Repo

Read **[spec.md](spec.md)** — it's the full guide.

It covers everything from scratch:
- What an agent is and what it can do for you
- Step-by-step setup (no coding experience required)
- Role-specific examples: Manager, Lead, People Ops, Engineer
- Copy-paste templates for every file you need
- How to connect Gmail and track every contact automatically
- Best practices and what to avoid

---

## What You'll Build

A workspace on your computer that acts like a real assistant:

```
your-agent-workspace/
├── CLAUDE.md          ← Tells the agent how to behave at startup
├── STANDUP.md         ← Daily carry-overs (auto-updated each session)
├── MEMORY.md          ← Index of your memory files
├── memory/            ← Who you are, your priorities, your context
├── skills/            ← Custom behaviors (daily standup, email handling, etc.)
├── domains/           ← Tracking logs per area of work
│   └── contacts/
│       └── people/    ← One file per person who contacts you (auto-created)
├── plans/             ← Reminders and explicit instructions
└── logs/              ← Full session records, auto-saved daily
```

Every session, the agent:
1. Reads your memory and carry-overs
2. Pulls your Gmail and updates your contact files
3. Drafts replies for emails that need a response
4. Extracts your action items from anything you share
5. Greets you with a sharp briefing — no asking needed

---

## MCP Servers — Power Up Your Agent

MCPs are integrations that give your agent access to real tools. The more you connect, the more your agent can do on its own.

### High Value

| MCP | What It Unlocks |
|-----|----------------|
| **Google Workspace** | Read/send Gmail, Calendar, Drive, Docs, Sheets |
| **Atlassian** | Jira tickets, boards, issue tracking |
| **GitHub** | Repos, PRs, issues, code |
| **Slack** | Read messages, post updates |
| **Notion** | Read/write pages and databases |

### Situational

| MCP | What It Unlocks | Best For |
|-----|----------------|---------|
| **Linear** | Issues and project tracking | Eng teams on Linear |
| **Postgres / Supabase** | Query databases directly | Backend engineers |
| **Figma** | Read design files | Designers, frontend |
| **Airtable** | Read/write bases | Ops, project managers |
| **HubSpot / Salesforce** | CRM contacts | Sales, BD, CS |

### Experimental

| MCP | What It Unlocks |
|-----|----------------|
| **Browser automation** | Control a real browser, scrape, fill forms |
| **Excalidraw** | Generate diagrams from descriptions |
| **Langfuse** | Trace and observe AI calls |

---

## Contributing

If you build your own workspace and find patterns that work — better memory structures, useful skills, MCP combinations — open a PR.

**We're tracking:**
- [ ] Role-specific starter templates (Sales, Design, Data, DevOps)
- [ ] More skills (weekly review, meeting prep, PR summary, Jira sync)
- [ ] MCP setup walkthroughs with step-by-step instructions
- [ ] Multi-workspace setups (personal + work)

---

Built by the Orenda team. Contributions welcome.
