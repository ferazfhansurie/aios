# Skill: Lead Leak Audit

Find customers who messaged the business but never got a reply within a reasonable window. These are dropped leads — money on the floor.

## Usage
"lead leak", "who did we miss", "unreplied leads", "leak audit"

## Steps

### 1. Define "leaked"

Default: any customer whose last inbound message is **>24h old** AND there's no outbound reply after that message. Adjust if the business has a different SLA.

### 2. Query

```sql
-- For Postgres-backed message stores. Adapt for Firebase / other.
WITH last_msgs AS (
  SELECT
    contact_id,
    MAX(CASE WHEN from_me = false THEN timestamp END) AS last_in,
    MAX(CASE WHEN from_me = true  THEN timestamp END) AS last_out
  FROM messages
  WHERE company_id = '{{COMPANY_ID}}'
    AND timestamp > NOW() - INTERVAL '30 days'
  GROUP BY contact_id
)
SELECT
  c.name,
  c.phone,
  to_char(l.last_in, 'YYYY-MM-DD HH24:MI') AS last_message_in,
  EXTRACT(epoch FROM NOW() - l.last_in) / 3600 AS hours_since
FROM last_msgs l
JOIN contacts c ON c.id = l.contact_id
WHERE l.last_in IS NOT NULL
  AND (l.last_out IS NULL OR l.last_out < l.last_in)
  AND l.last_in < NOW() - INTERVAL '24 hours'
ORDER BY l.last_in DESC
LIMIT 30;
```

### 3. Categorize

For each leaked lead, try to enrich:
- Their first-message intent (if you can read message bodies — was it a price question? complaint? booking?)
- Whether they're a known customer or cold
- Last spend amount if available

### 4. Present

```
Lead Leak Audit — {date}

{N} leads went cold in the last 30 days.

🔥 High value (cold >24h):
- {Name} ({hours_since}h ago) — last said: "{last message preview}"
- ...

🟡 Medium (cold 24-72h):
- ...

🧊 Old (cold >72h, probably gone):
- ...

Suggested next move:
- Hot list: send a personal "still need help?" message today
- Medium: batch follow-up template
- Old: write off OR re-engagement campaign
```

### 5. Optionally trigger follow-up

Ask the user: "Want me to draft re-engagement messages for the hot list?" If yes, write a personalized message per lead and save to `outputs/{date}-leak-followups.md` for review before sending.
