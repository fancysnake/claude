# Feature Step

Work through one step of the current feature plan using a TDD workflow.

If $ARGUMENTS is provided, use it as the step number or description to work on.
If $ARGUMENTS is empty, read `FEATURE_PLAN.md` and work on the **first unchecked step**.

---

## Before Starting

Read `FEATURE_PLAN.md`. Identify:
- Which step you are working on
- How many steps remain after this one
- The manual test instruction for this step

If `FEATURE_PLAN.md` does not exist, tell the user to run `/feature-plan <description>` first.

---

## TDD Loop

1. Write a failing test that covers the behavior this step should deliver
2. Run the test — confirm it fails (red)
3. Implement the minimum code to make the test pass
4. Run the test again — confirm it passes (green)
5. Refactor if needed, keeping tests green
6. Mark the step as complete in `FEATURE_PLAN.md` by changing `[ ]` to `[x]`

Then print:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Step N complete: [short description]

🧪 To test manually:
[Exact instructions — command to run, URL to visit, UI action, curl request]

📋 Remaining steps: N
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**STOP.** Ask the user: *"Let me know when it works, or describe any issues and I'll fix them."*

Wait for confirmation before doing anything else. If the user reports a problem, fix it and re-print the test instructions. Do not move on until they confirm it works.

---

## After user confirmed step worked

Once the user confirms the step works, proceed automatically through these phases:

### Commit

1. Run `git diff --stat` and summarize what changed across all steps
2. Stage relevant changes precisely (do not add unrelated files)
3. Write a conventional commit message with a descriptive body
4. Commit and show the hash

### Code Review

1. Run the `/gloria` skill on the new commit.
1. Run the `/tessa` skill on the new commit.
1. Run the `/hector` skill on the new commit.

### Coverage

1. Run `mise run diff-cover` and make a brief plan how to fix each of the missing coverage line
2. Ask if the plan is ok before you proceed
3. Add the required tests and ensure the lines they should covered were covered

### Shitcheck

1. Run `mise run shitcheck` and analyze how the problematic changes could be fixed. Make a plan and wait for confirmation
2. Make the required changes and ensure they fix the problem.

### Session Summary

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎉 Feature complete

✅ All N steps implemented and confirmed
🔖 Commit: <hash>
🔍 Code review: <N critical / N suggestions / N nitpicks>
📊 Coverage delta: <before>% → <after>%
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
