---
name: "code-simplicity"
description: "Use when designing, implementing, refactoring, or reviewing code for simplicity, complexity limits, interface restraint, and focused module boundaries. Applies across languages."
---

# Code Simplicity

Choose the simplest design that meets the requested behavior. Remove unnecessary code and process before adding abstractions. Preserve observable behavior unless the request or authoritative specification requires a change. Keep simplification within the task's scope.

Question requirements that come from the existing implementation. If the design is hard to explain plainly, clarify the requirements or simplify the design before proceeding.

Use idioms and standard APIs from the chosen language and ecosystem. When choosing a language or runtime, always prefer ahead-of-time compilation and avoid just-in-time compilation.

## Complexity and testing

Apply these limits to the code being changed using the repository's appropriate analysis tools:

| Metric | Requirement |
| --- | --- |
| Cyclomatic complexity | Below 22 |
| Cognitive complexity | Below 22 |
| Halstead Difficulty | Below 80 |
| Maintainability Index | At least 20 on the normalized 0-100 scale. Higher is better. |

No CRAP score threshold is defined. Do not invent one.

Report the analyzer, metric variant, and measurement scope when reporting scores. Apply function-level metrics to individual functions rather than hiding difficult functions behind aggregate averages. Do not compare raw Maintainability Index scores with the normalized threshold. If a metric cannot be measured with the available tooling, state that limitation instead of claiming compliance.

Keep functions small and focused. Prefer early returns over deep nesting. Reduce unnecessary branches and duplicated decisions. Do not split code into trivial helpers solely to improve scores.

Use `development-patterns:practical-testing` when adding, changing, reviewing, or removing tests. Keep tests beside the code where project conventions support it.

## Interfaces and abstractions

- Add an abstraction only when it simplifies the current system.
- Prefer concrete implementations until a shared contract serves a clear need.
- Define interfaces around consumer needs. Expose only the operations those consumers require.
- Avoid creating an interface for every implementation. A speculative future implementation does not justify a new interface.
- Prefer composition over inheritance.
- Prefer standard APIs and existing helpers before new abstractions or dependencies.
- Use explicit types for known data structures. Keep private implementation details out of public contracts.
- Prefer a shared codepath with simple conditions for minor workflow differences. Keep separate paths when their behavior or responsibilities differ enough that sharing would obscure them.

## Modules and boundaries

- Keep each module or package focused on one clear responsibility.
- Limit exported symbols. Keep implementation details private.
- Document each new module's responsibility using the repository's documentation conventions.
- Split modules when responsibilities, dependency direction, or public boundaries justify the split.
- Avoid modules that only add indirection. Keep closely related code together.
- Unify duplicated codepaths when doing so simplifies behavior and preserves the required boundaries.
- Avoid shared utility collections with unrelated responsibilities.

## Apply and verify

Define the outcome, scope, and hard constraints before acting. Limit discovery to what establishes the owning codepath, its consumers, and affected dependencies. Choose the smallest change that removes the complexity. Do not add atomicity, exactly-once behavior, crash recovery, or cross-store cleanup coordination unless the user explicitly requests that guarantee.

When delegating independent edits, give each agent exclusive ownership of its files or component.

For routine changes, review the final diff once for unnecessary interfaces, indirection, exports, module splits, and duplicated decisions. Run focused behavior checks and available complexity analysis. Keep checks for secrets, destructive changes, data loss, and production releases when applicable. Defer low-risk polish and redundant validation. Report the change, evidence, risks, deferrals, and any unmeasured limits. Finish once the requested outcome and applicable checks are verified.
