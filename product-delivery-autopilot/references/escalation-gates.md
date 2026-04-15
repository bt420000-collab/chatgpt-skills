# Escalation gates

Continuation is the default.
Escalation is the exception.

Do not escalate because a step is annoying, ambiguous, or failed once.
Escalate only when the next move crosses a real delivery boundary.

## Continue without escalation

Keep going when the issue is one of these:
- ordinary implementation choice
- ordinary writing or structuring choice
- routine debugging
- missing non-critical preference
- weak first pass that can be revised
- validation failure that can be patched and rerun
- plan resequencing within current constraints
- conservative reversible assumption is available
- a narrower fallback path still advances the deliverable

## Escalate immediately

Stop and surface the blocker when any of these are true:

### 1. external irreversibility
Examples:
- sending a message to a real recipient
- publishing, deleting, or overwriting live content
- destructive production changes
- final submission to an external authority

### 2. real financial commitment
Examples:
- making a purchase
- authorizing payment
- committing budget
- accepting billable external changes

### 3. missing access or credentials
Examples:
- login required and unavailable
- permission denied on the required system
- secret, token, or account access missing

### 4. live-user or live-system risk
Examples:
- destructive production configuration changes
- irreversible changes to real customer data
- pushing unvalidated automation into a live workflow

### 5. deliverable cannot be determined
Examples:
- two materially different outputs are equally plausible
- the required artifact is undefined
- acceptance criteria cannot be inferred

### 6. user constraints conflict
Examples:
- must use current facts but browsing is forbidden
- must not change files but must implement the file change
- must be exact but required source is inaccessible

### 7. validation is impossible without user-only knowledge
Examples:
- readiness depends on a private preference only the user can resolve
- correctness depends on unavailable ground truth
- release depends on an unstated subjective taste decision

### 8. high-stakes domains beyond safe bounded assistance
Examples:
- legal judgment
- medical judgment
- irreversible safety-critical instructions

## Escalation format

When escalation is necessary, provide exactly:
1. blocker
2. what was attempted
3. why autonomous continuation is unsafe or invalid
4. best current recommendation
