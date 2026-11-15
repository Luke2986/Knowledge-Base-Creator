---
name: knowledge-base-creator
description: Builds the starting knowledge base for developing software with an AI builder (Lovable, Replit, Claude Code or another tool) and delivers it as markdown files, namely permanent rules, master plan, design system, step-by-step prompts for the builder, context for the AI that runs inside the app, decision log, tasks and architecture. Starts from the idea and the details the user gives, asks only for what is missing with specific multiple-choice questions, one per message, adapts prompts, stack and database to the chosen tool, and writes in the user's language. Use it whenever the user has an idea for an app, tool, SaaS, MVP or prototype and wants to prepare the project before opening the builder, even without naming a knowledge base, for example "I want to build this idea", "prepare the files for Lovable", "write the master plan", "CLAUDE.md for the project", "voglio costruire questa idea", "prepara i file per Lovable". Not for fixing an app already in advanced development or for writing the code directly.
---

# Knowledge Base Creator

AI builders build well when they have a fixed context to reread, and go wrong when they have to rebuild it at every prompt. This skill prepares that context: a set of markdown files that describe what to build, how it should look, with which architecture, in what order, and under which rules. The user brings the idea, the skill asks only for what the user alone can know, drafts the rest, checks that the files agree with each other and delivers them.

## The files you produce

| File | When | What it contains |
|---|---|---|
| `00-permanent-rules.md` | always | How the agent works on any task: step by step, security, code structure, documentation, voice |
| `01-master-plan.md` | always | What, for whom, problem, principles, MVP scope, out of scope, done when, metrics, evolution |
| `02-design-system.md` | always | Character, visual hierarchy, tokens, typography, layout and breakpoints, components, states, accessibility |
| `03-prompts-<tool>.md` | always | Where each file goes in the tool and the step-by-step prompt sequence up to the MVP |
| `04-runtime-ai-context.md` | only if the app uses AI at runtime | The system prompt of the server-side function that calls the model: role, domain context, style, output constraints |
| `05-decision-log.md` | always | The decisions already made, with reason, alternatives and when to revisit them |
| `06-tasks.md` | always | Tasks grouped by prompt, each with its own "done when", plus QA |
| `07-architecture.md` | always | Stack, folders, data model, DB schema if there is one, server function contracts, flows, module responsibilities |

Only on Claude Code, and only if there is real material to fill them, `07` splits into `07-architecture.md`, `08-database.md` and `09-api.md`. Never create files that are empty or filled with guesses, such as deployment or troubleshooting at the start: the agent takes them as true. Write the troubleshooting file when the first problem appears.

The template for each file is in `assets/template/`. Read them before writing: each template explains what goes in each section and where it comes from.

## Language

Write the knowledge base and your messages in the language the user writes in. The file names in the table above and the technical keys (data model fields, table names, environment variables) stay in English in every language; headings and prose follow the user's language. If the app's interface is in a different language from the conversation, ask nothing: use the language the user states for the app in the app copy, in the style examples of `04` and in its output constraints, and the conversation language everywhere else. If the user states no language for the app, it is the conversation language. If the user asks for the files in a language other than the one they write in, that request wins. Headings and field labels quoted in these instructions and in the templates ("Done when", "Revisit when", "If something breaks") are translated like the rest.

Voice rules depend on the language. Read `references/voice-<language>.md` (`voice-en.md`, `voice-it.md`) for the output language. If there is no file for that language, apply `voice-en.md` and translate its banned-word list with the closest equivalents. In a language with two forms of address, use the informal one unless the user writes formally.

## Flow

### 1. Read the idea

The user gives you an idea with some details, sometimes two lines, sometimes a document. Before asking anything, extract everything already there on these points:

tool, database, AI inside the app and model, users, problem, main functions, what stays out of the MVP, when it is done, success metrics, visual references, language and register of the app.

What the user has already said you do not ask again, not even to confirm. If they said part of something, ask only for the missing part: if they write "with Supabase" without the tool, ask for the tool and skip the database.

### 2. Ask only the questions you need, one per message

Questions are always specific. Never ask "do you need saved data?" or "any design preferences?": give the list of concrete options and the user picks one or writes their own. Every list ends with "Other, tell me which". If you have a button-based question tool available (for example `ask_user_input_v0` on Claude.ai or the equivalent in Claude Code), use it for multiple-choice questions; otherwise use a numbered list.

Order of the questions, to skip when the answer is already there:

**Tool.** "Which tool are you building with?" 1. Lovable 2. Replit 3. Claude Code 4. Other, tell me which.

**Database**, with the options valid for the chosen tool:
- Lovable: 1. Lovable Cloud, the built-in backend 2. Supabase with your own account 3. No database, data stays in the user's browser 4. Other, tell me which
- Replit: 1. Replit's built-in PostgreSQL 2. Supabase 3. No database, data stays in the user's browser 4. Other, tell me which
- Claude Code: 1. Supabase 2. No database, data stays in the user's browser 3. Other, tell me which, for example SQLite or Neon
- Other tool: 1. Supabase 2. The tool's built-in database, if it has one 3. No database 4. Other, tell me which

