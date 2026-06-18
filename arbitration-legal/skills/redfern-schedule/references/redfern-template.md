# Redfern Schedule — template & quick reference

A reference for the `redfern-schedule` skill. The controlling authority is the **operative procedural order and the
adopted evidentiary rules**; this template is a structuring default, not a rule.

## Column schemas

**5-column (default).** Used where the schedule carries the parties' positions and the tribunal completes the last
column.

| No. | Documents / category requested | Relevance & materiality (requesting party) | Objections (requested party) | Reply (requesting party) | Tribunal decision |
|---|---|---|---|---|---|

**4-column.** Where the tribunal directs a single round without replies.

| No. | Documents / category requested | Relevance & materiality | Objections | Tribunal decision |
|---|---|---|---|---|

Conventions: number requests `R-1, R-2, …`; cross-reference submissions in the relevance column (`[SoC §__]`,
`[SoD §__]`, `[Reply §__]`); reference documents by exhibit ID (`[C-014]`, `[R-021]`); keep the relevance column to the
issue and the materiality consequence — no rhetoric.

## IBA Rules 2020 — Article 3.3 (a request must satisfy all three)

- **3.3(a) Identification.** A specific document, OR a *narrow and specific category* described in sufficient detail
  including subject matter and reasonably believed to exist. For ESI: may specify files, search terms, custodians, time
  periods.
- **3.3(b) Relevance & materiality.** A statement of how the documents are relevant to the case AND material to its
  outcome — best tied to a named pleaded issue.
- **3.3(c) Possession.** A statement that the documents are not in the requesting party's own possession/custody/control
  (or why self-production is unreasonably burdensome), AND why they are believed to be in the other party's
  possession/custody/control.

State labels used by the skill: `compliant` · `fishing-expedition` (fails 3.3(a)) · `relevance-thin` (fails 3.3(b)) ·
`possession-missing` (fails 3.3(c)).

## IBA Rules 2020 — Article 9.2 (objection grounds)

`relevance/materiality` 9.2(a) · `privilege/legal-impediment` 9.2(b) · `burden` 9.2(c) · `loss/destruction` 9.2(d) ·
`commercial/technical confidentiality` 9.2(e) · `political/institutional sensitivity` 9.2(f) ·
`procedural economy / proportionality / fairness / equality` 9.2(g).

Grounds (e), (f), (g) require the tribunal to find the ground **compelling**. A confidentiality objection (9.2(e))
pairs with an Art. 9.4 confidentiality-arrangement proposal, not a flat refusal.

## Article 9.3 — privilege (flag, do not decide)

Privilege is a choice-of-law question (seat / governing law / parties' home bars / tribunal discretion). Factors:
confidentiality of legal advice or settlement; expectations at creation; waiver; fairness and equality where parties are
subject to different rules. The skill flags `[review — privilege choice-of-law]` and never concludes.

## Regime note

Under the **Prague Rules (2018)** production is the exception; the relevance/materiality bar is higher and "narrow and
specific category" tightens toward "identified document." Under **ICSID / investment-treaty** practice, production
follows the tribunal's procedural order and differs from commercial IBA practice. The skill recalibrates and tags
outputs accordingly.
