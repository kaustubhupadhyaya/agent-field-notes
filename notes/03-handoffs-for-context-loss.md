# Handoffs for context loss

A handoff is written for the next agent, which starts with none of your context. It compresses the session into what the next agent needs, and keeps an audit trail of the decisions.

## What a handoff must carry

A structure that works:

1. **Intent.** The original request in the user's words, plus what was implied.
2. **Constraints.** Rules in force, including ones that are easy to violate by accident.
3. **Technical state.** The concepts, versions, APIs, and quirks the next agent needs to avoid rediscovering.
4. **Files.** What was created, modified, read-only, or deliberately left alone, and why.
5. **Errors and fixes.** The failure, the root cause, the fix, and whether the user was told.
6. **Solved and open.** Separate the two. An open item without an owner is how work disappears.
7. **Pending tasks.** Exact next actions, including commands when safe.
8. **Current work.** The last few actions, so the next agent knows where the cursor sits.

The order matters less than the completeness. A handoff that omits a declined option will cause the next agent to propose it again. A handoff that omits an unverified claim will turn it into a fact.

## Record what was not reported

Agents often finish work and summarize only the happy path. Write down the details the user has not seen:

- a probe bug that sent debugging in the wrong direction
- a timeout that was worked around rather than fixed
- a decision that was reversed
- a limitation that will bite later

This is the part that keeps the next session honest. It is also the part most likely to be skipped.

## Keep transcripts out

Do not attach a raw session transcript as the handoff. Transcripts are large, repetitive, and full of data that should not travel: names, paths, account labels, tokens, private project details. They also bury the decisions.

If a transcript is needed for local debugging, keep it local and temporary. The handoff is the durable artifact.

## Write for a reader who cannot ask questions

The next agent cannot interrupt you. Define terms on first use, name the file and the symbol, and state the assumption behind each recommendation. "Use the second approach" is useless without the reason and the rejected alternative.

## End with the next move

A handoff that ends in a summary invites re-analysis. A handoff that ends with "run this check, then decide X" lets the next session continue immediately. Include the command, the expected output, and what to do if it differs.

## Keep one canonical handoff

Parallel sessions can produce parallel handoffs. Two documents that both claim to be current will disagree. Keep one canonical file, and make the others point to it or mark them superseded. The cost of merging is lower than the cost of acting on the wrong one.
