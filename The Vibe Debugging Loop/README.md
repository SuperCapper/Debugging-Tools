Vibe coding has a loop. So does vibe debugging. Done badly, it spirals. Done well, it closes in two or three turns.

1. The symptom shows up. A user reports it, a test fails, a Sentry alert fires, the page is suddenly slow. Something that worked yesterday does not work today.

2. You frame the symptom in natural language. Not "TypeError on line 47," but "after a user signs up, the dashboard loads for them but the sidebar is empty." The model investigates intent, not just text.

3. You feed the AI structured context. This is the part most people skip. The model needs:

   - The exact error message and stack trace
   - The relevant source file (not the whole repo)
   - The most recent diff in the affected area
   - One signal of production state: a log line, a query result, a screenshot

4. You ask for an explanation before a fix. Have the model walk through its theory. If the theory is wrong, you catch it before any code changes. If the theory is right, the patch is usually trivial.

5. You verify by running the failing case yourself. Not "tests pass" — verify the actual flow. AI-generated fixes often pass tests by deleting the failing assertion.

6. If the bug is systemic, stop and escalate. Two failed attempts means the model does not have the right context, or the bug is not localized. Get a human in the loop.

That is the whole protocol. Most "vibe debugging is a nightmare" stories come from skipping step 3 and 4 and chasing the loop in step 5 forever.

Two adjacent practices keep the loop short:

- **Vibe logging.** Before you re-prompt, add print statements, assertions, or instrumentation to the code path you suspect. Give the next AI turn signal it cannot otherwise see. This is the cheapest leverage in the workflow.
- **Vibe refactor.** Once a fix lands, schedule a small follow-up session to rename, deduplicate, and comment the touched area. AI-generated code tolerates this beautifully and the next debug session benefits.
