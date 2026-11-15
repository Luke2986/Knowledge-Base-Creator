# Other tools

When the user picks a tool that is not covered (Bolt, Cursor, v0, Windsurf, Base44 or another), there are three things to find out, and you must not invent them.

1. Where the tool keeps permanent context: a project instructions field, a rules file in the repository, nothing. If you do not know for sure, look it up in the official documentation with web search. If you find no reliable answer, ask the user with options: 1. An instructions or knowledge field in the settings 2. A rules file in the project 3. I don't know, write `03` so that I paste the context in the first prompt.
2. Whether it has a built-in database, and which.
3. Whether it has a plan mode and a way to go back to a previous version.

With these three answers, write `03` as for the other tools. If the tool has no permanent context, prompt 0 contains the permanent rules in full and the condensed master plan, and every later prompt opens with "reread the rules in the first message".

The stack follows the tool: if the tool imposes it, record it in `05` as a constraint; if it is free, propose one as for Claude Code.
