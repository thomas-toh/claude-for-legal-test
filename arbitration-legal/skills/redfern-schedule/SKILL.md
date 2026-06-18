---
name: redfern-schedule
description: Build, populate, or review a Redfern Schedule for document production in international arbitration — draft IBA Rules (2020) Article 3.3-compliant requests, map objections to the Article 9.2 grounds, draft replies, and audit an existing schedule with a per-row disposition estimate. Use when the user mentions a Redfern Schedule, document production / disclosure requests, requests to produce, objections to production, Article 3 / Article 9 IBA Rules, or asks "what can we ask for / object to" in an arbitration.
argument-hint: '[--build | --requests | --objections | --replies | --review] [--side claimant|respondent] [--rules iba|prague|discretion]'
---

# /redfern-schedule

1. Load `~/.claude/plugins/config/claude-for-legal/arbitration-legal/CLAUDE.md` → side, seat, **applicable evidentiary rules**, confidentiality regime, work-product header, house style.
2. **Rules gate (run before anything else).** Read `## Arbitration framework → Evidentiary rules adopted`. The Redfern Schedule and the doctrine below assume the **IBA Rules on the Taking of Evidence (2020)**. If the profile says **Prague Rules**, **tribunal discretion**, or a **bespoke PO regime**, stop and recalibrate — see *Rules gate* below. Do not produce an IBA-Art.-3-shaped schedule against a non-IBA regime without flagging it.
3. If matter workspaces are enabled, confirm or select the active matter; load `matter.md` (side, seat, the pleaded case, the agreed list of issues, PO1).
4. Mode selection: `--build` (assemble/populate the schedule), `--requests` (draft your side's requests), `--objections` (object to the other side's), `--replies` (reply to objections), `--review` (audit an existing schedule). No flag → ask which.
5. Run the mode workflow below. Tie every request to a pleaded issue or submission paragraph; cite every document reference. Apply the apostrophe-prefix neutralisation before writing any cell value starting with `=`, `+`, `-`, `@`, tab, or CR.
6. Produce the priority output for the mode (vulnerable-request list / strongest-ground list / disposition estimate).
7. Write markdown, CSV (values + `_sources` companion), and Excel or Sheets per preference. Work-product header on every output. Write to the matter's `redfern-schedules/` folder if a matter is active, else the practice-level folder; append a one-line entry to `history.md` if a matter is active.
8. Return the summary readout and the next-steps decision tree.

---

# Redfern Schedule

## A SCHEDULE IS A DRAFT FOR COUNSEL, NOT A FILING OR A TRIBUNAL DECISION

**Put this at the top of every output. Do not drop it. Do not soften it.**

> This schedule is a working draft for instructed counsel's review, not a submission to the tribunal and not a ruling. Every relevance statement, every objection, and every disposition estimate is a lead counsel must verify and own. Whether a request is granted is the tribunal's decision alone; nothing here predicts or substitutes for it. The applicable evidentiary rules and the operative procedural order control over any default in this skill.

Under-stating a request's vulnerability is a one-way door — a request struck as a fishing expedition, an objection waived for being unfounded. Over-flagging is a two-way door counsel closes in review. The default is biased toward the two-way door.

## Confidentiality gate — unbypassable

Before working with any production material, confirm two things and flag if either is unmet:

- **Arbitration confidentiality.** Most arbitrations are confidential by rule, agreement, or PO. The schedule, the requests, and the documents inherit that duty. Do not move any of it outside the tribunal / parties / advisers circle. If the user names a destination outside that circle, flag it (see CLAUDE.md *Confidentiality / destination check*).
- **Disclosed-document use restriction.** Documents already produced in the arbitration may be used only for this arbitration. If the user is repurposing produced documents for another matter or a commercial use, flag and stop: "⚠️ Produced documents carry a use restriction — confirm this use is within this arbitration or that consent / tribunal permission exists before proceeding."

## Rules gate

