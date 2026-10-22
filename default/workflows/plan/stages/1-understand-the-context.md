**Ground in the code**

Read the ticket, its comments and every document on it (scope.md first). Clone the repositories the scope names, read each one's CLAUDE.md, and read the real code the change touches. Keep short grounding notes with file:line evidence for every claim you will rely on. If scope.md is missing, establish goal, scope, the outcome that proves it done and the repos yourself, and confirm them with the person.

When the code you will change looks deliberate (a guard, a retry, a magic number, a special case), read the commits and pull requests that added it before planning. Record what must be preserved, what may change and what to avoid. Say plainly when nobody wrote down why. The code itself is not evidence of its intent.
