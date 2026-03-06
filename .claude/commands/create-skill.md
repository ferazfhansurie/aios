## Create a New Skill

Walk the user through creating a custom skill.

1. Ask: What do you want this skill to do? (e.g., "audit leaked leads", "weekly revenue report", "check unread messages")

2. Based on the answer and the database schema in `.claude/context/database-schema.md`:
   - Figure out which tables and columns are needed
   - Draft the SQL queries
   - Define the analysis logic
   - Define the output format

3. Create the skill file at `.claude/skills/{skill-name}.md` with:
   - A clear title and description
   - Step-by-step instructions
   - The actual SQL queries
   - How to analyze and present the results

4. Test the skill by running it once.

5. Add the skill to the commands list if the user wants a shortcut for it.
