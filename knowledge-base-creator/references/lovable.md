# Lovable

## Stack
Imposed by the tool: React and TypeScript with Tailwind and shadcn/ui components, on Vite in older projects and on TanStack Start in newer ones. Do not propose alternatives and do not ask the stack question. In `07` write the stack as a fact, and in `05` record it as a constraint of the tool. If you cannot tell which base a project is on, write "the base Lovable generates for this project" and add a check after prompt 0 to fill it in.

## Where each file goes
Lovable has two levels of permanent context: the workspace knowledge, single and shared by all projects, and the project knowledge of the single project. Lovable applies short, concrete instructions better, so the knowledge has to be condensed: the full files stay the source, the knowledge gets the essential version.

- `00-permanent-rules.md` goes in the workspace knowledge. It is pasted once: if the user already has it from a previous project, they update it instead of duplicating it.
- `01-master-plan.md` and `02-design-system.md` go in the project knowledge, condensed: purpose, users, scope, out of scope, tokens and component rules. Drop the explanatory paragraphs.
- `07-architecture.md` goes in the project knowledge for the parts the agent must respect: folder structure, data model, table names, function contracts.
- `04-runtime-ai-context.md` never goes in the knowledge. It is the system prompt of the edge function that calls the model, it guides the AI that answers inside the app at runtime and not the agent that builds. In the prompt that integrates the AI, ask to paste it in full into the function.
- `03`, `05` and `06` stay with the user: `03` to give the prompts, `05` and `06` to keep track. If the project is synced to GitHub, it is worth saving them in the repository too, in `docs/`.

The placement index in `03` must give these as steps to follow: "Open the workspace settings, Knowledge section, paste the content of 00".

## Database
- Lovable Cloud: the default backend of new projects, built on the Supabase stack. Tables, auth, storage, edge functions and secrets are managed from the editor, with no separate Supabase account. Choose this route when the user has no reason to own the backend.
- Supabase with your own account: same technology, but the Supabase project belongs to the user, with the full dashboard and the option to move the backend elsewhere. The connection is made from Lovable's integrations. In `05` the entry must explain why one or the other was chosen.
- No database: the browser's localStorage. Fine for a single user on a single device, with no login. In `05` the "revisit when" is: you need sync across devices, multiple users or sharing.

With a database and multiple users, the architecture must include RLS policies on every table with personal data, and the persistence prompt must ask for them explicitly.

## Native integrations
Lovable already covers much of what an app needs beyond the MVP, so the knowledge base names the native route and forbids rebuilding it by hand.

- Login, file storage and server functions come with Lovable Cloud.
- Payments are built in, with Stripe or Paddle as provider: the user asks for them in chat and completes the provider's account setup. They need a paid Lovable plan, run in test mode in the preview and in live mode on the published app, and allow one provider per project. In `05` record the provider and the reason; in `06` add the provider's go-live steps as tasks.
- Other services (messaging, data, productivity, CRM) are connected from the connector catalog; a service that is not in the catalog can be reached through a custom connector or its API.

When a function in the scope matches one of these, the prompt says "use Lovable's built-in payments" or "use the Stripe connector" and adds "do not write a custom integration". The catalog changes often: check the current documentation before naming a connector, and mark the name with the verify marker if you cannot check it.

## Runtime AI
Always behind an edge function, never called from the browser, the key stays a server-side secret.
- Lovable AI gateway: no external keys to manage, unified billing. The quickest route.
- Claude: Anthropic key as a secret, called from the same edge function.
- Other providers: same pattern, key as a secret.

## How to write the prompts
- Prompt 0 goes in plan mode: the agent reads the knowledge and proposes the plan, without touching the code. The user compares it with `06` before moving on to building.
- The interface prompt asks for "frontend only, fake data, no edge functions, no tables".
- One prompt, one block that can be checked in the preview. Never two functions in the same prompt.
- Each prompt repeats in one line what not to create yet: backend, auth, tables, functions that come later.
- In the "If something breaks" section of `03`: if a prompt breaks the app, it is better to restore the previous version from the history and rephrase the prompt more narrowly, instead of piling correction prompts on top of broken code.
