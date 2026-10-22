**Draft plan.md**

Plan autonomously from here: do not ask the person anything. First read one or two existing implementations of the same kind, their tests and the lint configuration, and note the repo's patterns.

Write how a caller will use the change before choosing its shape: two or three real call sites, or the user's steps. Sketch at least two structurally different shapes that serve that usage. Pick the one that hides more behind a smaller interface and matches what you would build if the requirement had existed from the start; record the losing shape and why. Design for a next contributor who sees only the file it opened, copies the nearest example and takes the shortest path that compiles: reject shapes where one piece of state has two writers, one task has two ways to do it, the same list lives in two places, or a new flag must stay in sync with an old one. When the change is one or two files with an obvious approach, say so and keep the plan to the tasks and checks.

Write plan.md with: Context and goal; Requirements (R1...) and non-goals; Approach, including the technologies needed and the trade-offs considered with the option chosen and why; File structure; a coverage map from every requirement ID to the tasks that deliver it; then the tasks, each stating what it delivers, the units involved, the requirement IDs it covers, real code for the core (signatures, data structures, key logic, key tests, test first, no placeholders), and its verification (exact commands and expected results). Close with a Verification section for the whole change: the exact test, build, typecheck and lint commands, and the checks that prove each requirement.

**Fresh review**

Have a fresh-context subagent review plan.md once: requirement coverage, placeholders, missing core code, wrong path or tool assumptions, and divergence from repo patterns. Apply what it finds; record anything left as a residual.

**Save plan.md**

Save it as the ticket document plan.md, with a closing "Decisions" section listing the business decisions the person made, the technical decisions you made, and residuals. Do not create design.md.
