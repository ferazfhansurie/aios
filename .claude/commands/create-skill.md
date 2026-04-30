## Create a New Skill

Walk the user through creating a custom skill — a repeatable workflow for this business.

### Step 1: Understand

Ask: **What do you want this skill to do?**

Examples to prompt their thinking (don't list all of these — just one or two):
- "Audit leads we've gone quiet on"
- "Weekly revenue + expense report"
- "Find customers I haven't messaged in 30 days"
- "Daily morning pulse — unreads, deals, team activity"
- "Generate a proposal for {customer}"
- "Check whether anyone replied to my last blast"

### Step 2: Map it out

Based on their answer, figure out:

- **Data sources** — which tables, APIs, files does this skill need to read?
- **Logic** — what does the skill compute or look for?
- **Output** — table? Chart? Markdown report? File saved to `outputs/`?
- **Trigger** — what phrase makes them want this skill? (Used in the `## Usage` section.)
- **Cadence** — one-off, daily, weekly?

If the data isn't easily queryable yet (e.g. they mention "I want X but the data lives in WhatsApp screenshots"), tell them honestly: *"This skill needs you to first do Y. Want to set Y up now or skip this skill?"*

### Step 3: Write the skill file

Create `.claude/skills/{kebab-case-name}.md`:

```
# Skill: {Name}

{One-line description.}

## Usage
{Phrases the user might say to trigger this skill.}

## Steps

### 1. {What to query}
{The actual query, API call, or file read.}

### 2. {How to analyze}
{The logic — filter, aggregate, compare.}

### 3. {How to present}
{The output format. Table? Bullets? Saved file?}

### 4. (Optional) Save to outputs/
{If the output is meaningful, save it as outputs/{date}-{slug}.{ext}.}
```

### Step 4: Test

Run the skill once to make sure it works. Show the user the result. If it's wrong, iterate.

### Step 5: Optional shortcut

Ask: "Want a slash command for this so you can trigger it faster?" If yes, create `.claude/commands/{name}.md` that just says "Run the {name} skill."

### Step 6: Confirm

> "Skill created. Say 'X' or run `/Y` to use it."
