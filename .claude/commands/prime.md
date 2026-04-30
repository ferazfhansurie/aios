## Prime Session

Fast context load. No external calls — just read files and get ready.

### Step 1: Load context (in parallel)

Read all of these:
- `.claude/context/personal-info.md`
- `.claude/context/business-info.md`
- `.claude/context/current-data.md`
- `.claude/context/communication-style.md`

If `personal-info.md` contains `[NOT SET]`, tell the user:
> "Looks like this is a fresh AIOS workspace. Run `/onboard` to set things up — takes about 5 minutes."

…and stop.

### Step 2: Present

Keep it under 8 lines. Format:

```
AIOS — {today's date}
{Name} | {Role} | {Business}

Last data: {date from current-data.md, or "no data yet"}
{2-3 most recent / important data points if available}

What's the play?
```

Don't list commands. Don't explain what AIOS is. The user knows.

### Step 3: Wait

Do not proactively pull data, send messages, or run skills. The user will tell you what they want. If they say nothing for a while, don't fill the silence.
