---
name: plan-format
description: The structure a plan must follow. Used by the planner agent when writing a plan, and by the executor and reviewer agents when reading one.
---

# Plan format

Every plan is a markdown file with this structure:

```
# <task title>

## Context
<1-3 sentences. Link to wiki pages instead of restating them.>

## Steps
1. **<file path>** — `<function/class name>`
   - Change: <what changes and why, one or two sentences>
   - Acceptance: <how to verify this step is done correctly>
   - Complexity: trivial | moderate | complex

2. **<file path>** — `<function/class name>`
   - ...

## Out of scope
<anything explicitly not covered, so the executor doesn't scope-creep>
```

## Rules
- One numbered step per logical change, not per file — a step can touch multiple files if it's one coherent change.
- Complexity tags drive model selection at execution time: trivial/moderate → a lighter model is fine, complex → full-capability model.
- No prose padding. If a step needs more than 3 sentences to explain, the plan is either too coarse-grained or hiding complexity that should be its own step.
- Reference wiki pages by URL instead of copying their content into the plan.
