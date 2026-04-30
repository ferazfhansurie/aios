# Skill: Proposal Draft

Generate a customer-specific proposal from your business profile and the customer's stated needs.

## Usage
"draft proposal for {customer}", "write a proposal", "make a quote for {customer}"

## Steps

### 1. Gather inputs

If the user just said "proposal for {customer}", check:
- `.claude/context/business-info.md` for products + pricing
- Past conversations / notes about this customer (if stored)
- Ask the user: "What are they trying to solve? Anything specific they mentioned?"

If anything is missing, ask. Don't invent.

### 2. Write the draft

Save to `outputs/{date}-proposal-{customer-slug}.md`:

```markdown
# Proposal — {Customer Name}
**Prepared by:** {Business Name}
**Date:** {today}

## What you've told us
{1-2 paragraph summary of their problem / goal in their own words}

## What we recommend
{1-3 deliverables that solve their problem. Each one named, with one line of why.}

## Investment
| Item | Price |
|---|---|
| {deliverable 1} | RM X |
| {deliverable 2} | RM Y |
| **Total** | **RM Z** |

Payment: {standard terms — adapt to business}

## Timeline
{Realistic delivery window}

## Why us
- {1-2 lines from business-info.md credentials / wins}
- {Relevant case study or past customer if applicable}

## Next step
Reply to this message with a thumbs up and we'll get started.
```

### 3. Present

Show the user the draft in chat. Ask:
- "Want to tweak the price / scope / timing?"
- "Want me to draft the WhatsApp message to send this with?"

Don't send anything automatically.

### 4. Track it

If the user confirms they sent it, append to `.claude/context/current-data.md`:
```
## Active proposals
- {Customer} — RM {amount} — sent {date} — status: awaiting reply
```

So next session you can ask "any updates on the {customer} proposal?"
