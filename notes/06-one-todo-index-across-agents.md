# One todo index across agents

When several agent runtimes are in use, work scatters. Each has its own session list, its own naming, and its own idea of what is open. A single index fixes the visibility problem, but only if capture is automatic in every runtime.

## One store, several writers

Use one JSON store with a small schema:

```json
{
  "id": "...",
  "summary": "...",
  "status": "open",
  "source": "runtime-name",
  "project": "...",
  "sessionId": "...",
  "createdAt": "..."
}
```

Every runtime writes through the same CLI or library. Keep ids stable and avoid rewriting the whole file from multiple processes without a lock or an atomic replace.

## Capture per runtime

Each harness has a different extension point:

- A hook that runs at session start and on prompt submit.
- A plugin that listens to todo updates and session creation.
- A skill that instructs the model to record commitments.

Instruction-only capture is the weakest link. A model can forget. Prefer an event-driven path and keep the instruction as a backstop.

## Index from the source of truth

Do not ask each agent to remember its own tasks. Parse what the runtime already stores:

- JSONL transcripts for one tool
- a SQLite database for another
- a native todo table for a third

Read-only indexing is safer than asking the agent to write twice. Run the indexer at session start, cache by file modification time, and provide a force flag when a manual refresh is needed.

## Name sessions by meaning

Raw session ids are unusable in a list. Derive a label from the first meaningful user message, or from the metadata a subagent already carries. Show the label, the runtime, and a resume command.

A resume command turns the index from a reminder list into a launcher:

- one runtime resumes a parent session by id
- a subagent resumes through its parent, because sidechains are not directly resumable
- another runtime exposes a session flag

Store the command, not just the id.

## Normalize status without fighting the user

Map native statuses conservatively:

- pending and in progress become open
- completed becomes done

Never reopen an item a user marked done manually. Never turn a dismissed item back into an open one. The index is a convenience; the user's explicit action wins.

## Keep the live copy live

Plugins often run from a cache, not from the checkout you edited. A change to the source directory can have no effect until it is synced to the running copy. Check where the process actually loads from, sync deliberately, and restart the server if the runtime caches modules at startup.

This single mistake, editing the wrong copy, wastes more time than any schema decision.
