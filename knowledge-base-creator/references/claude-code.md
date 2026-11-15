# Claude Code

## Stack
Not imposed. Propose a stack with a one-line reason and ask only for confirmation. Starting proposals:
- web app with backend and Supabase: Next.js with TypeScript and Tailwind, Supabase client, deploy on Vercel;
- web app without backend: React, Vite, TypeScript and Tailwind;
- local prototype with a database: SQLite with Drizzle.
The reason must be tied to the idea, not to the stack itself: for example "Next.js because you need server routes to call the model without exposing the key".

## Where each file goes
- `CLAUDE.md` in the repository root: the permanent rules (`00`) plus a short index of the project files. It is loaded at every session, so keep it under about 200 lines. List the files in `docs/` by path in backticks, with one line on when to open each: Claude Code then reads them when the task requires it. Do not import them all with the `@docs/file.md` syntax: an imported file is loaded in full at every session, so use `@` only for a file that every task needs.
- `docs/`: all the other knowledge base files. Here it makes sense to split `07` into `07-architecture.md`, `08-database.md` and `09-api.md`, but only if there is real material for each.
- `04-runtime-ai-context.md` becomes the system prompt of the server route that calls the model, loaded from a file in the code.
- Secrets in `.env.local`, excluded from git, with a `.env.example` that lists the variables without values. `06` has a task for this.

The placement index in `03` says: create `CLAUDE.md` with this content, put the other files in `docs/`, then start Claude Code in the folder and give prompt 0.

## Database
- Supabase: client with the public key in the browser only if there are RLS policies on every table; everything else goes through the server with the service key, which never leaves the server. Migrations versioned in the repository.
- No database: localStorage.
- Other (SQLite, Neon, another Postgres): connection string in the environment variables, migrations in the repository.

## How to write the prompts
On Claude Code the prompts are tasks. Each one has:
- the goal in one sentence and the files in `docs/` to read first;
- what to build and what not to touch;
- the verification commands to run at the end (build, lint, tests if there are any);
- the request to update `docs/06-tasks.md` and, if a choice changed, `docs/05-decision-log.md`;
- a commit with a message that says what was done.

Prompt 0 goes in plan mode: Claude Code reads `CLAUDE.md` and `docs/`, proposes the plan and waits for approval.

In the "If something breaks" section: `git` is the safety net, so go back to the last commit that worked and rephrase the task more narrowly.
