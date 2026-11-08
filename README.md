# Agent field notes

Practical notes on building and running AI coding agents: delegation, orchestration, research workflows, handoffs, and the small pieces of infrastructure that keep multi-agent work from falling apart.

These notes are distilled from private working sessions. Each one is rewritten as a general lesson. No transcripts, session identifiers, local paths, employer or client details, or project-specific data are included.

## Notes

| # | Note | Topic |
|---|------|-------|
| 01 | [Why agents under-delegate](notes/01-why-agents-under-delegate.md) | Measuring delegation and making it a policy |
| 02 | [Test prompt injection with codewords](notes/02-test-prompt-injection-with-codewords.md) | Verification that does not lie to you |
| 03 | [Handoffs for context loss](notes/03-handoffs-for-context-loss.md) | Compression with an audit trail |
| 04 | [Background delegation and compaction](notes/04-background-delegation-and-compaction.md) | Durable async work |
| 05 | [Context pruning at task boundaries](notes/05-context-pruning-at-task-boundaries.md) | What to compress and what to protect |
| 06 | [One todo index across agents](notes/06-one-todo-index-across-agents.md) | Cross-harness task capture |
| 07 | [Skill drift across harnesses](notes/07-skill-drift-across-harnesses.md) | One canonical copy or silent rot |
| 08 | [Choosing swarm tooling](notes/08-choosing-swarm-tooling.md) | Fit before features |
| 09 | [Scrutinize before you build](notes/09-scrutinize-before-you-build.md) | Goal, ask, and prior art |

## Learning setup

[learn-setup.md](learn-setup.md) describes a small teaching and visualization setup for agent runtimes: the method, the two skills, and what to adapt. It accompanies the public video [How I Use AI to Learn Things](https://www.youtube.com/watch?v=kzcI5F4tGiU).

## Who these are for

People building agent tooling for themselves or a small team. The notes assume comfort with a terminal, plugin hooks, session stores, and the idea that prompts are part of the system design.

## What is deliberately absent

- Raw session transcripts.
- Names, email addresses, account labels, and company names.
- Absolute paths and machine-specific setup.
- Private project names and business context.
- Credentials, tokens, and configuration secrets.

## License

Text is licensed under [Creative Commons Attribution 4.0 International](LICENSE). Code snippets may be used under the same terms. Attribution: `agent-field-notes`, https://github.com/kaustubhupadhyaya/agent-field-notes.
