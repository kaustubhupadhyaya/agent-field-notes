# Background delegation and compaction

Synchronous subagents solve context pollution but block the main thread. Background delegation solves the blocking. It adds a new problem: the result must survive the session that asked for it.

## The loop

1. Delegate a bounded task with a clear deliverable.
2. Continue working in the main session.
3. Receive a notification when the delegation reaches a terminal state.
4. Read the persisted result by id.

The "waiter model" is the right mental picture. You do not follow the waiter into the kitchen. You keep talking and the order arrives.

## Persist before you notify

The critical ordering rule: write the result to disk before delivering the terminal notification. If the process dies between the two, a persisted result can still be read. A notification without a result is a dangling reference.

Each delegation should have:

- a stable id reused across state, artifact path, notifications, and retrieval
- explicit states: registered, running, terminal
- terminal-state protection, so a late progress event cannot move a finished job back to running
- a deterministic read that returns the terminal record even after a restart

## Carry context through compaction

Compaction is the moment background work pays off or disappears. When the main session is summarized, running and unread completed delegations must be carried forward with retrieval hints. Otherwise the model forgets that it asked for work and never reads the answer.

Store the id and a one-line summary in the compaction payload. The full result stays on disk. The hint is enough to recover it.

## The read-only restriction is not arbitrary

Background delegations often run outside the host session tree. The host's undo and branching system cannot see changes made in those sessions. A revert would leave the background writes in place, which is a data-loss surprise.

Until the runtime can track those writes, restrict background delegation to read-only agents: no edits, no writes, no shell that can mutate files. Write-capable work goes through the native task tool, where the runtime can follow it.

## Timeouts are part of the contract

A background job that never ends is worse than a failed one, because it holds attention and never resolves. Use a hard timeout, return a clear terminal state, and keep any partial artifact. Fifteen minutes is a reasonable default for research and reading tasks.

## Design lesson

Durability beats cleverness. A simple file per delegation, a stable id, and a notification after the write will outperform an elaborate in-memory graph that loses work when the context is compacted.
