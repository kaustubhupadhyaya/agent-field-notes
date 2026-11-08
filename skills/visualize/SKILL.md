---
name: visualize
description: Add one correct, minimal diagram to a lesson when a picture carries structure or geometry better than prose. Delegates authoring and visual verification to a maker subagent.
---

# Visualize

A picture earns its place when it shows something words cannot: shape, structure, direction, relationship, or geometry. This skill produces one such picture, verifies it by looking at the rendered output, and embeds it in the lesson.

The main agent is the creative director. It decides the idea and reduces it to the fewest carrying elements. A maker subagent authors, renders, inspects, and saves the image, then returns a filename. The main agent embeds that filename.

## When to visualize

Use a visual when the idea is:

- a structure or relationship: dependencies, a system with parts and arrows, a pipeline, a sequence, a state machine, a tree, a comparison, containment
- spatial or geometric: coordinates, a number line, vectors, a function's shape, a physical layout

Do not visualize when prose or one equation already carries the idea. A decorative diagram that restates the sentence adds noise and a chance to be wrong. A missing visual is cheaper than a false one.

## Choose the maker

- **Mermaid maker.** Structural and relational visuals: dependency graphs, flowcharts, sequence and state diagrams, trees, timelines.
- **SVG maker.** Spatial and geometric visuals that Mermaid cannot lay out: exact coordinates, geometry figures, number lines, vectors, plots, custom shapes.

Rule of thumb: nodes and edges go to the Mermaid maker. Positions and shapes go to the SVG maker.

## Brief the maker

The common failure is cramming. Every extra label makes the picture harder to read and easier to get wrong. Before briefing, delete every element whose absence still leaves the idea clear.

Give the concept and the concrete elements, not a vague topic and not a long checklist.

Bad: "make a diagram about how TCP works."

Good: "Top node: packet. Arrows down to ordering and retransmit-on-loss. Both arrows feed into reliable stream. No title. Show that reliability is built from packets, not placed beside them."

Keep the brief under roughly five to seven elements. If it is longer, cut it first.

## Invoke

Dispatch the appropriate maker with a self-contained brief. The maker owns its authoring and rendering tools. It authors the source, renders a PNG, looks at the PNG, iterates until the image is correct and clean, saves it with a unique filename, and returns:

```
RESULT:
filename: viz-<slug>-<timestamp>.png
path: <path>
```

If it returns `RESULT: NONE`, it could not make a correct picture. Simplify the brief, choose the other maker, or skip the visual. Never hand-author or fake a diagram yourself. Correctness depends on the render-and-inspect loop.

## Embed

Embed the returned filename in the lesson using the renderer's image syntax. In an Obsidian-style markdown log:

```
![[viz-<slug>-<timestamp>.png|500]]
```

Introduce the visual in one sentence, then let it carry the idea. Do not narrate every element back in prose.

## Why this is reliable

- The maker never returns an image it has not looked at, so a render that is clean but wrong is caught before the learner sees it.
- A PNG embed means what the maker verified is what the learner sees. No re-render drift.
- Unique filenames keep by-name embed resolution unambiguous.

## What to adapt

The maker definitions depend on the runtime's subagent and rendering setup. Replace the tool names and the render commands with your own. Keep the loop: brief narrowly, render, inspect, iterate, return a filename only when the image is correct.
