# Delivery lanes

Use this file to decide whether an artifact is merely built or actually fit for delivery.

## Principle

A fast build is necessary but insufficient.
A deliverable passes only when product fit, defect risk, and release judgment all support it.

## Lane 1: maker

Goal:
- reach a viable working artifact fast
- avoid over-design before a usable checkpoint exists

Questions:
- what is the shortest path to something testable
- what must exist before deeper review is meaningful
- what can be postponed without harming deliverability

Failure mode to avoid:
- polishing before a viable artifact exists

## Lane 2: product-owner

Goal:
- judge whether the artifact solves the right problem for the intended user or audience

Questions:
- does this match the requested deliverable
- is the scope right, not merely adjacent
- is the artifact usable by the intended audience
- are acceptance criteria actually satisfied
- would a stakeholder call this ready for review

Failure mode to avoid:
- accepting something because it looks complete while it misses the real job-to-be-done

## Lane 3: qa

Goal:
- identify likely defects, regressions, brittleness, and edge-case failures

Questions:
- what is most likely to break in real use
- what changed that could have introduced regressions
- what assumptions remain untested
- is the output internally consistent
- what simple stress check would expose a weakness fastest

Failure mode to avoid:
- claiming quality without trying to break the artifact

## Lane 4: releaser

Goal:
- make the bounded go, revise, or escalate decision for the current phase

Allowed decisions:
- go: fit to advance or hand off for the current phase
- revise: material issues remain and must be patched first
- escalate: a real boundary prevents valid continuation

Questions:
- is the current risk acceptable for this phase
- are the remaining issues cosmetic, material, or blocking
- is the evidence strong enough to describe this as ready
- would release now create avoidable rework or user confusion

Failure mode to avoid:
- releasing because momentum feels good

## Pass rule

A phase passes only when:
- maker produced a viable artifact
- product-owner found no unresolved acceptance gap
- qa found no unresolved material defect or regression risk
- releaser marks go

If any lane finds a material issue, patch it and rerun the narrowest sufficient review.
