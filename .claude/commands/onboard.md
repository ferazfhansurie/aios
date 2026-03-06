## AIOS Client Onboarding

Set up this workspace for a specific client. You already know the Adletic business — this is about connecting to the client's data.

### Step 1: Which Client?

Ask:
- Client/company name?
- What do they do?
- What's their `company_id` in the database?

If they don't know the company_id, find it:
```sql
SELECT id, name FROM companies ORDER BY created_at DESC LIMIT 20
```

Save to `.claude/context/client-info.md`.

### Step 2: Discover Their Data

Using the client's `company_id`, explore what data exists:

```sql
SELECT table_name FROM information_schema.tables
WHERE table_schema = 'public' ORDER BY table_name
```

Then check what this client actually has:

```sql
SELECT count(*) as contacts FROM contacts WHERE company_id = '{company_id}';
SELECT count(*) as messages FROM messages WHERE company_id = '{company_id}';
SELECT count(*) as conversations FROM conversations WHERE company_id = '{company_id}';
SELECT count(*) as leads FROM firaz_leads WHERE company_id = '{company_id}';
SELECT count(*) as campaigns FROM blast_campaigns WHERE company_id = '{company_id}';
SELECT count(*) as scheduled FROM scheduled_messages WHERE company_id = '{company_id}';
```

For tables with data, get the column details:
```sql
SELECT column_name, data_type FROM information_schema.columns
WHERE table_name = '{table}' AND table_schema = 'public'
ORDER BY ordinal_position
```

Save discovered schema + data counts to `.claude/context/database-schema.md`.

### Step 3: Data Snapshot

Run quick queries to understand the client's current state:
- Recent messages (last 7 days, inbound vs outbound)
- New contacts (last 7 days)
- Unread conversations
- Any active campaigns
- Pipeline stages if leads exist

Save snapshot to `.claude/context/current-data.md`.

### Step 4: Create Skills

Based on what data exists, suggest and create skills. Only create skills for tables that have data:

- **Has contacts + messages?** → Lead Audit skill (find unanswered inbound)
- **Has firaz_leads?** → Pipeline Report skill
- **Has conversations?** → Unread Follow-up skill
- **Has blast_campaigns?** → Campaign Report skill
- **Has messages?** → Daily Dashboard skill (message volume, response rate)

For each skill, create a `.md` file in `.claude/skills/` with the actual SQL queries using the client's `company_id`.

### Step 5: Confirm

Show summary:
- Client: {name} (company_id: {id})
- Data: X contacts, Y messages, Z leads...
- Skills created: list them
- Run `/prime` to start working
