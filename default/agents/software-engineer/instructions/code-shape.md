One responsibility per function, split along the logical steps; each function states its input contract. Parse and validate at the boundary where data enters (requests, files, environment, the database); inside, trust the types and handle only the cases the type allows (empty, boundary, large). Do not add single-use indirection.

Model before naming: one concept, one name, reused everywhere; no synonyms; match the codebase's conventions. Names are short but distinct and carry unit and kind (timeout_ms, config_path, is_ready). Do not rename existing things unless the name is misleading or inconsistent, and propose that rather than doing it silently.

Duplication is fine when two things are different concepts that can diverge; shared code implies shared meaning. Put each change in the place that owns its scope; the next addition of the same kind should have an obvious home.

Never remove an existing comment unless your change made it wrong. Write a comment only for a why the code cannot show (a constraint, a workaround, a non-obvious invariant); never restate what the code does, and never record the development history.

Before writing a test, name the production change that would make it fail; if you cannot, test an observable behavior instead. Judge it against two imagined edits: if the behavior breaks, the test must fail; if the internals are restructured with the same visible result, it must still pass. Write expected values as literals worked out from the requirement, never with the code under test or its helpers. Assert on the real component; mock only the slow or external layer, with the full shape of its real data. Code that only tests call lives in test utilities, not in production classes. Prefer no new test over one that mostly tests mocks.

In tests and scripts, wait for the condition you need (an event, a state, a file) with a timeout and an error naming what you waited for, never a fixed sleep. A fixed delay is right only for behavior that is itself timed, after waiting for its trigger, with a comment saying why that length.

For any operation that changes state and can be retried, restarted or interrupted, answer what happens if it runs twice and if the last run stopped at any point. Derive each step from the state that exists, not from what the last run meant to do, and make anything a run leaves behind (a lock, a temp file, a claimed job) recognizable as stale. When two actors could write the same thing, give each its own file, key or record first; add a lock only when one shared writer is a real requirement.
