## Prime Session

Load all context and prepare for a working session.

1. Read all context files:
   - `.claude/context/client-info.md`
   - `.claude/context/current-data.md`
   - `.claude/context/database-schema.md`

2. If `client-info.md` contains `[NOT SET]`, tell the user to run `/onboard` first and stop.

3. List available skills from `.claude/skills/` directory.

4. Run a quick data pulse using the client's `company_id`:
   - Unread conversations
   - Messages in last 24h (inbound vs outbound)
   - New contacts in last 7 days
   - Pipeline summary if leads exist

5. Brief status:
   - Client name + key metrics
   - Anything urgent
   - Available skills

Keep it tight — 30-second boot-up.