The doctrine in this skill is the **IBA Rules 2020 (Articles 3 and 9)**. Confirm the regime before producing a schedule:

- **IBA Rules adopted** → proceed normally.
- **Prague Rules (2018)** → recalibrate and say so first: *"This matter is on the Prague Rules, under which document production is the exception, not the norm — Art. 4 disfavours broad requests and the tribunal drives evidence-gathering. I can still build a schedule, but the relevance-and-materiality bar is higher and 'narrow and specific category' becomes 'specific, identified document.' I'll flag every request that would be routine under the IBA Rules but vulnerable under Prague."* Then build with the stricter calibration.
- **Tribunal discretion / no adopted rules** → ask what PO1 says about production. If PO1 sets a standard, use it and cite the operative paragraphs. If it is silent, default to the IBA framework *as a structuring tool only*, tagged `[IBA framework used as a default — confirm the tribunal's standard]`.
- **ICSID / investment-treaty** → note that ICSID practice on production differs from commercial IBA practice and tag conclusions `[ICSID practice — verify against the tribunal's procedural order]`.

If `CLAUDE.md` still has `[PLACEHOLDER]` markers, offer the configured run (`/arbitration-legal:cold-start-interview`, ~5 min) or a **provisional** run against generic defaults (IBA Rules 2020, commercial arbitration, claimant side) with every row tagged `[PROVISIONAL]`.

---

## The doctrine (carried in the skill, not pointed at)

### Request validity — IBA Rules 2020, Article 3.3

A Request to Produce must satisfy all three limbs. The skill tests each request against them and flags any limb that fails.

| Limb | Requirement | Failure mode the skill flags |
|---|---|---|
| **3.3(a) — Identification** | Either (i) a description sufficient to identify a specific document, **or** (ii) a description "in sufficient detail (including subject matter)" of a **narrow and specific category** of documents reasonably believed to exist. For electronic documents, the request may identify files, search terms, custodians, or time periods. | Category too broad / undefined date range / "all documents relating to" with no subject-matter or time limit → `fishing-expedition` |
| **3.3(b) — Relevance & materiality** | A statement of how the documents are **relevant to the case and material to its outcome** — tied, ideally, to a specific pleaded issue or submission paragraph. | No tie to a pleaded issue; relevance asserted but not materiality; argumentative padding instead of a clean statement → `relevance-thin` |
| **3.3(c) — Possession & custody** | (i) A statement that the documents are **not in the requesting party's own possession, custody or control** (or why self-production would be unreasonably burdensome); **and** (ii) the reasons the requesting party assumes they are in the **other party's** possession, custody or control. | Missing possession statement; no basis stated for believing the other side holds them → `possession-missing` |

A request that clears all three is `compliant`. Anything else is flagged with the failing limb. This is the gate before requests go into the schedule.

### Objection grounds — IBA Rules 2020, Article 9.2

Objections are not free-text. Each maps to an enumerated ground; the skill labels the ground and notes that several (e) (f) (g) require the tribunal to find the ground **compelling**.

| Ground | Art. 9.2 basis | Notes |
|---|---|---|
| `relevance/materiality` | 9.2(a) | Lack of sufficient relevance or materiality to the outcome |
| `privilege/legal-impediment` | 9.2(b) | Under the legal/ethical rules the tribunal determines applicable — **choice-of-law is contested; flag, don't resolve** (see Art. 9.3) |
| `burden` | 9.2(c) | Unreasonable burden to produce — quantify (volume, cost, custodians) or it is weak |
| `loss/destruction` | 9.2(d) | Reasonable likelihood the documents are lost or destroyed |
| `commercial/technical confidentiality` | 9.2(e) | Tribunal must find it **compelling**; pairs with an Art. 9.4 confidentiality-arrangement proposal rather than a flat refusal |
| `political/institutional sensitivity` | 9.2(f) | Incl. classified/State material; tribunal must find it compelling |
| `procedural economy / proportionality / fairness / equality` | 9.2(g) | Tribunal must find it compelling — the catch-all, strongest when paired with another ground |

