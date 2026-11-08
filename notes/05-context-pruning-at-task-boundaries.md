# Context pruning at task boundaries

Automatic compaction usually fires when the context is full, which is the worst time to decide what mattered. A better pattern lets the model compress at task boundaries, when it still knows which messages are finished.

## Compress on purpose

A compress tool exposed to the model can replace closed, stale content with a technical summary. Two modes are useful:

- **Range mode.** Compress a contiguous span into one or more summaries.
- **Message mode.** Compress individual messages independently for finer control.

Range mode is easier to reason about and produces better summaries. Message mode is useful when only a few large tool outputs are dead weight.

When a new compression overlaps an older one, nest the older summary inside the new one. Layered summaries preserve detail through repeated compression instead of diluting it away.

## Protect what cannot be reconstructed

Not all context is equal. Keep these verbatim or near-verbatim:

- subagent results
- skill instructions
- file contents that will be edited later
- user messages that contain the requirements

A generic summary of a subagent report loses the exact findings. A generic summary of a skill loses the procedure. Both are expensive to re-derive.

## Deduplicate repeated calls

Agents often run the same read or search more than once. Keep the most recent output for an identical tool call and drop the earlier copies. Recalculate the deduplication set when compression runs, so prompt caching is not invalidated on every turn.

## Purge errored inputs carefully

A failed tool call can carry a huge input: a log dump, a malformed query, a full file. After a few turns, the input is no longer useful. Drop the input, keep the error message. The model needs to know that the call failed and why; it rarely needs the payload.

## Watch the cache

Prompt caching rewards stable prefixes. Aggressive per-turn pruning breaks the cache and can cost more than it saves. Batch pruning with an explicit compression step and accept that the cache resets at that boundary.

## Do not over-prune

Compression is lossy. If the session is short, or the model has plenty of room, leave it alone. The goal is to keep the working set small enough to stay coherent, not to minimize tokens for its own sake. A session that keeps re-reading the same file because its summary was too thin has saved nothing.
