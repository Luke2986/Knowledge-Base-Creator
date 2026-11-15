# Replit

## Stack
Not imposed. Propose a stack with a one-line reason and ask only for confirmation. Starting proposal for a web app with a backend: React and Vite on the frontend, Express on the server, Drizzle as ORM on PostgreSQL, all in the same project. Reason to give the user: it is the stack Replit's Agent handles with the least friction, with a single project to deploy. If the app has no backend, React and Vite are enough.

## Where each file goes
The Agent's permanent context lives in the `replit.md` file in the project root, which the Agent rereads at every session.

- `replit.md` contains the permanent rules (`00`) and an operational summary of master plan, design system and architecture, with a pointer to the full files.
- All the knowledge base files also go in `docs/` in the project, so the Agent opens them when the task requires it.
- `04-runtime-ai-context.md` becomes the system prompt of the server route that calls the model, for example loaded from `server/prompts/` as a text file. It does not go in `replit.md`.

The placement index in `03` says: create `replit.md` with this content, create the `docs/` folder with these files, then give prompt 0.

## Database
- Built-in PostgreSQL: it is enabled from the project and adds `DATABASE_URL` and the other credentials to the environment variables automatically, with separate development and production databases. Some guides report that the database goes to sleep after a few minutes without queries: add a task to `06` to handle reconnection, and in `05` a note to check against the current documentation.
- Supabase: credentials go in Replit's Secrets, never in the code. With multiple users, RLS policies on every table with personal data.
- No database: localStorage, as for the other tools.

On Replit there are no edge functions: server-side logic, including calls to the AI model, lives in the app's server routes. `07` must say so explicitly, because models tend to propose edge functions out of habit.

## Native integrations
Replit already covers much of what an app needs beyond the MVP, so the knowledge base names the native route and forbids rebuilding it by hand. The Agent supports four kinds of integration:

- Replit managed: built in, no setup. Database, App Storage for files, Replit Auth for login, Domains. Before choosing Replit Auth, check its current sign-in methods against who the app's users are.
- Connectors: first-party integrations the user signs in to once and reuses across apps, Stripe among them. Most require a paid plan.
- External integrations: third-party services the Agent sets up with the user's API keys, which go in Secrets.
- Agent services: paid third-party APIs the Agent uses without keys, billed to the user's Replit credits.

The Agent picks an integration from the service or function named in the prompt, so the prompt names it: "add Replit Auth", "add Stripe for payments", followed by "do not write a custom integration". In `05` record which kind was chosen and why; when an integration is billed to credits, say so in the "impact" line. The catalog changes often: check the current documentation before naming a connector, and mark the name with the verify marker if you cannot check it.

## Runtime AI
Provider key in Secrets, called only from the server, never from the browser. The route contract (request and response) goes in `07` identical to the output format of `04`.

## How to write the prompts
- Prompt 0: ask the Agent to read `replit.md` and the files in `docs/` and to answer with a plan, without writing code. If the Agent has a plan mode, use it.
- Same sequence as the other tools: interface with fake data, persistence, AI, secondary functions one per prompt.
- Each prompt closes with the checks and with "update `replit.md` if you changed structure or decisions".
- In the "If something breaks" section: go back to the previous checkpoint and rephrase the prompt more narrowly, instead of piling up corrections.
