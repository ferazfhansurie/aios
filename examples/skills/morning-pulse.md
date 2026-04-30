# Skill: Morning Pulse

A daily snapshot of the business — what happened overnight, what needs attention today.

## Usage
"morning", "gm", "brief me", "morning pulse", "what's happening"

## Steps

### 1. Pull last 24h activity

Adapt the queries below to whatever data sources this business has. Common ones:

```sql
-- Last 24h customer messages (if WhatsApp / chat data is in Postgres)
SELECT contact_name, last_message, timestamp
FROM messages
WHERE company_id = '{{COMPANY_ID}}'
  AND timestamp > NOW() - INTERVAL '24 hours'
  AND from_me = false
ORDER BY timestamp DESC
LIMIT 20;

-- Unread / unreplied
SELECT name, phone, unread_count
FROM contacts
WHERE company_id = '{{COMPANY_ID}}'
  AND unread_count > 0
ORDER BY unread_count DESC
LIMIT 10;
```

For other data sources, swap in the equivalent (Firebase queries, Sheets reads, API calls).

### 2. Pull pipeline state

```sql
-- Active deals / opportunities
SELECT name, stage, value, updated_at
FROM deals
WHERE company_id = '{{COMPANY_ID}}'
  AND stage NOT IN ('won', 'lost')
ORDER BY value DESC
LIMIT 10;
```

### 3. Pull team activity

```sql
-- Who did what yesterday
SELECT employee_name, action_type, COUNT(*) as count
FROM activity_log
WHERE company_id = '{{COMPANY_ID}}'
  AND created_at > NOW() - INTERVAL '24 hours'
GROUP BY employee_name, action_type;
```

### 4. Present

```
Morning, {{NAME}}.

Overnight ({date}):
- {N} new messages — top: {top contact / topic}
- {N} unread — biggest: {worst-offender contact}
- {N} pipeline movements — {key deal}

Today's priorities (suggested):
1. {customer who's been waiting longest}
2. {deal closest to closing}
3. {anything overdue}

What's the play?
```

### 5. Update current-data.md

Append today's snapshot to `.claude/context/current-data.md` so the next session has context.
