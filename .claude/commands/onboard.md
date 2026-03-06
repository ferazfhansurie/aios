## Adletic Team Onboarding

Welcome a new team member to AIOS — their AI co-worker at Adletic.

### Step 1: Who Are You?

Ask (one at a time, keep it conversational):

1. **What's your name?**
2. **What's your role / department?** (e.g., sales, account management, media buying, creative, dev, operations, finance, HR, strategy, intern — anything)

### Step 2: How Will You Use Me?

Let them pick freely. Present these as starting points, but make it clear they can add anything:

> **What kind of work do you want help with?** Pick as many as you want, or tell me something not on the list.
>
> **Writing & Content**
> 1. Copywriting — ads, captions, scripts, WhatsApp messages
> 2. Proposals & decks — client proposals, pitch docs, one-pagers
> 3. Emails & comms — drafting emails, follow-ups, internal updates
> 4. Content strategy — content calendars, campaign briefs, ideas
>
> **Research & Strategy**
> 5. Market research — competitor analysis, industry trends, benchmarks
> 6. Client research — company background, stakeholder intel, prep for meetings
> 7. Strategy & planning — campaign strategy, go-to-market, positioning
>
> **Data & Analysis**
> 8. Reporting — pulling numbers, building reports, summarizing performance
> 9. Data analysis — making sense of spreadsheets, dashboards, metrics
> 10. Client data (bisnesgpt) — contacts, messages, leads, WhatsApp campaigns
>
> **Operations & Admin**
> 11. SOPs & documentation — writing processes, guides, checklists
> 12. Project planning — task breakdowns, timelines, resource planning
> 13. Meeting prep & notes — agendas, summaries, action items
>
> **Technical**
> 14. Coding & development — building tools, scripts, automations, debugging
> 15. Automations — workflows, scheduled tasks, integrations
> 16. Design feedback — reviewing creatives, suggesting improvements
>
> **Client Work**
> 17. Client reporting — performance summaries, monthly reports
> 18. Client comms — drafting updates, handling requests, QBRs
> 19. Onboarding new clients — setup checklists, kickoff docs
>
> **Learning & Growth**
> 20. Upskilling — explain concepts, teach tools, practice skills
> 21. Brainstorming — ideas, problem-solving, creative thinking

If they mention something not listed, just roll with it.

### Step 3: Save Profile

Save to `.claude/context/client-info.md`:

```
# Team Member

- **Name:** {name}
- **Role:** {role}
- **Use Cases:** {what they picked, in plain language}
- **Onboarded:** {today's date}
```

### Step 4: Quick Setup

Based on what they picked, briefly explain how you can help with each area. No need to create skill files — just give them a clear picture of what to ask you for.

If they picked **Client data (bisnesgpt)**, ask which client(s) they work with and note the company_id(s) in their profile.

### Step 5: Confirm

Keep it short and hype:
- Welcome {name}!
- Here's what I'm set up to help you with: {list}
- Just ask me anything. No commands needed — just talk to me like a teammate.
