---
name: review-criteria
description: The checklist the reviewer agent applies to every diff, covering security and performance. Used by the reviewer agent during /review.
---

# Review criteria

## Security
- Injection: SQL, command, template, path traversal
- Auth/authz: missing checks, privilege escalation, broken object-level authorization
- Secrets: hardcoded keys/tokens, secrets logged or returned in responses
- Deserialization: untrusted input into pickle/yaml.load/eval-equivalents
- Input validation: missing bounds/type checks on external input

## Performance
- N+1 queries or repeated I/O in a loop
- Unbounded loops or recursion on user-controlled input
- Unnecessary allocations/copies in hot paths
- Algorithmic complexity worse than what the change needed (e.g. O(n²) where O(n log n) was available)

## Correctness / drift
- Does the diff match what the plan specified, file-for-file?
- Are there changes outside the plan's stated scope?
- Do existing tests still pass? Were tests added for new branches?

## Severity guide
- **Blocker**: ships a security hole or breaks correctness — FAIL, no exceptions.
- **Major**: real risk but not exploitable/breaking as written — reviewer's judgment on PASS/FAIL.
- **Minor**: style, missed edge case with low impact — note it, doesn't block.
