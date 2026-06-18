# Arbitration Legal

International-arbitration counsel work for Claude — starting with the part of a matter that is unmistakably
arbitration and entirely public practice: **document production**.

The other plugins in this repo cover in-house functions and US litigation. International arbitration has its own
evidentiary world — the IBA Rules on the Taking of Evidence, the Prague Rules, seat-specific *lex arbitri*, and
institution rules (ICC, LCIA, SIAC, HKIAC, UNCITRAL, ICSID) — and its own confidentiality regime. This plugin starts
there.

> **Status:** `v0.1.0` — first skill. Built to the repo's conventions (doctrine carried in the skill, provenance tags
> on load-bearing items, a `CLAUDE.md` guardrail net, draft-not-a-filing posture). The matter / issue-element model,
> a Schedule of Costs builder, and a procedural-timetable tracker are the intended next skills.

## What's in it

| Skill | Command | What it does |
|---|---|---|
| **Redfern Schedule** | `/arbitration-legal:redfern-schedule` | Build, populate, or review a Redfern Schedule. Drafts IBA Rules 2020 **Article 3.3**-compliant requests, maps objections to the **Article 9.2** grounds, drafts replies, and audits an existing schedule with a per-row disposition *estimate* (counsel's judgement, never asserted as the tribunal's ruling). |
| **Cold-start interview** | `/arbitration-legal:cold-start-interview` | Captures the seat, the institution and rules, the **adopted evidentiary rules**, the side, and the confidentiality regime, and writes the practice profile. Run this first. |

## Two things this plugin is strict about

1. **It reads the adopted evidentiary rules before it acts.** A Redfern Schedule built against the wrong regime is
   wrong. If the matter is on the Prague Rules, tribunal discretion, or ICSID practice rather than the IBA Rules, the
   skill recalibrates and says so.
2. **Confidentiality and the disclosed-document use restriction are hard gates.** Arbitration is usually confidential,
   and documents produced in the arbitration may be used only for it. The plugin will not move the schedule or produced
   documents outside the tribunal / parties / advisers circle.

## Getting started

1. `/arbitration-legal:cold-start-interview` (~5 minutes) — sets the seat, rules, and side.
2. `/arbitration-legal:redfern-schedule --requests` (or `--objections`, `--review`).

Every output is a draft for instructed counsel. Whether a request is granted is the tribunal's decision alone.

## Licence

Apache-2.0, consistent with the repository.
