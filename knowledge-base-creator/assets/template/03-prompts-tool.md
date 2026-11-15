<!-- TEMPLATE. The file name becomes 03-prompts-lovable.md, 03-prompts-replit.md, 03-prompts-claude-code.md or 03-prompts-<tool>.md. Read references/<tool>.md first. Write it in the output language, prompts included; interface copy quoted inside a prompt is in the app's language. -->

# Prompts for <tool>

## Placement index
<!-- Operational instructions, in order, on where each file goes before the first prompt. Lovable example: "1. Workspace settings, Knowledge: paste 00. 2. Project settings, Knowledge: paste the condensed version of 01, 02 and 07. 3. 04 does not go in the knowledge: you paste it into the edge function at prompt 3." Always distinguish the context that guides the agent that builds from the one that guides the AI inside the app. -->

## How to use these prompts
One at a time, in order. After each prompt run the checks listed below and move to the next one only if they all pass. If one does not pass, fix that point before going on.

## Prompt 0: the plan
<!-- In plan mode if the tool has one. Asks to read the context and propose the build plan by phases, without writing code. -->

> <prompt text>

Check: the plan follows the order of this file and adds no functions outside the scope of the master plan.

## Prompt 1: <interface with fake data>

> <prompt text: what to build, with an explicit reference to the design system; what not to create yet (backend, tables, server functions, AI)>

Check before going on:
- <checks observable in the preview, tied to the tasks in 06>

## Prompt 2: <persistence>
<!-- Chosen database or localStorage. If there is a database with users: tables, RLS policies, no access from the client without a policy. -->

## Prompt 3: <runtime AI, if there is one>
<!-- Server-side function, key as a secret, content of 04 as the system prompt in full, response format identical to the contract in 07, handling of loading and error, invalid response from the model. -->

## Prompt 4 onwards: <secondary functions, one per prompt>

## If something breaks
<!-- Instruction specific to the tool: restore a version, checkpoint or commit, then rephrase the prompt more narrowly. -->
