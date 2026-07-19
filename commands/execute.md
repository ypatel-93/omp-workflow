---
description: Execute a plan produced by /plan
---
Use the `executor` subagent to implement the plan at `.omp/plans/$@.md`. Follow each step exactly; flag anything ambiguous instead of improvising.

<!--
Model-by-complexity note: this template currently always uses the executor
agent's default model (Sonnet 5). If you want trivial-tagged steps to run on
a lighter model, read the complexity tags out of the plan file before this
line and pass an explicit model override when spawning the agent — check
your installed OMP fork's docs (`omp agents --help` or `/agents`) for the
exact override flag/argument, since it varies between forks.
-->
