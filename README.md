# chatgpt-skills

A dedicated repository for reusable ChatGPT Skills.

This repo stores skill source files in a clean, versionable structure so each skill can be reviewed, improved, and published independently.

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

## Current skills

### product-delivery-autopilot

Autonomous product delivery execution for tasks that should end in a user-ready deliverable rather than a rough draft.

Highlights:
- delivery-oriented execution instead of partial progress reporting
- internal multi-role review lanes: maker, product-owner, qa, releaser
- explicit acceptance gates and release-readiness checks
- regression-aware repair loop before declaring completion

Path:
- `product-delivery-autopilot/`

## How this repo is intended to grow

Future skills can be added as sibling directories, for example:

- `validated-autopilot/`
- `unattended-operator/`
- `product-delivery-autopilot/`

## Maintenance notes

When updating a skill:

1. edit the skill directory directly
2. keep `SKILL.md` concise and focused
3. move longer detail into `references/`
4. package and validate the skill before external upload when needed

## Status

This repository is now initialized as the dedicated home for ChatGPT Skills.
