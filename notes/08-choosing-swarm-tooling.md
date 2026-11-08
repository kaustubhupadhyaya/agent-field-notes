# Choosing swarm tooling

Swarm tooling is easy to install and hard to justify. The useful question is "which bottleneck does this remove from work I actually repeat?", and the agent count is a distraction from it.

## Start from the work mix

Measure a sample of real sessions and classify the work:

- independent reading and verification: parallelizable
- writing and editing shared files: mostly serial
- interactive decisions: not parallelizable
- media rendering and live browser control: usually single-lane
- disk-heavy copies: contention-bound

A typical hard project is roughly half parallelizable read and verify work, a third serial write work, and a small interactive remainder. That ratio sets the ceiling on swarm benefit. If the parallel share is low, a swarm adds overhead.

## Score adoption cost

For each candidate, write down:

- runtime requirements (a container runtime, a language version, a CLI)
- install path and whether it replaces built-in agents
- isolation model (worktrees, containers, separate sessions)
- persistence and resume behavior
- license and maintenance activity
- failure behavior when a worker dies

A tool that requires a container runtime you do not have is not free. A tool that replaces built-in agents can break existing prompts. A tool with no terminal-state protection can hang a pipeline.

## Check health, not stars

Stars measure attention. Check the last commit, the open issue count, the license, and whether the README matches the code. Prefer a smaller project with recent commits over a large abandoned one.

## Match the layer to the problem

- **Prompt nudge.** Cheapest. Changes model behavior without new infrastructure. Good when the only problem is under-delegation.
- **Background delegation.** Good for research that would otherwise block the main thread. Needs durable artifacts and notification.
- **Pipeline or swarm framework.** Good for repeated multi-step jobs with a stable shape. Adds configuration and a new failure surface.
- **Durable workflow runtime.** Good for long-running work that must survive restarts and human approval. Highest setup cost.
- **MCP bridge.** Good when one runtime already has the orchestration you want and another runtime needs to call it.

Pick the lowest layer that removes the measured bottleneck. Moving up a layer without evidence adds maintenance for a benefit you cannot name.

## Anti-patterns

Do not fan out work that must share one writer, one browser profile, one GPU, or one config file. Do not parallelize a job whose workers will fight over the same disk. Do not use a swarm to avoid writing a clear task description; vague work becomes vague in parallel, faster.

## Verdicts

End with one of:

- adopt as is
- adapt or configure
- compose existing tools
- build the small missing piece
- keep the current setup

A menu of options is not a decision. The value of the analysis is the single recommendation and the evidence behind it.
