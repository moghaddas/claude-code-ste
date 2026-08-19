# STE reference: term lists, rewrites, and where the rules yield

Loaded by `SKILL.md` when a task needs the term-list template, a worked
example, or the boundary cases the core rules don't cover on their own.

## Term list

Every other part of this skill is reusable as written. The term list is not:
each project builds and maintains its own.

Fix one word for each concept in the system and never substitute a synonym
for variety. A synonym reads as a second thing. If an `event type` is also
called a booking page in one comment and a meeting type in another, a reader
who does not already know the codebase now believes there are three
entities.

Write the list as two columns, the word to use and the words people have
used instead:

| Use | Not |
|---|---|
| slug | handle, path, identifier, URL name |
| workspace | account, organisation, tenant |
| seat | licence, user slot |

Two rules keep the list alive. Add a row when a term drifts twice — once is
a slip, twice is a pattern. And a list nobody extends stops being true, at
which point it is worse than none, because people still trust it.

## Rewrites

**Comment**

Before:
> // This was previously handled by the old sync job, but since we moved to
> // the new architecture the caching is now being done here to avoid the
> // N+1 that was causing timeouts in production.

After:
> // Caches the connected calendars for the request. Without it, each slot
> // check queries the calendar table again and the availability endpoint
> // times out.

The first version narrates how the code got here, which git already
records. The second states what is true now and what breaks without it.

**Runbook step**

Before:
> It should be noted that prior to deployment the migration will need to
> have been run, otherwise errors may potentially occur in the seat
> synchronisation subsystem.

After:
> Run the migration before you deploy. If you deploy first, seat sync fails
> and the billing provider is not retried.

The rewrite puts the condition first, uses one instruction per sentence, and
states the consequence plainly instead of hedging it into "may potentially
occur".

**Pull request description**

Before:
> This MR implements a refactoring of the availability calculation logic in
> order to facilitate the resolution of the timezone-related discrepancies
> which have been observed being reported by users situated in
> DST-observing regions.

After:
> Fixes wrong slots for hosts in DST regions. Availability now computes in
> the host's timezone and converts once, at render. It converted per slot
> before, so a slot that crossed the DST boundary shifted by an hour.

## Where the rules yield

STE is a constraint language, so it occasionally makes a sentence worse. Two
cases that happens in:

**Terms of art.** `idempotent`, `webhook`, and `JSONB` are the everyday
words in this domain. The rule against uncommon vocabulary targets words
chosen to sound clever, not words chosen to be exact.

**Real ambiguity.** Sometimes a thing genuinely has two possible readings,
and the honest sentence says so. Write the longer sentence.

Break a rule only when obeying it makes the sentence wrong or unreadable.
Not before.

## Origin

This is a working distillation of **ASD-STE100**, licensed by the AeroSpace
and Defence Industries Association of Europe and not reproduced here. The
full specification is free after registration at
[asd-ste100.org](https://www.asd-ste100.org/).
