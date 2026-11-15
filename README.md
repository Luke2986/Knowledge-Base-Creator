# Knowledge Base Creator

Leggi in italiano: [README.it.md](README.it.md)

A skill for Claude that turns a software idea into the knowledge base to give an AI builder before writing a line of code. You bring the idea with the details you already have, the skill asks only the questions that are missing, one per message and with the options ready, then writes eight markdown files that agree with each other and are adapted to the tool you build with.

It works with Lovable, Replit and Claude Code, and handles other tools too by finding out where they keep permanent context.

## Why it helps

AI builders build well when they have a fixed context to reread, and go wrong when they have to rebuild it at every prompt: they add functions nobody asked for, create backends that are not needed, change the data model halfway through. This skill prepares that context before you open the builder, and splits the build into small prompts to check one at a time, so the agent does not try to do everything at once.

## What it produces

| File | When | Content |
|---|---|---|
| `00-permanent-rules.md` | always | How the agent works on every task: one step at a time, security, code structure, documentation, voice of the copy |
| `01-master-plan.md` | always | What, for whom, problem, principles, MVP scope, out of scope, done when, metrics, evolution |
| `02-design-system.md` | always | Visual hierarchy, CSS tokens, typography, breakpoints, components, states, accessibility |
| `03-prompts-<tool>.md` | always | Where to paste each file in the tool and the prompt sequence up to the MVP, each with its checks |
| `04-runtime-ai-context.md` | only if the app uses AI | The system prompt of the server-side function that calls the model: role, domain context, style, output format |
| `05-decision-log.md` | always | The decisions already made, with reason, alternatives and when to revisit them |
| `06-tasks.md` | always | Tasks grouped by prompt, each with the condition that says when it is done |
| `07-architecture.md` | always | Stack, folders, data model, database schema, server function contracts, flows |

On Claude Code, when there is enough material, the architecture also splits into `08-database.md` and `09-api.md`. The skill never creates files that are empty or filled with guesses.

## How it works

1. It reads the idea and extracts what you have already decided: tool, database, AI, users, functions, visual references. What you said it does not ask again.
2. It asks only the missing questions, with options specific to your case. If you choose Replit, for the database you see Replit's options; if you choose Lovable, Lovable's.
3. It asks you only what you alone can know, that is problem, for whom, what stays out, when it is done, metrics, and drafts the rest: architecture, data model, tasks, design system tokens.
4. For the design it asks for concrete references and in the same message proposes three visual directions drawn from the idea.
5. It marks with `[to verify]` the sentences it draws from general knowledge instead of from what you wrote, so you know where to look.
6. Before delivering it checks that the files do not contradict each other: same data model everywhere, a task for every scope item, a decision log entry for every choice.

## Supported tools and databases

| Tool | Permanent context | Database |
|---|---|---|
| Lovable | workspace knowledge and project knowledge | Lovable Cloud, Supabase with your own account, none |
| Replit | `replit.md` and `docs/` folder | built-in PostgreSQL, Supabase, none |
| Claude Code | `CLAUDE.md` and `docs/` folder | Supabase, SQLite, Neon or other, none |
| Other | looks it up in the tool's documentation or asks you | Supabase, built-in database, none |

"None" means data saved in the browser with localStorage, suited to a single-user MVP with no login.

On Lovable and Replit the skill points the builder to the native integrations (login, storage, payments, connectors) instead of having them rebuilt by hand.

## Installation

On Claude.ai upload the `knowledge-base-creator.skill` file from the Skills section of the settings.

In Claude Code copy the `knowledge-base-creator/` folder of this repository to `~/.claude/skills/` to have it in all projects, or to `.claude/skills/` inside a single repository:

```bash
git clone https://github.com/Luke2986/Knowledge-Base-Creator.git
mkdir -p ~/.claude/skills && cp -R Knowledge-Base-Creator/knowledge-base-creator ~/.claude/skills/
```

## How to use it

Describe the idea with the details you have, even a few. For example:

```text
I want to build on Lovable an app for self-assessing Product Manager
skills: eight sliders, a radar wheel and AI that suggests how to use AI
on the three strongest areas. No login, I save in the browser.
```

```text
Prepare the files for a tool on Replit: the hotel owner pastes a Google
or Booking review and gets three reply drafts in the property's tone.
```

The skill also triggers without being named, with requests such as "I want to build this idea", "prepare the files for Lovable", "let's set up the project" or "write the master plan".

## Repository structure

```text
Knowledge-Base-Creator/
├─ README.md
├─ README.it.md
├─ knowledge-base-creator.skill      package to upload to Claude.ai
└─ knowledge-base-creator/           the skill, to copy into Claude Code
   ├─ SKILL.md
   ├─ references/
   │  ├─ lovable.md
   │  ├─ replit.md
   │  ├─ claude-code.md
   │  ├─ other-tools.md
   │  ├─ runtime-ai-context-example.md
   │  ├─ voice-en.md
   │  └─ voice-it.md
   └─ assets/
      └─ template/
         ├─ 00-permanent-rules.md
         ├─ 01-master-plan.md
         ├─ 02-design-system.md
         ├─ 03-prompts-tool.md
         ├─ 04-runtime-ai-context.md
         ├─ 05-decision-log.md
         ├─ 06-tasks.md
         └─ 07-architecture.md
```

## Voice and language

The skill writes in the language you write in. File names and technical keys stay in English in every language.

Each language has its own fixed voice rules, which also end up in the app copy and in the answers of the AI at runtime: no em dash, no emoji, no "not only X but also Y" constructions, and a list of banned words. English and Italian are covered by `references/voice-en.md` and `references/voice-it.md`; for other languages the skill applies the English rules and translates the banned words. To change the rules or add a language, edit or add a `voice-<language>.md` file.

## Limits

The skill prepares the project, it does not write the code and it is not meant for tidying up an app already in advanced development. The information on the tools reflects Lovable, Replit and Claude Code as of September 2026, with native integrations and Claude Code's handling of `CLAUDE.md` rechecked in November 2026: the platforms change often, so the files in `knowledge-base-creator/references/` need updating when the way they handle context, database or secrets changes.

## Author

Luca Versilia, product manager and digital strategist.
