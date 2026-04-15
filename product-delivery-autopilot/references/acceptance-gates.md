# Acceptance gates

Use these gates before calling a phase complete.

## Gate 1: deliverable identity
The artifact matches the requested type.
Examples:
- plan is actually a plan, not a brainstorm
- implementation is actually implemented, not only described
- summary is actually audience-appropriate and decision-useful

## Gate 2: scope fit
The result covers the needed scope without drifting into unrelated work.

## Gate 3: usability
Another person could use, review, or act on the result without reconstructing missing context.

## Gate 4: evidence
There is a concrete basis for correctness or fitness.
Examples:
- direct inspection
- test output
- consistency checks
- requirement matching
- source verification

## Gate 5: defect posture
No unresolved material flaw is known for the current phase.
Minor cosmetic issues may remain only if they do not change usability or release safety.

## Gate 6: handoff clarity
The current state is legible.
The user can see what is done, what was checked, what still risks failure, and what the next move is.

## Rule

Do not say “done” or “ready” if any gate materially fails.
Say which gate failed, patch it, and rerun the narrowest sufficient review.
