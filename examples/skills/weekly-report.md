# Skill: Weekly Report

A one-page summary of the week. Save to `outputs/` so the team can share or archive it.

## Usage
"weekly report", "what happened this week", "weekly recap"

## Steps

### 1. Define the window

```sql
-- Default: last 7 days. Override via natural language ("show me last week", "weekly report for Oct")
WHERE created_at >= NOW() - INTERVAL '7 days'
```

### 2. Pull headline numbers

For a typical SMB, try to compute:

- **Revenue** — sum of paid invoices / orders / payments in the window
- **New customers** — distinct customers with first activity in the window
- **Active customers** — distinct customers who interacted (message, purchase, login)
- **Pipeline** — deals moved into "won", deals added new
- **Costs** — sum of expenses in the window (if tracked)
- **Net** — revenue minus costs

Adapt the queries to whatever data the business has.

### 3. Pull notable events

- Biggest deal closed
- Top customer this week (by spend or activity)
- Anything stuck (overdue invoices, unresponded leads)

### 4. Compare to previous week

For each headline number, compute the % change vs the previous 7-day window. Show ↑ green / ↓ red badges.

### 5. Generate the report

Save as `outputs/{YYYY-MM-DD}-weekly-report.md`:

```markdown
# Weekly Report — {start date} → {end date}

## Headlines
| Metric | This week | Last week | Δ |
|---|---|---|---|
| Revenue | RM X | RM Y | ↑ Z% |
| New customers | 12 | 9 | ↑ 33% |
| Active customers | 87 | 92 | ↓ 5% |

## Notable
- Closed: {Customer A} — RM X
- Top of mind: {Customer B} — {what's pending}
- Stuck: {N invoices overdue, total RM X}

## Suggested actions for next week
1. {action}
2. {action}
3. {action}
```

### 6. Present in chat

Show the highlights in chat (top 3-5 lines), then say "Full report saved to outputs/{filename}." so the user can open it.