### Privilege — IBA Rules 2020, Article 9.3 (flag, don't decide)

Privilege in international arbitration is a **choice-of-law problem**, not a single standard. The tribunal may weigh (9.3): the need to protect the confidentiality of legal advice or settlement negotiations; the parties' and advisers' expectations when the document was created; possible waiver; and the need to maintain fairness and equality, especially where the parties are subject to **different legal or ethical rules**. The skill flags a privilege objection and surfaces the choice-of-law question (`[review — privilege choice-of-law: seat / governing law / parties' home bars all potentially relevant]`). It never asserts that a document is or is not privileged.

---

## Modes

### `--build` — assemble or populate the schedule

Produce the schedule in house format (default 5-column). If the parties have exchanged requests/objections, populate from them; if starting fresh, lay out the numbered request rows with the relevance and possession statements built per Art. 3.3 and the objection/reply/decision columns blank. Tie each request to its pleaded issue. Run the Art. 3.3 check on every request and surface the vulnerable-request list.

### `--requests` — draft this side's requests

For each document or category the user wants, draft a request that satisfies all three Art. 3.3 limbs: a narrow-and-specific description (with subject matter + a bounded time period; for ESI, propose custodians and search terms), a relevance-and-materiality statement tied to a named pleaded issue, and the possession/custody statement. **Killer output:** the vulnerable-request list — every request flagged `fishing-expedition`, `relevance-thin`, or `possession-missing`, with the fix, *before* the request goes to the other side or the tribunal.

### `--objections` — object to the other side's requests

For each incoming request, identify the strongest available Art. 9.2 ground (and any secondary grounds), draft the objection, and — where the ground is confidentiality (9.2(e)) — pair it with an Art. 9.4 confidentiality-arrangement proposal rather than a flat refusal. **Killer output:** the strongest-ground-per-request map, plus a note on which objections are weak enough that pressing them risks the tribunal's patience.

### `--replies` — reply to objections

For each objection, draft the requesting party's reply: narrow the request if that defeats a burden/specificity objection, restate the materiality tie if relevance is challenged, propose a confidentiality ring if confidentiality is raised. Flag where a reply is unlikely to move the tribunal and a narrowed request is the better play.

### `--review` — audit an existing schedule

For each row: is the request Art. 3.3-compliant? Is the objection a real Art. 9.2 ground or rhetoric? Then a **per-row disposition estimate** — `likely granted` / `likely narrowed` / `likely denied` — **tagged `[disposition estimate — counsel's judgement, not the tribunal's ruling]`** with the one-line reason. The estimate is a planning aid, never a prediction asserted as fact.

---

## Output

Prepend the work-product header from CLAUDE.md `## Outputs`.

### Markdown table (always) — default 5-column Redfern

```markdown
| No. | Documents / category requested | Relevance & materiality (requesting party) [submission cross-ref] | Objections (requested party) [Art. 9.2 ground] | Reply (requesting party) | Tribunal decision |
|---|---|---|---|---|---|
| R-1 | Board minutes of [Co.] approving the 2018 supply variation, Jan–Jun 2018 | Goes to whether the variation was authorised — disputed at [SoD §§ 41-46]. Material: if unauthorised, the breach claim fails at the threshold. | Burden 9.2(c); confidentiality 9.2(e) | Narrowed to the two meetings identified in [C-014]; ring proposed | ☐ |
```

Follow with: the **vulnerable-request list** (`--requests`/`--build`), the **strongest-ground map** (`--objections`), or the **disposition estimate** (`--review`) — the priority output for the mode — then a one-line conclusion: *"This skill does not decide production. Requests compliant: [list]. Requests flagged: [list]. Tribunal decides."*

### CSV (always)

Two files: `[slug].csv` (values) and `[slug]_sources.csv` (verbatim quotes, document IDs, submission pin-cites).

