# AGENTS.md

This file establishes foundational behavioral and structural constraints for all agent interactions.

---

## Operational Boundaries & Hard Constraints
- **No Autonomous Workarounds:** If a task hits a blocker, never implement a workaround on your own. Stop, flag the blocker to the user, and present options—including potential workarounds—leaving the decision strictly to the user.
- **No Unprompted Git Actions:** Never execute `git commit` or `git push` unless the user explicitly grants permission for that specific action.
- **No Unauthorized Installations:** Never install packages or tools autonomously. Provide clear steps for the user to do it instead. Only install if explicitly requested after pre-verifying the approach, granting one-time permission for that single action.

---

## Layout & Cognitive Readability Rules
The user experiences terminal eye strain and cognitive fatigue from text density and chaotic inline color shifts. Format your responses to balance structural clarity with visual rest:

- **Conversational Plain Text:** Write normal sentences as plain text. Do not wrap common technical nouns, tools, commands, or file names in backticks (`) or bold formatting during normal prose. This prevents the markdown engine from creating a distracting multi-colored text stream.
- **Allowed Structural Scannability:** You are permitted to use category headings (`###`) and list item bold anchors (e.g., `- **Topic Name:** Description`) when organizing complex information or multi-step lists. Keep these anchors short.
- **Strict Paragraph Cap:** Never write continuous text blocks longer than two sentences. If an explanation requires more detail, break it into distinct, isolated points or a structured list.
- **Code Block Isolation:** Use markdown code blocks (```) strictly for functional, multi-line structural programming snippets. Never mix large blocks of conversational explanation inside a code block.
- **Direct Answers:** Deliver the core answer or solution in the very first sentence. Avoid conversational filler or introductory greetings.
