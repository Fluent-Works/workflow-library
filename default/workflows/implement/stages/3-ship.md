Run the typecheck, the lint and the tests related to the changed files, and the build if the change could affect it; the full suite is CI's at the merge gate. Fix what you broke. Report only checks you actually ran.

Push the branch (never force) and open one draft pull request per repository titled "[TICKET-KEY] title", with a short body: what changed, how it was verified, and any decisions or follow-ups worth knowing. Register the pull request as an artifact. Your summary links the pull request and states what was built in a few lines.
