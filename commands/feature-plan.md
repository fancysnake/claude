# Feature Plan

Analyze the codebase relevant to this feature and produce an implementation plan.

The feature to build: $ARGUMENTS

## Steps

1. Explore the relevant parts of the codebase — existing structure, patterns, conventions, and anything that will be touched by this feature
2. Produce a numbered implementation plan where:
   - Each step delivers a **small, independently testable slice** of functionality
   - Steps build incrementally (no big bang steps)
   - Each step ends with a concrete description of **what the user can manually test** to verify it works
3. Save the plan to `FEATURE_PLAN.md` in the project root with this format:

```markdown
# Feature: <name>

## Steps

- [ ] 1. <description> — _Test: <what to manually verify>_
- [ ] 2. <description> — _Test: <what to manually verify>_
...
```
4. Review the plan with `/gloria`
5. Review the plan with `/tessa`
6. Review the plan with `/hector`
7. Print the plan and ask: *"Does this plan look good? Any changes before we start?"*
8. If the user requests changes, update both the output and `FEATURE_PLAN.md` before finalizing

Do not write any implementation code. Planning only.
