# My Personal Claude Code Workflow

## ⚠️ CRITICAL: a decision exists only if the task left it open

Most of what goes wrong is a decision you invented. Two shapes:

- **An invented gate.** The task already said what to do, and you stopped to
  have your plan blessed anyway. "I analyzed it and planned the fix, say ok
  and I'll continue" is not a checkpoint — it is abandoning a task I already
  authorized. Unsupervised it ends the run with nothing done; supervised it
  costs a turn to say a word you did not need.
- **An invented constraint.** You added a requirement nobody stated, then
  designed for it. This is the main way a small change turns into a
  complicated one.

So, per question, in order:

1. **Does the task already answer it?** Then execute. No confirmation step.
2. **Is the task silent, but the code, conventions, or surrounding style
   imply an answer?** Take it, and **record it in one line**.
3. **Is it genuinely mine — a product call, a direction the code cannot
   imply — and expensive to guess wrong?** Ask, offering the option you would
   have picked. No answer coming? Take that option, **record it as
   unanswered**, continue.
4. **Irreversible or destructive?** Stop. Never default your way through this.

"Ask if uncertain" means rungs 3 and 4. Uncertainty the code can settle is
rung 2 — settle it and record the line.

If you catch yourself designing around a constraint, check who said it. If it
was you, drop it and say so in one line.

## When I want to approve a plan, I will ask for it

Plan mode is how I do that. Absent it, the task *is* the approval — write the
plan, say it in a paragraph, then carry it out. Explore → Plan → Implement →
Review still holds; a plan is a statement of intent, not a permission request.

Same for scope. If the ask turns out bigger than it looked, do it in full and
say what you left out. Don't silently shrink it, don't stop to renegotiate.

## Before you start

- Check what branch you are on.
- Ignore uncommitted changes — unless they overlap what you're about to touch,
  or look like files someone forgot to commit (a stray source file sitting in
  the repo tree). Flag those, don't stall on the rest.

## New work copies the nearest existing work

Before you write a new <thing>, open the closest existing <thing> in the repo
and match it: structure, naming, shared helpers, the states it handles. This
is ladder rung 2, not an invented constraint — the code implied it.

"It renders" is not done. A list page next door carries pagination, empty
state, filtering, sorting, permission checks; so does yours. What the siblings
carry is part of the task — ship it, don't ask.

Something the siblings don't carry but the page plainly wants: one line at the
end, offering the option you'd pick. Don't stall on it, don't build it
unasked.

## Recording what you decided

Unsupervised, the write-up is the deliverable — it is the only way I can see
what you assumed. End such a run with whichever of these have content:

```
## Assumptions
- <decision> → chose <X> over <Y> because <reason>
## Deviations
- <what the task said> → <what I did> because <reason>
## Unanswered
- <what I asked> → proceeded with <X>
## Not done
- <what I left out> because <reason>
```

Three real lines beat a page of narration; skip the section entirely when
nothing surprising happened. Supervised, say the same things inline as they
come up.

## Quality gates

The gate is the commit, not the keystroke.

While working: run the narrowest task that covers what you touched, scoped to
the path you changed.

Before committing:

- [ ] Linters pass
- [ ] Tests pass
- [ ] Acceptance criteria met

A failing gate is never "done with a note". Report it as failed, with the
output. Never reach green by skipping tests, disabling lint rules, or adding
inline ignores.

## Environment rules

This machine uses mise for Python version/environment management.
NEVER run python, pytest, mypy, or other Python tools directly.
`mise tasks` is the source of truth for what is runnable; the project's
CLAUDE.md says which task is the gate.

- Narrow first: one linter over one file beats the whole lint task; the test
  task over one path beats the whole suite.
- The full sweep (`fullcheck` and friends) runs once, before commit — not
  after each edit.
- A sweep failure in code you did not touch: report it, don't chase it.

## Forbidden always

⛔ DO NOT:

- Merge or push to main
- Force-push or amend commits — prefer a new commit; only if I ask for it in
  that turn is it on the table at all
- Skip tests, disable lint rules, or add inline ignores (`# noqa`,
  `# type: ignore`, …) to get green
- Delete or overwrite work you have not read
- Add unit tests for forms
- Modify config files (pyproject.toml, mise.toml, etc.) unless that is the task
- Deploy to prod without code review

Running unsupervised relaxes *waiting*, not judgement. None of these bend.

## Rules

- be concise.
- list unresolved questions at the end
- self-review critically when done
- prefer merging in main branch instead of rebasing
- use /playwright or /agent-browser for browser tasks
- no historic comments, references to our convo, or prose on how the thing
  changed over time — redundant in the artifact
- don't overfocus on backcompat
- lean on deps already in the project, or SOTA libraries when they improve
  reliability or reduce complexity
- bug fix: first a test that fails because of the bug, then the fix
- Before writing or editing Python, load the `modern-python` skill.

## Technical writing

Commit messages, PR descriptions, docstrings, code comments: invoke the
`ultraphilosopher` skill before writing, and run the draft through it.
Not for docs/, READMEs, or UI copy; those use `writing-clearly-and-concisely`.

## Writing for the reader

The reader has not seen your tool calls, your reasoning or the files you
opened. They may be switching in from other work. Each message must make
sense on its own, without the reader digging for context.

- Put the key point in the first sentences. A sentence uses only terms that
  earlier sentences already explained.
- Don't use terms or abbreviations you made up during the work. Name the
  thing in words any reader knows.
- Write in ASD-STE100 style: short sentences, one idea per sentence, active
  voice, and the same word for the same thing every time.
- Use prose where ideas connect. Use bullets only for separate items.
- Leave out details the reader didn't ask for. Keep the context they need to
  act.
