# Agent Workspace Blueprint
### A Beginner-Friendly Guide to Building Your Own AI Agent with Claude Code

> **Who this is for:** Anyone on the team — Manager, Lead, People Ops, or otherwise — who wants a personal AI assistant that knows their work, remembers context between sessions, and helps them stay on top of things. No coding experience required.

---

## Table of Contents

- [PART 1 — What Is an Agent?](#part-1--what-is-an-agent)
- [PART 2 — The System at a Glance](#part-2--the-system-at-a-glance)
- [PART 3 — Step-by-Step: Build Your Agent](#part-3--step-by-step-build-your-agent)
- [PART 4 — Role-Specific Examples](#part-4--role-specific-examples)
- [PART 5 — Customization Guide](#part-5--customization-guide)
- [PART 6 — Best Practices & What to Avoid](#part-6--best-practices--what-to-avoid)
- [PART 7 — Starter Kit (Copy-Paste Templates)](#part-7--starter-kit-copy-paste-templates)

---

## PART 1 — What Is an Agent?

### In Plain Language

An **agent** is an AI assistant you configure to know who you are, what you do, and how you like to work. Unlike a generic chatbot (which forgets everything after each conversation), an agent has **memory** — it reads files you've written about yourself and your work before each session begins.

Think of it like a very capable colleague who:
- Reads your notes before every meeting
- Remembers decisions you made last week
- Follows instructions you wrote down once
- Handles repetitive tasks automatically

### What an Agent Can Do

| Category | Examples |
|----------|----------|
| **Personal Assistant** | Draft messages, summarize notes, track tasks, prepare daily briefings |
| **Team Workflow** | Automate status updates, generate reports, route information |
| **Research** | Gather and summarize information from documents, write structured briefs |
| **Communication** | Draft emails, meeting recaps, announcements |

### What an Agent Cannot Do (Setting Expectations)

- It cannot browse the internet on its own (unless specifically connected to a tool)
- It cannot take actions outside your computer without explicit setup
- It does not learn automatically — you update its memory files when things change
- It is only as good as the instructions and context you give it

> **New to AI tools?** Think of your agent as a very smart assistant who only knows what's written in their briefing folder. If you want them to know something, you write it down. If things change, you update the notes.

---

## PART 2 — The System at a Glance

### How Everything Fits Together

Your agent workspace is a folder on your computer. Here's what a complete setup looks like:

```
my-agent-workspace/
│
├── CLAUDE.md          ← The "brain stem" — tells the agent how to behave at startup
├── STANDUP.md         ← Your daily status snapshot (auto-updated each session)
├── MEMORY.md          ← Index of all memory files (lives at root, not inside memory/)
│
├── memory/            ← Who you are and what matters to you
│   ├── profile.md     ← Your role, goals, working style
│   └── context.md     ← Current projects, priorities, key relationships
│
├── agents/            ← The agent definitions (one file per agent)
│   ├── daily-standup.md   ← The orchestrator — runs at the start of every session
│   ├── work-assistant.md  ← Handles your work/project questions
│   └── comms-helper.md    ← Drafts emails, messages, updates
│
├── domains/           ← Tracking files for each area of your work
│   ├── projects/
│   │   └── log.md
│   ├── team/
│   │   └── log.md
│   ├── communications/
│   │   └── log.md
│   └── contacts/          ← (optional) one file per person you interact with
│       ├── email-tracker.md
│       └── people/
│           └── name-surname.md
│
├── logs/              ← Auto-saved record of each session
│   └── 2026-03-31.md
│
└── skills/            ← Custom behaviors (optional, added as you grow)
    └── daily-standup/
        └── SKILL.md
```

### How the Pieces Connect

```
You open Claude Code
        ↓
CLAUDE.md runs automatically
        ↓
Daily Standup Agent reads:
  → MEMORY.md (index at root, lists all memory files)
  → memory/profile.md (who you are)
  → memory/context.md (your current priorities)
  → STANDUP.md (carry-overs from yesterday)
  → domains/*/log.md (what's been happening)
        ↓
Agent greets you with a personalized status snapshot
        ↓
You ask questions or give tasks
        ↓
Agent routes to the right specialist (work, comms, etc.)
        ↓
Logs the session → saves to logs/YYYY-MM-DD.md
```

**Key idea:** The agent reads files, does work, and writes logs. You update the memory files when your situation changes. That's the whole loop.

---

## PART 3 — Step-by-Step: Build Your Agent

---

### Step 1: Install Claude Code

Claude Code is the tool that runs your agent. It works inside a terminal (a text-based window on your computer).

**Installation:**
1. Go to [claude.ai/code](https://claude.ai/code) and follow the installation instructions for your operating system
2. Once installed, open your terminal and type `claude` — you should see a prompt appear
3. Sign in with your Anthropic account

> **Never used a terminal?** On Mac, search for "Terminal" in Spotlight (Cmd + Space). On Windows, search for "Command Prompt" or "PowerShell". You type commands and press Enter to run them.

---

### Step 2: Create Your Workspace Folder

In your terminal, run these commands one at a time:

```
mkdir my-agent-workspace
cd my-agent-workspace
mkdir memory agents domains logs skills
mkdir domains/projects domains/team domains/communications
```

This creates all the folders you need. You only do this once.

---

### Step 3: Write Your CLAUDE.md

This is the most important file. It tells the agent what to do every time you open a session.

Create a file called `CLAUDE.md` in your workspace folder. Copy the template from [Part 7](#part-7--starter-kit-copy-paste-templates) and fill in your details.

**The key things CLAUDE.md should contain:**
- What agent to run at startup (your daily standup)
- Where your key files live
- Any automatic behaviors (e.g., "always save a log at the end of the session")

> **Think of CLAUDE.md as the orientation packet you'd give a new assistant on their first day.** It should tell them your name, your role, what you're focused on, and how you like to work.

---

### Step 4: Set Up Your Memory Files

Memory files are plain text documents that tell the agent about you. You write them once and update them when things change.

**Create these two files to start:**

**`memory/profile.md`** — Who you are:
- Your role and responsibilities
- Your working style and preferences
- Your goals for the next 3–6 months
- Tools and systems you use daily

**`memory/context.md`** — What's happening right now:
- Your current top 3 priorities
- Active projects and their status
- Key people you work with and their roles
- Any blockers or things to watch

> **Keep memory files short and factual.** Bullet points are better than paragraphs. The agent reads these at the start of every session, so they should be easy to scan.

---

### Step 5: Create Your Daily Standup Agent

This is the "orchestrator" — the agent that runs first and routes your conversation to the right place.

Create `agents/daily-standup.md` using the template in Part 7.

**What this agent should do:**
1. Read your memory files and STANDUP.md
2. Check your domain logs for overdue items
3. Greet you with a brief status snapshot
4. Ask what you want to focus on today
5. Hand off to the right specialist agent based on your answer

---

### Step 6: Add Domain Agents

Domain agents are specialists. Each one handles a specific area of your work.

Start with 2–3 based on what you actually do most:

| Agent | What it handles |
|-------|----------------|
| `work-assistant.md` | Project updates, task tracking, decisions |
| `comms-helper.md` | Emails, messages, announcements, recaps |
| `research-agent.md` | Summarizing docs, briefing notes, gathering info |
| `team-tracker.md` | Team updates, 1:1 prep, hiring notes |

Each agent file contains:
- Its purpose
- Which files it reads for context
- How it should respond
- What it should log after each session

---

### Step 7 (Optional): Add Email Integration

Connecting Gmail lets your agent read emails at the start of every session and surface anything that needs your attention.

**What it unlocks:**
- Agent reads emails from the last 24 hours at every session start
- Flags emails that need a reply and drafts suggested responses for your approval
- Tracks every person who emails you in `domains/contacts/email-tracker.md`

**How to set it up:**

1. Install the Gmail MCP server for Claude Code (search "Claude Code Gmail MCP" for the current instructions — setup changes as the tool evolves)
2. Once connected, add these lines to your `CLAUDE.md` under `## Auto-start`:

```markdown
## Auto-start

At the beginning of every session:
1. Invoke the `daily-standup` skill.
2. Read Gmail — fetch emails from the last 24 hours.
3. Update `domains/contacts/email-tracker.md` with every person who emailed
   (name, email, subject, date, one-line summary).
4. Flag any emails that need a reply — present them with a suggested response.
   Ask for approval before sending anything.
```

3. Create the contacts tracking files:

```bash
mkdir -p domains/contacts/people
touch domains/contacts/email-tracker.md
```

4. Add a header to `domains/contacts/email-tracker.md`:

```markdown
# Email Tracker

| Name | Email | Subject | Date | Summary |
|------|-------|---------|------|---------|
```

**How contacts tracking works:**

Each person who emails you gets a file in `domains/contacts/people/firstname-lastname.md`. The agent creates these automatically and adds context over time — role, what you've discussed, open items. Useful when you need to remember who someone is before a meeting.

> **No Gmail?** This step is fully optional. The rest of the workspace works without it.

---

### Step 8: Set Up Logs & Standup Tracker

**`STANDUP.md`** is your carry-over file. At the end of each session, the agent updates it with:
- What was done
- What's pending
- What needs attention tomorrow

**`logs/`** folder gets a new file each day (`2026-03-31.md`) with a full record of the session. These are for your own reference — useful when you need to remember a decision you made two weeks ago.

Tell your agent in CLAUDE.md to always commit/save logs at the end of each session.

---

### Step 8: Your First Session — What to Expect

Open your terminal, navigate to your workspace folder, and type `claude`.

The agent will:
1. Read your CLAUDE.md and run the startup skill
2. Read your memory files
3. Check STANDUP.md for carry-overs
4. Greet you with a personalized summary

Then just talk to it naturally:
- *"What should I focus on today?"*
- *"Draft a message to the team about the Q2 planning session."*
- *"Summarize what happened with the onboarding project last week."*

The more context you've put in your memory files, the better the responses will be.

---

## PART 4 — Role-Specific Examples

---

### Example A: Manager Workspace

**What a Manager agent workspace looks like:**

```
my-agent-workspace/
├── memory/
│   ├── profile.md       ← Role: Engineering/Product/Ops Manager
│   └── context.md       ← Current team size, active initiatives, OKRs
├── agents/
│   ├── daily-standup.md ← Morning briefing + routes to specialist agents
│   ├── team-tracker.md  ← 1:1 prep, performance notes, team updates
│   └── comms-helper.md  ← Drafts status updates, announcements, escalations
└── domains/
    ├── team/log.md       ← Team activity, wins, concerns
    ├── projects/log.md   ← Project health, blockers, milestones
    └── stakeholders/log.md ← Key stakeholder interactions
```

**Sample prompts a Manager might use:**
- *"Prepare my 1:1 agenda for [team member name] based on what we discussed last week."*
- *"Write a status update email for the Q2 roadmap review."*
- *"What are the open action items from last week's team meeting?"*
- *"Draft a message to leadership about the timeline change on Project X."*

**What to put in `memory/profile.md`:**
```
Role: [Your Title] — [Team Name]
Responsible for: [List 3-5 key responsibilities]
Team size: [Number] direct reports
Key stakeholders: [Names/roles of people you report to or coordinate with]
Working style: [e.g., async-first, daily standups at 9am, prefer bullets over prose]
Current focus: [Top 1-2 things you're driving this quarter]
```

---

### Example B: Lead Workspace

**What a Lead agent workspace looks like:**

```
my-agent-workspace/
├── memory/
│   ├── profile.md       ← Role: Tech Lead / Product Lead / Design Lead
│   └── context.md       ← Current sprint, active decisions, team dependencies
├── agents/
│   ├── daily-standup.md ← Morning sync + routing
│   ├── work-assistant.md← Technical decisions, specs, PR/ticket tracking
│   └── research-agent.md← Summarizing proposals, benchmarking options
└── domains/
    ├── decisions/log.md  ← Key decisions made and why
    ├── projects/log.md   ← Work in progress, blockers
    └── team/log.md       ← Cross-team coordination, dependencies
```

**Sample prompts a Lead might use:**
- *"Summarize the trade-offs between Option A and Option B from the doc I just shared."*
- *"Draft a brief for the team explaining the decision to switch to [approach]."*
- *"What decisions did we make last month that I should brief the new joiner on?"*
- *"Help me write the acceptance criteria for this feature."*

**What to put in `memory/context.md`:**
```
Current sprint/cycle: [Sprint name or dates]
Active projects:
  - [Project name]: [Status, owner, key risk]
  - [Project name]: [Status, owner, key risk]
Key dependencies: [Teams or people you're waiting on]
Open decisions: [Things still being debated]
Recent decisions: [What was decided and when]
```

---

### Example C: People Ops Workspace

**What a People Ops agent workspace looks like:**

```
my-agent-workspace/
├── memory/
│   ├── profile.md       ← Role: People Ops / HR / Talent
│   └── context.md       ← Active hiring, onboarding, initiatives
├── agents/
│   ├── daily-standup.md ← Morning briefing + routing
│   ├── comms-helper.md  ← Drafts offer letters, announcements, policy updates
│   └── research-agent.md← Summarizes feedback surveys, benchmarks, frameworks
└── domains/
    ├── hiring/log.md     ← Open roles, pipeline status, decisions
    ├── onboarding/log.md ← New joiners, checklist progress
    └── initiatives/log.md← Culture, engagement, policy projects
```

**Sample prompts a People Ops person might use:**
- *"Draft an offer letter for a [role] joining on [date]."*
- *"Summarize the key themes from last month's engagement survey."*
- *"What's the onboarding status for the two people who joined this month?"*
- *"Write an announcement for the new [policy/benefit/program] we're rolling out."*
- *"Prepare talking points for the all-hands on our Q2 hiring plan."*

**What to put in `memory/profile.md`:**
```
Role: [Your Title] — People Ops / HR / Talent
Responsible for: [e.g., hiring, onboarding, culture, L&D, policy]
Team size supported: [Number of employees in the org]
Key stakeholders: [Hiring managers, leadership, finance]
Tools used: [e.g., ATS name, HRIS name, Slack, Notion]
Current focus: [Top 1-2 initiatives this quarter]
```

---

## PART 5 — Customization Guide

### How to Adapt Each File

**CLAUDE.md** — Change the startup skill name and the list of key files to match your workspace. The structure stays the same; the content is yours.

**memory/profile.md** — Update this whenever your role changes, you take on new responsibilities, or your priorities shift. It's a living document.

**memory/context.md** — Update this weekly (or whenever something significant changes). Think of it as your "current state of play" document.

**agents/*.md** — Each agent file has a simple structure: purpose, context files to read, how to respond, what to log. Change the purpose and context files to match your domain.

**domains/*/log.md** — These are append-only logs. The agent adds to them; you rarely edit them directly. You can add a "domain" for any area of your work: hiring, projects, clients, partnerships, etc.

### Adding a New Domain

1. Create a folder: `domains/new-area/`
2. Create a log file: `domains/new-area/log.md` with a header and today's date
3. Tell your orchestrator agent about it in `agents/daily-standup.md`
4. (Optional) Create a specialist agent: `agents/new-area-agent.md`

### Adding Contacts Tracking

If you interact with many people (collaborators, stakeholders, clients), a contacts domain gives you a searchable record of who everyone is.

**Setup:**
```bash
mkdir -p domains/contacts/people
touch domains/contacts/email-tracker.md
```

**How it works:**
- `domains/contacts/email-tracker.md` — running table of every person who's contacted you (name, email, subject, date, summary)
- `domains/contacts/people/firstname-lastname.md` — one file per person; the agent fills these in automatically over time

**What to put in a person file:**
```markdown
# [Full Name]

- **Email:** name@example.com
- **Role:** [Their title / how they relate to your work]
- **Organisation:** [Company or team]
- **Context:** [How you know them, what you've worked on together]
- **Open items:** [Anything pending with this person]
```

Tell your standup agent to check `domains/contacts/email-tracker.md` during startup so it can flag anyone you haven't followed up with.

---

### Common Use Case Prompts (Copy-Paste Ready)

**For drafting communications:**
> "Draft a [message type] to [audience] about [topic]. Tone should be [formal/casual/direct]. Keep it under [length]."

**For summarizing:**
> "Summarize the key points from [document/discussion/log]. Give me bullets, not prose. Flag anything that needs a decision."

**For tracking:**
> "Update the [domain] log with what we just discussed. Include date, what happened, and any next steps."

**For preparing:**
> "I have a [meeting type] with [person/group] in [timeframe]. What context should I review and what should I prepare?"

**For drafting decisions:**
> "I need to decide between [Option A] and [Option B]. Here's what I know: [context]. Help me think through the trade-offs."

---

## PART 6 — Best Practices & What to Avoid

### How to Write Clear Instructions for Your Agent

**Be specific about role and audience.** Instead of "help me write an email," say "draft a 3-paragraph email to my direct reports announcing the new leave policy, friendly but clear in tone."

**Tell the agent what you want it to read.** If your agent has multiple context files, tell it which ones matter for this task: "Based on what's in my hiring log, tell me..."

**Give examples of what good looks like.** If you have a sample email you like, paste it in and say "write something in this style."

**Use consistent language.** If you call something "the Q2 initiative" in your memory files, use the same name when talking to the agent.

### Common Mistakes to Avoid

| Mistake | What to do instead |
|---------|-------------------|
| Leaving memory files empty | Fill them out before your first session — even a rough draft is better than nothing |
| Writing memory files like essays | Use bullets and short sentences — the agent scans, not reads |
| Never updating memory files | Set a recurring reminder to review and update `context.md` weekly |
| Creating too many agents at once | Start with just the orchestrator + 1 specialist. Add more as you discover what you need |
| Asking the agent to remember things without writing them down | The agent only knows what's in files. If you want it to remember, update a file |
| Putting sensitive data in files | Do not store passwords, personal data about others, or confidential company information in these files |

### Keeping Your Agent Focused and Useful

- **One domain per agent.** Don't create a "do everything" agent — it becomes unfocused.
- **Review your STANDUP.md weekly.** If carry-overs pile up, your context files need updating.
- **Delete or archive domains you no longer use.** A cluttered workspace gives the agent noise.
- **When the agent gives a wrong or unhelpful answer, update your files.** Usually the issue is missing context, not the agent itself.

---

## PART 7 — Starter Kit (Copy-Paste Templates)

### Complete Folder Structure

Run these commands in your terminal to set up the workspace in one go:

```bash
mkdir my-agent-workspace
cd my-agent-workspace
mkdir -p memory agents domains/projects domains/team domains/communications domains/contacts/people logs skills/daily-standup
touch CLAUDE.md STANDUP.md MEMORY.md memory/profile.md memory/context.md
touch agents/daily-standup.md agents/work-assistant.md agents/comms-helper.md
touch domains/projects/log.md domains/team/log.md domains/communications/log.md domains/contacts/email-tracker.md
touch skills/daily-standup/SKILL.md
```

---

### Template: CLAUDE.md

```markdown
# [Your Name]'s Agent Workspace

This is [Your Name]'s personal agent workspace. When a session starts here,
automatically run the daily-standup skill — read all context files and greet
[Your Name] with a daily status snapshot.

## Auto-start

At the beginning of every session, invoke the `daily-standup` skill.
Do not wait for the user to ask.

## Skills

Custom skills live in `skills/`. Use them:
- `/daily-standup` — daily briefing, status snapshot, session routing

## Key files

- `MEMORY.md` — start here, indexes all memory files
- `STANDUP.md` — carry-overs and today's focus
- `logs/` — daily session logs (create YYYY-MM-DD.md each session)
- `agents/` — agent definitions
- `domains/` — tracking files per area of work

## End of every session

Always save a log before closing:
Write a summary of the session to `logs/[TODAY'S DATE].md`.
Update `STANDUP.md` with carry-overs and tomorrow's focus.
```

---

### Template: memory/profile.md

```markdown
# My Profile

## Role
[Your job title] — [Team or department name]

## Responsibilities
- [Responsibility 1]
- [Responsibility 2]
- [Responsibility 3]

## Working Style
- [e.g., Prefer async communication]
- [e.g., Daily check-ins at 9am]
- [e.g., Think in bullet points, not paragraphs]

## Goals This Quarter
- [Goal 1]
- [Goal 2]

## Tools I Use Daily
- [Tool 1 — what it's for]
- [Tool 2 — what it's for]

## Key People I Work With
- [Name/Role] — [context, e.g., my manager, key collaborator on X]
- [Name/Role] — [context]
```

---

### Template: memory/context.md

```markdown
# Current Context

## Top Priorities Right Now
1. [Priority 1]
2. [Priority 2]
3. [Priority 3]

## Active Projects
- [Project Name]: [Status] — [Key risk or next step]
- [Project Name]: [Status] — [Key risk or next step]

## Waiting On
- [Person/team] for [what] by [when]

## Recent Decisions
- [Date]: [Decision made and why]

## Open Questions / Blockers
- [Thing that's unclear or blocked]

## Last Updated
[Date]
```

---

### Template: MEMORY.md (root of workspace)

> This file lives at the **root of your workspace**, not inside `memory/`. It's an index — one line per memory file.

```markdown
# Memory Index

- [My Profile](memory/profile.md) — [Your role and goals, one line]
- [Current Context](memory/context.md) — [Active projects and priorities, one line]
```

---

### Template: agents/daily-standup.md

```markdown
# Daily Standup Agent

## Purpose
You are [Your Name]'s daily orchestrator. At the start of every session,
you read all context files and produce a personalized status snapshot.
Then you route the conversation to the right specialist agent.

## Context Files to Read
- memory/profile.md
- memory/context.md
- STANDUP.md
- domains/projects/log.md
- domains/team/log.md
- domains/communications/log.md

## What to Produce at Startup
1. A brief greeting using [Your Name]'s name
2. Top 3 priorities for today (from context.md + STANDUP.md carry-overs)
3. Any overdue items flagged from domain logs
4. A prompt: "What do you want to focus on today?"

## Routing Rules
- Work / projects → work-assistant agent
- Emails / messages / announcements → comms-helper agent
- Research / summarizing → research-agent (if set up)
- Team / people questions → team-tracker agent (if set up)

## End of Session
- Append a summary to logs/[TODAY'S DATE].md
- Update STANDUP.md with: what was done, what's pending, what needs attention tomorrow
```

---

### Template: agents/work-assistant.md

```markdown
# Work Assistant Agent

## Purpose
Handle questions about projects, tasks, decisions, and work in progress.

## Context Files to Read
- memory/context.md
- domains/projects/log.md

## How to Respond
- Be direct and concise
- Use bullet points for lists
- Flag risks or blockers explicitly
- If something needs a decision, present options clearly

## After Each Session
Append a log entry to domains/projects/log.md with:
- Date
- What was discussed or decided
- Next steps
```

---

### Template: agents/comms-helper.md

```markdown
# Communications Helper Agent

## Purpose
Draft emails, messages, announcements, meeting recaps, and any written communication.

## Context Files to Read
- memory/profile.md
- domains/communications/log.md

## How to Respond
- Ask about audience, tone, and length before drafting if not specified
- Default to clear, professional, and concise
- Offer to revise after the first draft

## After Each Session
Append a log entry to domains/communications/log.md with:
- Date
- What was drafted and for whom
```

---

### Template: STANDUP.md

```markdown
# Daily Standup

## Carry-overs from Last Session
- [ ] [Item 1]
- [ ] [Item 2]

## Today's Focus
[Date] — [What you're working on today]

## Reminders
- [Any time-sensitive item]

## Quick Status
| Domain | Last Activity | Status |
|--------|--------------|--------|
| Projects | [Date] | [On track / Needs attention] |
| Team | [Date] | [On track / Needs attention] |
| Communications | [Date] | [On track / Needs attention] |
```

---

### Template: domains/[area]/log.md

```markdown
# [Area] Log

## [YYYY-MM-DD]
- [What happened]
- [Decision made]
- [Next steps]

---

## [YYYY-MM-DD]
- [What happened]
```

---

### Template: skills/daily-standup/SKILL.md

```markdown
# Daily Standup Skill

Run this skill at the start of every session.

## Steps
1. Read memory/MEMORY.md to find all memory files
2. Read each memory file listed in the index
3. Read STANDUP.md for carry-overs
4. Read the last entry in each domain log file
5. Produce a status snapshot:
   - Greet [Your Name] by name
   - List today's top priorities
   - Flag any overdue items
   - Ask what to focus on
6. Wait for input and route to the appropriate specialist agent
```

---

## Quick Reference Card

| File | What it's for | Update when |
|------|--------------|-------------|
| `CLAUDE.md` | Agent startup instructions | Rarely — only if your workflow changes |
| `MEMORY.md` | Index of all memory files (at root) | When you add or remove memory files |
| `memory/profile.md` | Who you are | Role or priorities change |
| `memory/context.md` | What's happening now | Weekly or when things shift |
| `STANDUP.md` | Daily carry-overs | Auto-updated by agent each session |
| `agents/*.md` | How each agent behaves | When you want to change agent behavior |
| `domains/*/log.md` | Activity history per area | Auto-updated by agent each session |
| `domains/contacts/email-tracker.md` | Everyone who's emailed you | Auto-updated if Gmail integration is on |
| `domains/contacts/people/*.md` | Per-person context files | Auto-created by agent, edit to add detail |
| `logs/*.md` | Full session records | Auto-created by agent each session |

---

*This spec was designed to be adapted — not followed exactly. Take what fits your role, skip what doesn't, and add what's missing. The best agent workspace is the one that matches how you actually work.*
