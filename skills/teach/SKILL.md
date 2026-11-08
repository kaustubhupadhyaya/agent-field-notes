---
name: teach
description: Teach a topic so it is understood rather than memorized. Use whenever explaining something, from a one-line answer to a deep lesson.
---

# Teach

The goal is understanding: the learner can derive the fact from foundations they already accept, connect it to what they know, and keep it without rehearsal. Memorized facts decay. Understood facts do not.

## Two principles

### 1. Start from unconditional truths

Begin with facts the learner can accept at face value, with no caveats. They are safe to commit to because nothing more fundamental will later contradict them.

- Prefer simple statements over nuanced ones. If a statement needs "usually" or "it depends", dig deeper.
- Use real definitions when a domain has one. A list of typical properties is not a definition.
- Confirm the foundation reads as obviously true before building on it.
- Keep "axiom" for facts that genuinely follow from nothing else. Many unconditional truths derive from deeper facts; they still do not need that derivation to be accepted.

### 2. Show how the learner could have discovered it

Facts feel arbitrary when no path leads to them. Walk the discovery path:

- Why are we trying to solve this at all?
- Why reach for this idea, formula, or step?
- What would make someone try this next?

Every step should feel motivated. Nothing should appear from nowhere.

Use Socratic questioning when the learner can plausibly reason to the answer. Narrate the path when the topic is beyond cold reasoning or the learner wants delivery. When a Socratic question has a definite answer, grade it. Reserve open questions for preferences and direction.

## The session shape

Run all three phases. Scale their size to the topic, never their shape.

### Phase 1: probe

Find two things.

**Current level.** Locate the edge of what the learner knows along every strand the lesson will use. The edge is bracketed only when you have both a question they answer correctly and a question they miss. All-correct means the questions were too easy; escalate. One miss is one coordinate; probe around it to see whether it is a slip, a narrow gap, or a misconception.

**Goal.** Ask what they actually want to understand. A broad subject can mean ten different lessons. Make the target concrete. This is a preference question, not a graded one.

### Phase 2: plan

Design the lesson before teaching it.

- Ground the content in canonical textbooks, not research papers. Textbooks build foundations in a proven order.
- Use the standard terminology and definitions from those books, and cite them.
- Identify the unconditional truths the lesson rests on.
- Mark which of those the learner already holds.
- Choose the discovery path from those truths to the goal.
- Decide where to question and where to narrate.

Present the plan in two parts: a short prose description of the approach, then a small dependency graph with roots at the bottom of the reasoning and the goal as the sink. Stress-test the roots before showing it. If a root is itself derived, push it down.

Stop and wait for approval. A wrong root is cheap to fix at this stage and expensive mid-lesson.

### Phase 3: teach

Build the graph one node at a time. For every node, including foundations:

1. **Motivate.** Say why this node is needed now.
2. **Establish.** State the unconditional truth plainly, or build the derived step from what is already held.
3. **Connect.** Make the dependency edge explicit.
4. **Check.** Ask a question that confirms the node landed. If it did not, fix it before continuing.

Do not front-load all foundations and then stop checking. A new foundation that appears mid-session gets the same four steps.

## Accuracy

Verify uncertain claims with a research subagent before stating them. Names, dates, formulas, definitions, and attributions are all candidates for invention. Pausing to check is always acceptable. If a check changes what you were about to teach, say so plainly.

## Writing quiz options

Build the options so evenness is automatic:

1. Every option is a bare claim. Put all reasoning in the explanation, which appears after the answer.
2. Write the correct claim first, then mutate it into each distractor using a real misconception. Keep the same sentence shape, grain, and register.
3. Each distractor must be wrong on the intended reading but tempting to someone who holds that misconception.
4. Do not bold the key term in one option only. Bold nothing, or bold the parallel term everywhere.

Read the finished set cold. If you can identify the answer without knowing the material, regenerate the set.

## Formatting

Write math in LaTeX when the renderer supports it: inline `$f(x)$`, display on its own lines with `$$`. Prefer notation over plain-text approximations.
