# chatgpt-skills

A dedicated repository for reusable ChatGPT Skills.

This repo stores skill source files in a clean, versionable structure so each skill can be reviewed, improved, and published independently.

## Quick navigation

- [Current skills](#current-skills)
- [Repository layout](#repository-layout)
- [How to use this repo](#how-to-use-this-repo)
- [Planned growth](#planned-growth)

## Current skills

| Skill | Status | Best for | Path |
|---|---|---|---|
| `product-delivery-autopilot` | active | turning ambiguous multi-step work into a user-ready deliverable with acceptance, QA, and release gates | [`product-delivery-autopilot/`](./product-delivery-autopilot/) |
| `spacekeeper-reference` | v0.1 | stable 2D spatial memory for AI image keyframes across cameras and agents | [`spacekeeper-reference/`](./spacekeeper-reference/) |

### product-delivery-autopilot

Autonomous product delivery execution for tasks that should end in a user-ready deliverable rather than a rough draft.

Highlights:
- delivery-oriented execution instead of partial progress reporting
- internal multi-role review lanes: maker, product-owner, qa, releaser
- explicit acceptance gates and release-readiness checks
- regression-aware repair loop before declaring completion

Core files:
- [`SKILL.md`](./product-delivery-autopilot/SKILL.md)
- [`agents/openai.yaml`](./product-delivery-autopilot/agents/openai.yaml)
- [`references/`](./product-delivery-autopilot/references/)

### spacekeeper-reference

Lightweight, agent-agnostic spatial continuity rules for AI image keyframe references. Records actors, props, landmarks and camera viewpoints in a common 2D scene JSON. Agents are free to implement visualization and prompt generation however they prefer; cross-agent handoff uses a stable JSON schema.

Core files:
- [`SKILL.md`](./spacekeeper-reference/SKILL.md)
- [`spec/CONTRACT.md`](./spacekeeper-reference/spec/CONTRACT.md)
- [`spec/scene.schema.json`](./spacekeeper-reference/spec/scene.schema.json)
- [`examples/`](./spacekeeper-reference/examples/)
- [`tests/ACCEPTANCE.md`](./spacekeeper-reference/tests/ACCEPTANCE.md)

## Repository layout

Each skill lives in its own top-level directory.

```text
chatgpt-skills/
  product-delivery-autopilot/
    SKILL.md
    agents/
    references/
```

Typical skill contents:

- `SKILL.md`: the skill entrypoint and core behavior
- `agents/openai.yaml`: UI metadata for the skill
- `references/`: supporting guidance loaded when needed
- `scripts/`: optional helper code for deterministic tasks
- `assets/`: optional templates or non-context assets

## How to use this repo

When adding or updating a skill:

1. create or edit the skill directory directly
2. keep `SKILL.md` focused on behavior and trigger conditions
3. move heavier detail into `references/`
4. validate and package before external upload when needed
5. keep each skill independent so it can evolve without affecting others

## Planned growth

This repository is intended to grow into a small skill library. Likely future sibling directories include:

- `validated-autopilot/`
- `unattended-operator/`
- other task-specific execution skills

## Status

This repository is initialized and now serves as the dedicated home for ChatGPT Skills.
