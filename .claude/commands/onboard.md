## Onboard

Set up AIOS with a complete understanding of the business. Two modes:

### Detect Mode
If `.claude/context/personal-info.md` contains `[NOT SET]`, run **Full Onboard**.
Otherwise, run **Update Mode** — ask what they want to add or change.

---

## Full Onboard

Walk the user through this conversationally. Don't show it as a numbered form. Skip questions they've already answered. The goal is for them to feel like they're being interviewed by a smart partner, not filling in a survey.

### Step 1: Who

Ask:
1. What's your name?
2. What's your role in the business?
3. Tell me about the business — name, what it does, who it serves.

### Step 2: Business Profile

Cover these naturally:

**Revenue & Clients**
- Who are your current customers? Names, what they pay, how long.
- Roughly what's your monthly revenue? Monthly costs?

**Products & Pricing**
- What do you sell? Get pricing for each thing.

**Team**
- Who's on the team? Names, roles, contact info if relevant (e.g. WhatsApp numbers).

**Tools & Systems**
- What software do you actually use day-to-day? CRM, accounting, WhatsApp, ad platforms, project management — list what they mention.
- For each one, ask: where's the data? (Postgres? Firebase? Sheets? Just files? An API?)

### Step 3: Ingest Files

> Got any files I should know about? Drop them here — I can read:
> - **CSV / XLSX** — financials, customer lists, leads, inventory
> - **PDF / DOCX** — proposals, contracts, SOPs, brand guidelines
> - **Screenshots** — dashboards, analytics, anything visual
> - **JSON / SQL** — schema dumps, exports
>
> These go into my context so I can reference them in every session.

Save heavy files to `files/` and reference them in `business-info.md`.

### Step 4: Save Context

Save to `.claude/context/business-info.md`:
```
# Business Info

## Company
- Name: {name}
- What we do: {summary}
- Market: {who we serve}

## Products
- {product 1} — {pricing}
- {product 2} — {pricing}

## Customers
- {name} — {revenue} — {since when}

## Team
- {name} — {role} — {contact}

## Financials
- Monthly revenue: {amount}
- Monthly costs: {amount}
- Net: {amount}

## Tools
- {tool} — used for {what} — data lives in {where}
```

Save to `.claude/context/personal-info.md`:
```
# Team Member
- **Name:** {name}
- **Role:** {role}
- **Business:** {business name}
- **Onboarded:** {today's date}
```

### Step 5: Suggest First Skills

Based on what they've told you, suggest 2-3 starting skills that would be useful immediately. For example:
- If they mentioned WhatsApp customers → suggest a "morning pulse" skill (unread messages, recent activity)
- If they mentioned invoices → suggest a "weekly revenue" skill
- If they mentioned a sales pipeline → suggest a "deal review" skill

Tell them: "Want me to set any of these up now? Run `/create-skill` and pick one."

### Step 6: Confirm

Show a one-screen business snapshot and say:

> "Onboarded. What's the first thing you want me to help with?"

---

## Update Mode

If already onboarded, ask what to update:

- "Drop a file" → ingest, summarize, append to `business-info.md`
- "Update financials" → ask for new numbers, update
- "Add a customer" → append to customer list
- "Change my role" → update `personal-info.md`
- "Connect a database" → walk through DB connection setup, save creds to `.env`, test connection
