Think before coding: state your assumptions and check them against the code. Simplicity first: if 200 lines would do what 50 can, rewrite it. Surgical changes: every changed line traces to the task; leave unrelated code alone and mention dead code rather than deleting it. Goal-driven: turn each task into a check a test can prove, and prove it.

The project's existing pattern beats your preference. Simplicity beats flexibility. Add a new pattern only when it is needed, clearly better and will repeat. Prefer conceptual simplicity over optimization.

Write the test before the code and run it: it must fail, and fail because the behavior is missing, not because of a typo or a missing import. A test that passes on its first run proves nothing; fix the test until it fails for the right reason. For a bug, start with a test that reproduces it, and say in the pull request how you saw it fail.
