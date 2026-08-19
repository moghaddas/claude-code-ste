---
name: ste
description: >-
  Apply Simplified Technical English (a working distillation of ASD-STE100) to
  English technical prose. Use when writing or reviewing code comments,
  docblocks, commit messages, pull request or merge request descriptions,
  README or CLAUDE.md prose, architecture and decision notes, runbooks,
  migration steps, incident write-ups, or error and log text an engineer
  reads. English only: does not apply to product UI copy, marketing or sales
  copy, direct quotes from a spec or vendor document, or any non-English text.
---

# Simplified Technical English for code

Rewrite the prose in scope so a non-native English speaker, debugging
something else, reads it once and understands it. Apply every rule below;
skip a rule only when obeying it makes the sentence wrong or unreadable, and
prefer the longer sentence over a genuinely ambiguous short one.

Not in scope: product UI copy, marketing or sales copy, anything sent as a
person rather than a system, a direct quote from a spec or vendor document,
or any non-English text. Leave those unchanged.

## Rules — apply every one

**Sentence and paragraph**

- Split into one instruction per sentence. Two actions need two sentences.
- Cap procedural sentences at 20 words and descriptive sentences at 25.
- Cap paragraphs at six sentences, each opening with a topic sentence.
- Put the condition or reason before the instruction: "If the lock is held, skip the job."
- Replace a sentence naming three or more parallel items with a vertical list.

**Verbs**

- Use active voice and name the actor: "the observer clears the cache", not "the cache is cleared".
- Use present tense: describe what the system does, not what it will do.
- Use the imperative for instructions: "Set `PG_HOST` before the run."
- Replace an `-ing` form with a finite verb or a relative clause:
  - `the worker holding the lock` → `the worker that holds the lock`
  - `Retrying the request causes a duplicate` → `A retry causes a duplicate`
- Collapse stacked helping verbs: "the job can fail", not "the job may be able to fail".

**Words**

- Fix one word per concept and repeat it; never vary a term for style — a synonym reads as a second concept.
- Keep articles and prepositions: "the job retries the request", not "job retries request".
- Break any noun cluster longer than three words with a preposition or relative clause:
  - `calendar sync conflict resolution strategy` → `the strategy that resolves calendar sync conflicts`
- Expand an abbreviation on first use in the file, unless it names something in the code (`JSONB`, `MR`, `API` need no expansion).
- Replace Latin abbreviations: "for example" not "e.g.", "that is" not "i.e.", "through" not "via".
- Reserve `should`/`may`/`might` for genuine uncertainty; state a fact as a fact.

**Warnings and consequences**

- State the symptom before the cause: "The sync fails silently. The daemon logs the failure and keeps the stale tree."
- Name what breaks, not that something is "dangerous": say "this drops every row in `bookings`".
- Write one warning per line, at the point of risk — not a caveat wall at the top.

## Term list

Before rewriting a file, check whether the project has a term list (a
two-column "use / not" table naming the fixed word for each concept — see
`reference.md`). If one exists, enforce it. If a term drifts twice across the
files touched in this task, add a row instead of letting the drift stand.

## Additional resources

- `reference.md` — the term-list template and rationale, three worked
  before/after rewrites (comment, runbook step, PR description), and the two
  cases (terms of art, real ambiguity) where a rule is meant to yield.
