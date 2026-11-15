<!-- TEMPLATE. Fixed in structure and in almost all the content: adapt only the points marked ADAPT to the tool and the database. On Lovable it becomes the workspace knowledge, on Replit the first part of replit.md, on Claude Code the first part of CLAUDE.md. Keep it under 80 lines: it is read at every task. Write it in the output language. -->

# Permanent rules

These rules apply to every task in this project. If a request contradicts them, stop and ask before going on.

## How you work
- Do only what the prompt asks. Do not add functions, pages, tables, dependencies or backend that were not requested.
- One step at a time: finish the requested block, check that it works, stop and wait for the next prompt.
- Before changing a file the prompt does not name, explain why it is needed and ask.
- If a choice is not covered by the project documentation, propose two options with the reason and wait for the decision.
- Do not invent data, endpoints or table names: use the ones written in the architecture.

## Code structure
- Components only render: no fetch, no storage access, no business logic inside components.
- Server calls, persistence, AI and export live in services; hooks coordinate state, services and interface.
- Files under 300 lines. If a file goes over, split it and say so.
- Shared types in one place, never redefined in two files.
- No console.log in the code that stays.

## Security
- No key or secret in client code, ever. ADAPT: where secrets live (Lovable Cloud or Supabase secrets, Replit Secrets, .env.local excluded from git).
- ADAPT if there is a database with users: every table with personal data has RLS policies; no query from the client without a policy.
- Validate user input before saving it or sending it to the model.
- Calls to the AI model always go through a server-side function. ADAPT: edge function on Lovable, server route on Replit and Claude Code.

## Documentation
- When you complete a task, mark it as done in 06-tasks.
- When you change a choice recorded in the decision log, add a new entry in 05, do not edit the old ones.
- When you change structure, data model or contracts, update 07 in the same task.

## Voice of the app copy
<!-- Copy here the rules from references/voice-<language>.md for the language of the app, banned-word list included, and keep the line below. -->
- No exclamation marks of enthusiasm.
