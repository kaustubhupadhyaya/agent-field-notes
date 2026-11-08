# Scrutinize before you build

Most build requests hide a goal. "Build me a dashboard that watches sessions" may mean "I keep losing track of what my agents are doing." The tool is one answer. The goal admits several.

## Separate the goal from the ask

Write two sentences:

- **Goal:** the outcome the person wants in their working life.
- **Ask:** the artifact they requested.

If the ask is the only thing on the table, every later decision inherits its assumptions. Name the goal first, then judge the ask against it.

## Search before you build

Look for existing open source before writing code. Search by the goal, not by the requested implementation:

- the goal itself
- the goal plus "faster"
- the goal plus "more"
- the underlying data source or protocol

Check GitHub, package registries, curated lists, and the runtime's own plugin registry. Record what you found and why it does or does not fit. A candidate that does 80 percent of the goal is often better than a new tool that does 100 percent of the ask.

## Use named quality attributes

Score the ask and the alternatives on the same axes:

- time to value
- maintenance burden
- portability across machines and runtimes
- resource consumption
- speed
- scalability
- observability
- testability

Weight them for the actual context. A solo user on one laptop should weight time to value and maintenance above raw scalability. A team with a deployment pipeline should weight the opposite.

## Check candidate health

For every serious candidate:

- last commit date
- license
- open issues and release cadence
- install prerequisites
- whether the README matches the current code

A dead project with a good README is a trap.

## Proportionality

Not every task deserves this pass. A one-off script, a throwaway query, or a five-minute fix should skip it. Apply the gate to anything that will run more than once, touch shared state, or be maintained.

## One verdict

Close with a single recommendation:

- adopt
- adapt
- compose
- build differently
- build as asked

Include the evidence, the rejected options, and the condition that would change the answer. The point is to make the next action obvious, not to display a comparison table.