**AI inside the app**, only if the idea does not make it clear: 1. No AI inside the app 2. Lovable AI gateway (only if the tool is Lovable) 3. Claude with an Anthropic key 4. OpenAI 5. Other, tell me which. With "none" you do not produce `04`.

**Stack**, only on Replit, Claude Code or another tool, where it is not imposed. Do not ask in the abstract: propose a stack with a one-line reason taken from the tool's reference file and give as options 1. Fine 2. I prefer another stack, tell me which.

**The questions only the user can answer**, one per message, only the missing ones: the problem, for whom, what stays out of the MVP, when it is done, the success metrics. These are open, but stay specific because they start from the idea. For a skills self-assessment app, bad: "What problem are you solving?"; good: "Today your user does the self-assessment and then what? What happens after they see the scores, and why is that not enough?". For out of scope and metrics you can offer two or three candidates drawn from the idea as options, always with "Other".

**Design**, in a single message: ask for concrete references (a site, brand colours, a logo, an existing design system) and in the same message propose three visual directions drawn from the idea, that is from who will use the app and in what context. Each direction fits in one line with palette, font pair and tone. If the user gives both a reference and a direction, the reference wins where it is precise and the direction covers the rest.

Ask nothing else. Everything else you draft yourself in step 3.

### 3. Draft the files

Read `references/<tool>.md` (`lovable.md`, `replit.md`, `claude-code.md`, `other-tools.md`), the voice file for the output language and the templates in `assets/template/`, then write the files.

What comes from where:
- from the user's answers and the idea: problem, for whom, scope, out of scope, done when, metrics, visual references, choice of tool, database and AI model;
- derived by you: principles, design system tokens and components, architecture, data model, DB schema, tasks, prompt sequence, domain context of `04`;
- fixed: the voice rules and the structure of the permanent rules.

For the domain context of `04` write a first version starting from the idea. The risk of this draft is that it fills up with plausible sentences that would fit any app of the same kind, which is what the domain context exists to avoid. So mark every sentence you draw from your general knowledge, and not from what the user wrote, with the verify marker at the end: `[to verify]` in English, `[da verificare]` in Italian, the translated equivalent in other languages, always in square brackets and always the same within a project. The user then knows where to look. The example of a well-made context is in `references/runtime-ai-context-example.md`.

The same marker applies in all other files to content the user named without writing it. If the idea says "three guiding questions" and does not list them, you draft them, each with the marker, instead of leaving a pointer to something that does not exist.

The prompts in `03` follow one rule: a prompt corresponds to a block the user can check in the preview in a few minutes. The order is plan, interface with fake data, persistence, runtime AI, secondary functions one per prompt. Each prompt says what to build, what not to touch, what not to create yet, and closes with the checks to run before the next prompt. Prompts stop at the MVP; later phases stay in the master plan.

### 4. Cross-check before delivering

The files are written at different moments and contradict each other easily. Before delivering, check and fix what does not match:

- the data model is identical in `07`, in the server function contract and in the output format of `04`: same key names, same types (for example not a `{text}` object on one side and a string on the other);
- every item in the MVP scope of `01` has at least one task in `06` and appears in at least one prompt of `03`;
- every state described in `02` (empty, loading, error, storage unavailable) has a task;
- every choice made in any file (tool, database, AI model, stack, chart library, no login) has an entry in `05`;
- every element one file mentions really exists somewhere: if the prompt says "the three questions in the master plan", the master plan contains them;
- no file breaks the voice rules of the output language: no em dash, none of the banned words.

### 5. Deliver

Write the files in a folder named after the project. On Claude.ai the folder is `/mnt/user-data/outputs/<project-name>/` and you present it with `present_files`; in Claude Code write to `docs/` in the repository root and `CLAUDE.md` in the root; if a `CLAUDE.md` already exists, do not overwrite it: write yours to `docs/proposed-CLAUDE.md` and say so. In the delivery message say in two or three sentences which file to start from and which parts carry the verify marker. No summary of the files: the placement index in `03` already does that job.

## Voice rules

The voice rules live in `references/voice-<language>.md`. They apply in two places: in the files you write and in your messages to the user, and inside the project, because you copy them into the permanent rules (`00`) and into the output constraints of `04`, so they end up in the app copy and in the answers of the AI at runtime.

If the app is in a different language from the knowledge base, the rules of register and style still apply and the banned-word list is the one for the app's language.

## Reference files

- `references/lovable.md`: where each file goes in Lovable, Lovable Cloud versus external Supabase, native integrations, AI gateway, how to write the prompts.
- `references/replit.md`: `replit.md`, built-in database, native integrations, Secrets, stack to propose, prompts for the Agent.
- `references/claude-code.md`: `CLAUDE.md` and the files in `docs/`, plan mode, stack to propose, tasks with checks and commits.
- `references/other-tools.md`: how to handle a tool that is not covered.
- `references/runtime-ai-context-example.md`: a well-made `04`, to use as calibration and not to copy.
- `references/voice-en.md`, `references/voice-it.md`: voice rules and banned words for each output language.
- `assets/template/`: the structure of each of the eight files.
