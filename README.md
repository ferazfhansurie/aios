# AIOS — AI Operating System for your business

> An open-source pattern for running your business through Claude Code. No dashboard. No web app. Just a folder of context, a few skill files, and Claude.

```bash
git clone https://github.com/ferazfhansurie/aios my-business-aios
cd my-business-aios
claude        # opens Claude Code
> /onboard    # 5-minute interview, then your AI co-founder is live
```

That's the whole setup. After `/onboard`, every time you `cd` into the folder and open Claude, it knows your business — your team, your customers, your tools, how you talk — and can take action on your behalf.

---

## Why this exists

I run [Adletic](https://adletic.com), an AI agency in Malaysia. I kept rebuilding the same thing for every client:

- A dashboard nobody opens after the first week
- A chatbot that lives on someone else's UI
- A set of skills locked inside one tool

What actually works — for me, for my clients — is this:

> **The AI lives where you already work.** It reads your context on every session. You talk to it like a partner, not a chatbot. It uses your existing databases, your existing tools, your existing files. It doesn't try to replace anything. It just makes you 5x faster at the things you already do.

After deploying this pattern for an influencer agency, a carpet retailer, a renewable-energy company, and my own agency, I extracted the bones. **This repo is the bones.**

Clone it, run `/onboard`, and you'll have the same kind of AI co-founder in 10 minutes.

---

## What you get

A workspace with a clear pattern:

```
.
├── CLAUDE.md                      # The system prompt. Loaded automatically.
├── .claude/
│   ├── commands/                  # Slash commands you can run
│   │   ├── onboard.md             # First-time setup interview
│   │   ├── prime.md               # Fast context-load on every session
│   │   └── create-skill.md        # Walk-through to add a new skill
│   ├── skills/                    # Your business's repeatable workflows
│   └── context/                   # What AIOS knows about your business
│       ├── personal-info.md
│       ├── business-info.md
│       ├── current-data.md
│       └── communication-style.md
├── examples/skills/               # Reference skills — copy into .claude/skills/
│   ├── morning-pulse.md
│   ├── weekly-report.md
│   ├── lead-leak-audit.md
│   └── proposal-draft.md
├── outputs/                       # Generated reports, drafts, dashboards
└── files/                         # Files you upload for AIOS to read
```

## The 5-layer pattern

Every AIOS workspace is structured as five layers:

| Layer | Lives in | What it does |
|---|---|---|
| **1. Context** | `.claude/context/` | Who the business is, who's on the team, how they talk, what's on right now |
| **2. Data** | Wherever your data already lives (Postgres, Firebase, Sheets, an API) | The AI queries it directly. No copying, no syncing, no separate database |
| **3. Intelligence** | `.claude/skills/` | Repeatable analyses: "morning pulse", "weekly report", "leak audit" |
| **4. Automate** | Action calls inside skills | Send WhatsApp, post Slack, update a CRM, fire an API |
| **5. Build** | `outputs/` | Generated artifacts — proposals, ad copy, reports, dashboards |

The first time you run `/onboard`, AIOS interviews you about all five layers and writes the answers into your context files. After that, every Claude session starts with full awareness of your business.

---

## Install

**Prerequisites:**
- [Claude Code](https://claude.ai/code) installed and signed in
- Git

**Setup:**
```bash
git clone https://github.com/ferazfhansurie/aios my-business
cd my-business
claude
```

Inside Claude:
```
> /onboard
```

It'll interview you for ~5 minutes. Tell it your business name, what you sell, who your customers are, what tools you use, drop in any files you want it to know about. Done.

From then on, every time you open the folder:
```bash
cd my-business
claude
> /prime
```

You'll get a one-screen snapshot of your business — last metrics, what's pending, what's on. Then you start talking.

---

## What it looks like in practice

After onboarding, conversations sound like:

> **You:** morning
>
> **AIOS:** Morning, Firaz.
>
> Overnight (Apr 30): 14 new customer messages, 3 unread (biggest: Sarah at Hello Billionaires — RM36K invoice), 2 deals moved to negotiation.
>
> Today's priorities:
> 1. Reply to Sarah — invoice 7 days overdue
> 2. Send proposal to Wad Works (we said by Wednesday)
> 3. CnB demo at 3pm
>
> What's the play?

> **You:** draft proposal for wad works, focus on lead gen
>
> **AIOS:** _[reads `business-info.md` for AIOS pricing, drafts proposal, saves to `outputs/2026-04-30-proposal-wad-works.md`]_
>
> Drafted. RM12K setup + RM3K/mo for 12 months, lead gen focus. Want me to draft the WhatsApp message to send it with?

> **You:** any leaks this week?
>
> **AIOS:** _[runs lead-leak-audit skill]_
>
> 6 leads went cold in the last 7 days. 2 are hot:
>
> 🔥 Ahmad (Bizplus) — last said "interested, when can we talk?" 47h ago
> 🔥 Tika (Aie Network) — asked about pricing 36h ago
>
> Want me to draft re-engagement messages?

That's it. No dashboard. No clicking through tabs. Just the conversation.

---

## Real builds using this pattern

These are real businesses I've built AIOS workspaces for. Each one started from this same template:

- **An influencer agency** (3000+ KOLs) — daily campaign briefings, KOL discovery from natural language ("find me 10 beauty micro-influencers in KL"), invoice generation from chat
- **A carpet retailer** (Malaysia) — customer conversation routing, automated KOL payment tracking, daily team pulse via WhatsApp
- **A renewable-energy company** (B2B solar) — lead leak audits, deal pipeline summaries, automated proposals
- **My own agency** — sales pipeline, prospect research, proposal generation, daily ops

Different industries, different data, same five layers. The skills are different per business; the structure is the same.

---

## FAQ

### How is this different from custom GPTs / Assistants?

Custom GPTs live inside ChatGPT's UI. This lives inside your file system, talks to your real databases, runs on your machine, and can take real actions (send messages, write files, deploy code). It's a workspace, not a chatbot.

### Why Claude Code specifically?

Three reasons: (1) it has full filesystem + bash access, so it can actually do work, (2) it's the only assistant that's serious about the slash-command + skill pattern, (3) the per-project `CLAUDE.md` instruction file makes context-as-code possible. You could in theory port this to Cursor / Cline / etc., but Claude Code is where it works best today.

### What about my data privacy?

AIOS runs on your machine. Your context files stay on your machine. The only thing that goes to Anthropic is whatever Claude needs to read to answer your questions (which you control via `.claude/settings.local.json` permissions). You can run AIOS on an air-gapped machine if you want.

### Do I have to use Postgres?

No. AIOS works with whatever data sources you already have. During `/onboard`, tell it what you use — Postgres, Firebase, Sheets, Notion, just files, even nothing — and it adapts. The example skills assume Postgres because that's the most common, but they're easy to rewrite for other backends.

### Can I run this for clients?

Yes. That's literally how I make money. Clone for each client, customize the skills for their business, hand it over. If you want a managed version (we host the database, the WhatsApp transport, the Claude tokens), [hire Adletic](mailto:firaz@adletic.com) — that's the paid offering.

### What about MCP servers?

AIOS plays nicely with MCP. The Postgres MCP, WhatsApp MCP, Google Calendar MCP, Notion MCP — install whichever ones match the tools your business uses, and reference them from your skills. The example skills use plain SQL (assumes a Postgres MCP is configured), but you can swap in MCP tool calls anywhere.

---

## Roadmap

This is what I'm shipping next under the AIOS banner:

- [ ] **`bisnesgpt` template** — a multi-tenant WhatsApp + Claude backend you can self-host. Pairs with AIOS for the messaging layer.
- [ ] **`aios-dashboard` template** — a Next.js dashboard scaffold that reads from any AIOS workspace's `outputs/` and `current-data.md`. For when you want a glance-able view alongside the conversation.
- [ ] **`aios-app` template** — a Flutter starter for customer-facing mobile apps that talk to your AIOS workspace.
- [ ] **Vertical packs** — pre-configured AIOS workspaces for specific industries (carpet/furniture seller, KOL agency, solar, F&B).

Subscribe to [my newsletter](#) (coming soon) for updates.

---

## Contributing

If you build something interesting on AIOS — a new skill, a vertical pack, a clever automation — open a PR or just send it to me on [LinkedIn](https://www.linkedin.com/in/firazfhansurie/) / [Threads](https://www.threads.net/@ferazfhansurie). I'll feature good ones in the README.

Bug reports and improvements are welcome. Issues triaged when I have time — paid support available via [Adletic](mailto:firaz@adletic.com).

---

## License

MIT. Use it, fork it, sell consulting on top of it. If it helps your business, tell me — I want to hear how you use it.

---

## Built by

[Adletic Agency](https://adletic.com) — AI builds for Malaysian SMBs.
[Firaz Fhansurie](https://www.linkedin.com/in/firazfhansurie/) on LinkedIn.
