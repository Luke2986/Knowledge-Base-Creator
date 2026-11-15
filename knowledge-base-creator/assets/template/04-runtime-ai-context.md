<!-- TEMPLATE. Only if the app uses AI at runtime. It is the system prompt of the server-side function, it does not go in the builder's knowledge. Calibrate the specificity on references/runtime-ai-context-example.md. Put the verify marker of the output language at the end of every sentence drawn from general knowledge and not from the idea or the user's answers. Write it in the output language, so the user can check the sentences that carry the verify marker; write the two style examples in the language the runtime AI must answer in, and name that language in the output constraints. -->

# Context for the runtime AI: <what it generates>

This text is the system prompt of the server-side function that <what it does>. It does not go in the builder's knowledge: that guides the agent that builds the app, this guides the AI that answers inside the app.

## Role
<!-- Who the model is, who it works for, what the user wants to get, and the guiding principle of the product. -->

## How to reason
<!-- Which inputs arrive with each request and which weighs most. If the user writes notes or free text, they usually count more than any standard advice. -->

## Domain context
<!-- For each function, area or entity (same keys as 07): what it means in this app, where it shows, in which direction the AI must work. Examples of real inputs, not advice. They are not ready answers, they are the space to derive them from. -->

## Style, to use as calibration and not to copy
Good: <concrete example, starts from a real input, leaves the judgement to the person, can be started right away>. Why it works, in one sentence.
To avoid: <vague example>. Why it does not work, in one sentence.

## Quality checklist
- It starts from the user's input, not from standard advice.
- It would not fit just anyone: with a different user, it would change.
- It can be carried out without further explanation.
- No motivational language, no buzzwords.

## Output constraints
<!-- Quantity, length, language and register, voice rules from references/voice-<language>.md for the language of the app (no emoji, no em dash, the banned-word list of that language). Exact format of the response, identical to the contract in 07, with the keys provided in the request. "Answer only with valid JSON, with no text before or after." -->
