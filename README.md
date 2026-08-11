# Security+ Boundary Drill

A single-file, offline study tool for **CompTIA Security+ (SY0-701)** that drills the thing multiple-choice
practice banks train badly: **telling confusable categories apart.**

No install, no server, no dependencies, no network. Download `boundary-drill.html`, open it in a browser,
done. Progress saves to `localStorage`.

## Why this exists

Most Security+ prep asks you to recall a definition. The exam asks you to **apply a label to a situation** —
and the situations are written so that several answers look defensible. If you learn Security+ by reviewing
missed questions and reading the correct answer, you build *item recognition*: it transfers well where the
answer carries a portable fact (a port number, where a DMZ sits, what a SIEM does) and transfers poorly where
the answer is a **judgement about where one category ends and another begins**.

That second kind is most of Domain 1 and Domain 5 — control types and categories, risk responses, agreement
types, governance documents, due diligence versus due care. Reading "the answer was *compensating*" teaches
you almost nothing about the next scenario, because the wording changes and the boundary is the actual
content.

This tool drills boundaries directly: read a situation, classify it, get the discriminating rule back
immediately.

## What's in it

**47 boundaries · 338 scenarios · 217 acronyms**, covering all five SY0-701 domains.

| Domain | Boundaries | Scenarios |
|---|---|---|
| 1.0 General Security Concepts | 13 | 93 |
| 2.0 Threats, Vulnerabilities & Mitigations | 6 | 43 |
| 3.0 Security Architecture | 6 | 44 |
| 4.0 Security Operations | 9 | 63 |
| 5.0 Security Program Management & Oversight | 13 | 95 |

Examples of what a "boundary" means here: preventive vs deterrent vs detective vs corrective vs
compensating; MAC vs DAC vs RBAC vs ABAC; incremental vs differential backups; SLA vs MOU vs MOA vs MSA vs
SOW; RTO vs RPO vs MTTR vs MTBF; data owner vs controller vs processor vs custodian; IDS vs IPS; forward vs
reverse proxy; SPF vs DKIM vs DMARC; false positive vs false negative; policy vs standard vs procedure vs
guideline; honeypot vs honeynet vs honeyfile vs honeytoken; due diligence vs due care.

## How it works

**Every answer explains the boundary, not just the item.** You get the discriminating rule for the whole
category set, plus — when you're wrong — your pick and the correct answer side by side with both definitions.
The goal is that you leave knowing the *line*, not that one scenario.

**Miss one and it serves three more on that same boundary** before moving on. You can't skip past a
distinction you've just demonstrated you don't hold.

**Selection is weighted by measured miss rate.** Unseen and sub-60% boundaries surface roughly 4× as often as
ones you're holding at 80%+. Unseen *scenarios* are strongly preferred over ones you've already answered.

**Scoring counts cold attempts only.** This is the important one. Any finite pool gets memorised eventually,
and when it does your in-app accuracy climbs while your real ability doesn't. So a scenario scores toward
your band only when it is **cold** — never seen, or not seen for 14 days. Anything sooner is a same-week
repeat, tracked separately and excluded from the band.

The 14-day rule matters at volume. Scoring *true first exposures only* would freeze your stats once the pool
is used up — at an hour a night that happens in about two weeks, after which the numbers would show where you
were a fortnight ago. Re-testing an item you last saw two weeks back is genuine retrieval, so it re-qualifies
and the band stays alive.

The tool shows **cold accuracy against same-week repeat accuracy**. If the gap exceeds 20 points it says
plainly that you're recalling scenarios rather than judging boundaries, and that the repeat number is not
your exam score.

**Bands under 10 cold answers are marked provisional.** At a 4-option guess floor, five attempts cannot
distinguish a 60% boundary from an 85% one.

**Selection is recency-aware.** Accuracy alone has no concept of time, so a boundary answered three weeks
ago would otherwise rank identically to one answered this morning. Weight rises with days since last seen,
and nothing is allowed to go more than 10 days untouched.

Options are shuffled on every render, so you can't encode button positions.

## Optional: set your exam date

Near the top of the script block:

```js
const EXAM = null;   // set to e.g. new Date(2027, 2, 14)
```

Set it — month is 0-indexed, so `2` is March — and two things switch on:

- a **countdown** in the header, amber inside two weeks and red in the final week;
- a **final-week coverage sweep**. In the last 7 days the scheduler stops chasing your weakest boundaries and
  starts prioritising any boundary you have *not* touched that week, so none of the 47 is cold on exam
  morning. A banner tracks how many remain.

Leave it `null` and both features stay off; everything else works unchanged.

## Glossary

A second view holds 217 acronyms, searchable across the abbreviation, the expansion *and* the explanation —
so searching `kerberos` surfaces KDC, TGT and NTP, not just an exact match. Where an acronym is genuinely
ambiguous on the exam it says so rather than picking one: MAC has three meanings, RBAC two, SAN and SOC two
each, and AV means antivirus *or* asset value depending on the domain.

## Usage

Number keys `1`-`9` select an answer. `Enter` advances. The domain filter restricts the pool to one domain
and scopes the stats with it. "Reset progress" clears everything.

Works on phones — one option per row, 48px targets, and it can be added to the home screen to run
full-screen. Note that mobile browsers treat `file://` pages as origin-less, so `localStorage` may not
persist for a downloaded local copy; serve it over `http(s)` if you want progress to survive on a phone.

## Scope and honest limits

- **It does not cover performance-based questions.** PBQs are a meaningful part of the exam and this trains
  none of them. Source real PBQ practice separately.
- **It is not a question bank.** There's no timed full-length mode and no score prediction. It targets one
  specific weakness; use real practice exams to measure readiness.
- **Ports and protocols are not drilled.** That's recall rather than judgement and doesn't fit the format.
- Content was written against the published SY0-701 objectives. Verify anything that matters against
  CompTIA's current objectives document — exam versions change.

## Contributing

Scenarios live in the `ITEMS` array and boundaries in `B`, both near the bottom of the file. A scenario is:

```js
{b:"control-type", a:"Deterrent", s:"<the situation>", w:"<why that answer, in terms of the boundary>"}
```

`b` is the boundary id, `a` must exactly match one of that boundary's `defs` keys. Keep `s` a *situation*
rather than a definition prompt, and make `w` explain the discriminating line rather than restating the
answer. PRs adding depth to existing boundaries are more useful than new boundaries.

## Licence

MIT — see [LICENSE](LICENSE).

Not affiliated with or endorsed by CompTIA. CompTIA and Security+ are trademarks of their respective owners.
