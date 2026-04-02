# Personal Agent Workspace

> A blueprint for building your own AI personal assistant with Claude Code — one that knows your work, remembers context, reads your emails, tracks every person you interact with, and helps you stay on top of everything without being asked.

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
