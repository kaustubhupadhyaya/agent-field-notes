# Why agents under-delegate

A common observation: a coding agent has a task or subagent tool and still does everything in the main thread. Sessions look busy, context grows, and quality drops on long jobs. The tool is present. The behavior is absent.

## Measure first

Do not infer from a few sessions. Count:

- total tool calls
- task or subagent calls
- root sessions versus child sessions
- the agent and model behind each call

Most session stores expose this. Query the session database or parse the transcript files. A baseline turns a feeling ("it never delegates") into a number.

A useful baseline shape:

```
root sessions: N
tool calls:     N
task calls:     N
child sessions: N
```

If task calls are near zero, the question changes from "is delegation broken?" to "what discourages it?"

## Look for the built-in bias

In one setup, nothing blocked delegation. Permissions allowed it, plugins did not touch the tool, and a few successful calls existed. The strongest cause was the tool description itself: it opened with a section on when not to use the tool, written to prevent runaway fan-out. Models read that as a default preference for working alone.

Prompt-level policy is the fix. Inject a short delegation policy into the system prompt and append a counterweight to the tool description. Keep the policy harness-neutral so the same file can serve more than one runtime.

Two surfaces are worth using:

1. System prompt transformation. Insert a high-priority block that says when to delegate and what to delegate.
2. Tool description augmentation. Append one line that names delegation as the preferred path for research, reading, and verification.

The policy should be short. Long policy blocks get ignored or crowd out the task.

## Scoping hooks is the hard part

A hook that injects on every message will also inject into child sessions. Child sessions should be focused workers, not orchestrators. Scope the injection to root sessions.

One runtime passed `agent: null` to hooks even though the type allowed a name. Name-based scoping silently failed. The reliable signal was the session event stream: every child session reports a parent id. Track created and updated sessions, keep the child ids in a set, and skip injection for those ids.

When a runtime's convenience field is unreliable, use the event that owns the relationship.

## Make hooks best-effort

Hooks sit in the hot path of every request. A thrown error can break a session. Wrap file reads and parsing in try/catch, fall back to an inline policy, and log a single line on load. Missing config should degrade, not crash.

## Verify behavior, not installation

Two checks matter:

- Does the text actually reach the model?
- Does delegation frequency move?

For the first, use a codeword test (see note 02). For the second, re-run the counter after enough new sessions. Installing a plugin proves that a file exists. It proves nothing about behavior.

## When not to delegate

Delegation costs a handoff. Keep work in the main thread when it is small, when it is a single write that needs continuity, or when the subtask cannot be described without the full context. The point is to move independent research, reading, and verification out of the main context, not to turn every action into a subagent.
