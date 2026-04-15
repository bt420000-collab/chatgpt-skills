# Recovery patterns

Treat failures as normal delivery work.
Patch, re-evaluate, and continue.

## Pattern 1: build failed
Action:
- inspect the concrete failure
- identify the most likely cause
- apply the smallest strong fix
- rerun the failed step
- rerun one adjacent regression check if the fix was material

## Pattern 2: output exists but is weak
Action:
- identify whether the weakness is scope, clarity, correctness, or usability
- patch the narrowest high-impact weakness first
- rerun product-owner and releaser lanes

## Pattern 3: validation failed
Action:
- identify which acceptance gate failed
- patch specifically for that gate
- rerun the narrowest sufficient review instead of restarting everything

## Pattern 4: regression risk introduced
Action:
- identify what previously passing area may have been destabilized
- run a targeted regression check there
- do not mark ready until the check passes or the risk is explicitly escalated

## Pattern 5: progress stalled
Action:
- reduce the task to the next smallest deliverable checkpoint
- produce a viable artifact there
- rebuild momentum from a smaller validated base

## Rule

Never treat “first pass exists” as a recovery endpoint.
Recovery ends only when the material flaw is patched and the relevant validation path passes.
