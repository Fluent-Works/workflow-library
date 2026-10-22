Read the ticket, its comments and documents (scope.md, design.md, ui-design.md, plan.md, whichever exist) and any design mocks registered as artifacts. Scope and design are settled upstream; take them as given and do not re-ask or re-design. If plan.md is missing, do not write one: just note the few tasks you will do and the files you will touch. When a decision has no clear answer, or several approaches exist with no clear winner, ask the person with AskUserQuestion; otherwise decide and move on.

Use the clone at repo/ in this directory, or clone it there with all branches; make the worktree at wt/ off the latest default branch on a branch named after the ticket identifier in lower case plus a short slug, and continue an existing branch if one exists. Read only the code the change touches.

When the build would depart from design.md or scope.md on purpose (a control hidden, a name changed, a state dropped), ask the person with AskUserQuestion before building it, with the departure as the recommended option; never build it and note it later.

Before changing anything, run the typecheck and the tests related to the files you will touch on the untouched worktree, and note any that already fail. If the area you are changing is already red, ask before building on it, with the failing output. Report pre-existing failures as such.
