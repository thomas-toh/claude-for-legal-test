---
name: cold-start-interview
description: House cold-start for the arbitration plugin — captures the seat, the institution and applicable rules, the adopted evidentiary rules (IBA vs. Prague vs. tribunal discretion), the side (Claimant or Respondent), the confidentiality regime, and house style, then writes the practice profile CLAUDE.md. Use on a fresh install, when setting up or redoing the profile, or to re-check available integrations.
argument-hint: "[--redo | --check-integrations]"
---

# /cold-start-interview

1. Check `~/.claude/plugins/config/claude-for-legal/arbitration-legal/CLAUDE.md`. If already populated and no `--redo`, ask before overwriting.
2. Read the shared `~/.claude/plugins/config/claude-for-legal/company-profile.md` if it exists; reuse the party-level facts rather than re-asking. If it doesn't exist, create it.
3. Run the interview. Keep it to ~5-10 minutes; offer a 2-minute quick start that fills only the load-bearing fields (seat, rules, side) and leaves the rest as defaults to refine later.

## Part 0 — role and side

- **Role:** `firm-counsel` | `in-house` | `sole-practitioner` | `other`. Routes vocabulary and whether matter workspaces are offered (multi-matter practices) or suppressed (single matter).
- **Side:** `claimant` | `respondent` | `both` (with a default). Note any counterclaim, which flips the frame within the matter.

## Part 1 — the arbitration framework (the load-bearing block)

Capture, because every skill reads it and a Redfern Schedule built on the wrong rules is wrong:

- **Seat (lex arbitri)** and **governing law of the contract** (they often differ).
- **Institution or ad hoc:** ICC | LCIA | SIAC | HKIAC | UNCITRAL ad hoc | ICSID | other; and the **rules + version** (e.g., SIAC 2025, ICC 2021).
- **Evidentiary rules adopted:** IBA Rules 2020 | Prague Rules 2018 | tribunal discretion | bespoke PO regime. **Ask explicitly** — do not assume the IBA Rules.
- **Operative procedural order on production** (cite the paragraphs once issued).
- **Regime:** commercial | investment-treaty (name the instrument) | ICSID Convention.
- **Language**, **tribunal composition**, and the **confidentiality regime** (by rule / agreement / PO / none).

## Part 2 — integrations

Check document storage (Drive / SharePoint / Box), DMS (iManage / NetDocuments), chat (Slack / Teams), and any
arbitration research connector (Jus Mundi / Kluwer). Record status and the fallback when unavailable.

## Part 3 — house style

Schedule format (4- vs 5-column Redfern), numbering and cross-reference conventions, tone, and any seed documents (a
prior Redfern Schedule, PO1, the Statement of Claim / Defence, the agreed list of issues). Seed documents are optional
but sharpen every skill.

## Write

Write the populated profile to `~/.claude/plugins/config/claude-for-legal/arbitration-legal/CLAUDE.md`, creating parent
directories as needed, preserving the shared-guardrail sections from the template verbatim. Confirm the path and the
key fields back to the user, then suggest the first run: `/arbitration-legal:redfern-schedule`.

`--check-integrations` re-tests connector availability and updates only the integrations table.
