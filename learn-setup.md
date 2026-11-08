# Learning setup: teach and visualize

This is a small setup for using an agent to build understanding rather than hand back answers. It pairs a teaching skill with a visualization skill and two maker subagents. The method comes from the public video [How I Use AI to Learn Things](https://www.youtube.com/watch?v=kzcI5F4tGiU) and the public project it describes at [github.com/amosblomqvist/learn](https://github.com/amosblomqvist/learn). The versions here are rewritten and sanitized. They are not copies of the upstream files, and they carry no personal data, local paths, or configuration secrets.

## The idea

Two learners can answer the same questions and still differ. One holds a pile of disconnected facts. The other holds a few core truths from which the facts follow. The second kind of knowledge survives, compresses, and transfers. The setup aims at the second kind.

The felt moment is the click: a set of separate facts collapses into a few generating ideas. A lesson that produces recitation has missed the point.

## The loop

1. **Probe.** Find the edge of what the learner already knows, then find what they want to understand.
2. **Plan.** Choose the smallest dependency graph that reaches the goal, with unconditional truths at the roots. Show the plan before teaching.
3. **Teach.** Build the graph one node at a time. Motivate the node, establish it, connect it to what is already held, and check it with a question.

Accuracy outranks flow. If a fact, date, formula, or definition is uncertain, verify it with a research subagent before saying it. A confident error at the root corrupts everything built on top.

## The teach skill

[skills/teach/SKILL.md](skills/teach/SKILL.md) encodes the process:

- start from unconditional truths that can be accepted without caveats
- explain how the learner could have discovered each step, so nothing feels decreed
- use Socratic questions when the learner can reason to the answer, and narration when the topic is out of reach or energy is low
- write quiz options so the correct answer is not identifiable by length, justification, or bolding
- verify claims with a research subagent when uncertain
- keep math in LaTeX when the note renderer supports it

The skill is written for a generic learner. Change the register, the pacing, and the examples to fit the person using it.

## The visualize skill

[skills/visualize/SKILL.md](skills/visualize/SKILL.md) adds one diagram when a picture carries something prose cannot: structure, direction, sequence, geometry, or containment.

The rule is one idea and the fewest elements that carry it. A maker subagent authors the source, renders it, looks at the image, and iterates until it is correct. Structural ideas go to a Mermaid maker. Spatial and geometric ideas go to an SVG maker. If the maker cannot produce a correct picture, the lesson goes without one. A false diagram is worse than no diagram.

## A minimal setup

You need:

- an agent runtime that can load skills
- two subagent definitions, one for research and one for each visual maker
- a folder for rendered images
- a markdown log or notebook the agent can write to

The upstream project uses a specific runtime's extension system. The skills are the portable part. The quiz, question popup, and markdown logging extensions are conveniences. Replace them with whatever your runtime offers, or run the loop in chat.

## What was sanitized

- Personal names and pronouns were removed.
- Machine paths, runtime versions, and plugin configuration were removed.
- Examples tied to private projects were replaced with generic ones.
- The skill bodies were rewritten rather than copied, because the upstream repository does not declare a license.
- No session data, credentials, or account labels are included.

## Attribution

Method, video, and original configuration: [How I Use AI to Learn Things](https://www.youtube.com/watch?v=kzcI5F4tGiU) and [amosblomqvist/learn](https://github.com/amosblomqvist/learn). This adaptation is offered under CC BY 4.0.
