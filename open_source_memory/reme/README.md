# ReMe: beginner-to-production guide

The [experiment notebook](./experiment.ipynb) tests reuse of successful task experience. Follow the current ReMe documentation for framework compatibility and exact APIs.

## 1. Beginner: reusable experience

Reusable memory captures what worked on a task so an agent can use it again. It should be a helpful precedent, not a command to repeat blindly. Store the task context, procedure, result, and constraints that affect whether reuse is appropriate.

## 2. Intermediate: retrieve and adapt

- Save successful and failed experience with evidence and task labels.
- Retrieve only when the current task is similar.
- Compare constraints before reusing a procedure.
- Let the agent adapt to new inputs, and expose uncertainty when a precedent does not fit.
- Avoid storing transient secrets or user data in reusable global memory.

## 3. Advanced and production

- Separate private user memory from shared team/task experience.
- Enforce authorization and data redaction before any experience is shared.
- Version experience records and track provenance, outcome, and applicability.
- Validate agent-generated lessons before making them broadly reusable.
- Apply retention/deletion and support removal of unsafe or obsolete procedures.
- Restrict tools and require approval for consequential actions; memory must not grant authority.
- Monitor reuse success, negative transfer, stale procedures, retrieval quality, latency, and cost.

## 4. Evaluation

Test a similar task with a changed constraint, an unrelated task, a failed historical attempt, and sensitive content. Measure whether the right experience is recalled, adapted, and attributed correctly.

## 5. Common pitfalls

Do not equate task similarity with identical requirements. Avoid global sharing of unreviewed agent experiences. The notebook is an evaluation plan, not a direct ReMe runtime integration.
