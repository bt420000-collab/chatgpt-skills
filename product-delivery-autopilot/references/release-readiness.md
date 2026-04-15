# Release readiness

Release readiness is phase-specific.
The question is not whether the artifact is perfect.
The question is whether it is safe and useful enough to release for the current phase.

## Ready for internal review
Use when:
- the artifact is coherent
- the main acceptance criteria are met
- known risks are visible
- remaining defects are non-blocking for review

## Ready for operational use
Use when:
- acceptance criteria are met
- basic regression risk has been checked
- instructions or structure are clear enough for real use
- no unresolved material flaw is known

## Not ready
This applies when any of the following is true:
- the output still misses the actual target
- a core edge case is likely to fail
- the latest patch could have broken a previously passing area and has not been rechecked
- correctness is mostly assumed rather than evidenced
- the user would need to repair the artifact before using it

## Release phrasing

When marking go, explicitly state:
- what level of readiness was reached
- what was validated
- what risks remain

Good example:
- Ready for operational use in the current phase. Acceptance checks passed, targeted regression passed, remaining risk is limited to optional polish.

Bad example:
- Looks good to me.
