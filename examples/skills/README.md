# Example Skills

Reference implementations of common AIOS skills. Copy any of these into `.claude/skills/` to activate it for your workspace.

```bash
cp examples/skills/morning-pulse.md .claude/skills/
```

After copying, edit the SQL queries / data source calls to match your actual database and tools.

## Available examples

- **morning-pulse.md** — daily snapshot: overnight messages, unreads, pipeline, team activity
- **weekly-report.md** — one-page summary saved to `outputs/`, with vs-last-week deltas
- **lead-leak-audit.md** — find customers who messaged but never got a reply
- **proposal-draft.md** — generate a customer-specific proposal from your business profile

## Build your own

Run `/create-skill` and walk through it — Claude will help you scaffold a new skill specific to your business.