**Cell safety.** Before writing any cell, check the first character. If it is `=`, `+`, `-`, `@`, tab (`\t`), or carriage return (`\r`), prepend a single apostrophe to neutralise spreadsheet formula execution. Verbatim text from the counterparty's requests or produced documents can carry strings a spreadsheet will execute (`=HYPERLINK(...)`, `=cmd|...!A1`); RFC-4180 quoting does not defeat this. Apply in CSV, XLSX, and Sheets. Log neutralised cells in the reviewer note.

### Spreadsheet (Excel or Sheets)

Ask which the team uses. One row per request. Each substantive column paired with a hidden `_source` column carrying the verbatim text and pin-cite (surfaced on hover). Colour by Art. 3.3 state: white = `compliant`, yellow = `relevance-thin` / `possession-missing`, orange = `fishing-expedition`. A `Tribunal decision` column, blank. An `_issues` sheet mapping each request number to the pleaded issue it serves — this is what makes the schedule auditable. Apply the apostrophe-prefix to every cell.

### Filename and location

`redfern-[matter-slug]-[side]-[round]-YYYY-MM-DD.{md,csv,xlsx}`. If a matter is active: `~/.claude/plugins/config/claude-for-legal/arbitration-legal/matters/<matter-slug>/redfern-schedules/`; else the practice-level folder. Surface the path; append a line to `history.md`.

## Summary readout

One screen: side, seat, rules basis, mode; requests drafted/reviewed; counts by Art. 3.3 state; the priority list for the mode; file paths; and the reminder that the tribunal decides and every row is a lead.

## Non-lawyer gate

If `## Who's using this` Role is Non-lawyer:

> This schedule is a working draft, not a submission. Serving production requests or objections has consequences in the arbitration — instructed counsel must review and own it before anything goes to the other side or the tribunal. Here is a one-page brief to bring to counsel: [side, seat, rules, the requests by issue, the flagged-vulnerable list, the two or three calls counsel needs to make].

## Shared guardrails — checklist

- **Tie to a pleaded issue.** A request with no link to the pleaded case is `relevance-thin` by default — relevance and materiality are the gate, not an afterthought.
- **No silent supplement.** If a document's existence or location is asserted without basis, the cell is `possession-missing`, not an assumption. Do not invent custodians or document IDs.
- **Provenance on the load-bearing items.** Document IDs, submission pin-cites, and rule articles each carry their source; a relevance statement that cites `[SoD §__]` must point at a real paragraph or be tagged `[verify]`.
- **Privilege is flagged, never decided** (Art. 9.3 choice-of-law).
- **Rules basis stated.** Every output names the regime it was built against (IBA / Prague / discretion / ICSID).
- **The tribunal decides.** No disposition is asserted as the tribunal's ruling; estimates are tagged as counsel's judgement.

## Relationship to other skills

- `arbitration-legal:cold-start-interview` — sets the seat, the rules, and the side this skill reads.
- A future `arbitration-legal:issue-element-model` (the matter model) would supply the pleaded-issue list each request ties to — the relevance column is strongest when it points at a tracked issue, not a free-text description.
- `litigation-legal:claim-chart` — the US-litigation cousin; same element/issue-to-evidence discipline, different procedural world.

## Close with the next-steps decision tree

End with the decision tree per CLAUDE.md `## Outputs`, customised to what the run produced (e.g., draft the cover letter to the tribunal, narrow the flagged requests, draft the reply column, hold pending the other side's objections, something else). The tree is the output; counsel picks.

## What this skill does not do

- **It does not decide production.** Whether a request is granted is the tribunal's call alone.
- **It does not decide privilege.** It flags the Art. 9.3 choice-of-law question for counsel.
- **It does not assert a disposition as a ruling.** Estimates are counsel-judgement planning aids, tagged as such.
- **It does not apply the IBA Rules to a non-IBA matter** without flagging the recalibration.
- **It does not move produced documents or the schedule outside the confidentiality circle**, and it does not invent document IDs, custodians, or submission cites to fill a gap.
