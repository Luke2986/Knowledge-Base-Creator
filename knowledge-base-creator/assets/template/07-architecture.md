<!-- TEMPLATE. Stack and location of the server logic depend on references/<tool>.md. The keys and types here are the source of truth for 01, 03, 04 and 06. On Claude Code, if database and API have real material, move those sections to 08-database.md and 09-api.md. Write it in the output language; keys, types and names stay in English. -->

# Architecture: <project name>

## Principles
1. Interface separate from logic.
2. AI separate from the interface.
3. Persistence separate from components.
4. No needless dependency.
5. Each module can be changed without breaking the others.

## Stack
<!-- Imposed or chosen, with a pointer to the entry in 05. -->

## Where the server-side logic lives
<!-- Edge function on Lovable Cloud or Supabase, server route on Replit or Claude Code, none if the app has no backend. Where secrets live. -->

## Folder structure
```text
<tree>
```

## Data model
```ts
// Types. One definition per entity, reused everywhere.
// If a field is a list of texts, it is string[] everywhere: in the type, in the contract, in the output of 04.
```

## Database
<!-- Only if there is one: tables, columns, relations, RLS policies per table. If data lives in the browser: localStorage key, saved format, what happens if storage is unavailable. -->

## Server-side function contracts
<!-- For each function: name, request, response, errors. The response of the AI function is identical to the output format of 04. -->

## User flows
<!-- For each flow of the MVP, the numbered steps. -->

## Module responsibilities
<!-- components: rendering only. services: server, persistence, AI, export. hooks: coordinate. -->

## Evolution rules
<!-- What changes and what stays fixed when auth, database, multiple users arrive. -->

## Architecture checklist
- [ ] Small components, no file over 300 lines
- [ ] No key in the client
- [ ] Interface independent of persistence and AI
- [ ] Types defined only once
