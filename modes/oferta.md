# Mode: oferta — Full Evaluation A-F

## OUTPUT RULE: Be extremely brief in user-facing output. Save all detail to the report file. Show the user ONLY a compact summary (see "User-Facing Output" section at the bottom).

When the candidate pastes a job offer (text or URL), ALWAYS run all 6 blocks internally:

## Step 0 — Archetype Detection

Classify the offer into one of the 6 archetypes (see `_shared.md`). If hybrid, indicate the 2 closest. This determines:
- Which proof points to prioritize in Block B
- How to rewrite the summary in Block E
- Which STAR stories to prepare in Block F

## Block A — Role Summary

Table with:
- Detected archetype
- Domain (regulatory/quality/clinical/digital health)
- Function (write/document/coordinate/review/submit)
- Seniority
- Remote (full/hybrid/onsite)
- Team size (if mentioned)
- TL;DR in 1 sentence

## Block B — CV Match

Read `cv.md`. Create a table mapping each JD requirement to exact lines from the CV.

**Adapted to archetype:**
- If Regulatory Affairs → prioritize CTD/eCTD authoring, 510(k), IND/NDA/BLA, dossier organization, regulatory frameworks (FDA, ICH, EU MDR)
- If Medical Writer → prioritize ICF authoring, protocol inputs, safety narratives, plain-language writing, literature review, compliance-aware content
- If QA Documentation → prioritize CAPA documentation, SOP writing, root cause analysis, deviation investigations, document control, audit readiness
- If Regulatory Operations → prioritize cross-functional coordination, dossier assembly, submission workflows, trackers, deadline management
- If Post-Market Surveillance → prioritize PMS plans/reports, MAUDE synthesis, complaint documentation, safety signals, vigilance reporting
- If Digital Health Regulatory → prioritize SaMD regulatory, RPM documentation, digital health content, labeling-aware communication

**Gaps** section with mitigation strategy for each. For each gap:
1. Is it a hard blocker or nice-to-have?
2. Can the candidate demonstrate adjacent experience?
3. Is there a portfolio project that covers this gap?
4. Concrete mitigation plan (phrase for cover letter, quick project, etc.)

## Block C — Level and Strategy

1. **Detected level** in the JD vs **candidate's natural level for that archetype**
2. **Plan "position at level without overstating"**: specific phrases adapted to archetype, concrete achievements to highlight, how to position M.S. Regulatory Affairs + B.Pharm as advantage
3. **Plan "if downleveled"**: accept if comp is fair, negotiate 6-month review, clear promotion criteria

## Block D — Comp and Demand

Use WebSearch for:
- Current salaries for the role (Glassdoor, Payscale, salary surveys)
- Company compensation reputation
- Demand trend for the role

Table with data and cited sources. If no data available, say so instead of inventing.

## Block E — Customization Plan

| # | Section | Current state | Proposed change | Why |
|---|---------|---------------|-----------------|-----|
| 1 | Summary | ... | ... | ... |
| ... | ... | ... | ... | ... |

Top 5 CV changes + Top 5 LinkedIn changes to maximize match.

## Block F — Interview Plan

6-10 STAR+R stories mapped to JD requirements (STAR + **Reflection**):

| # | JD Requirement | STAR+R Story | S | T | A | R | Reflection |
|---|---------------|--------------|---|---|---|---|------------|

The **Reflection** column captures what was learned or what would be done differently. This signals seniority — junior candidates describe what happened, senior candidates extract lessons.

**Story Bank:** If `interview-prep/story-bank.md` exists, check if any of these stories are already there. If not, append new ones. Over time this builds a reusable bank of 5-10 master stories that can be adapted to any interview question.

**Selected and framed per archetype:**
- Regulatory Affairs → emphasize submission documentation accuracy, regulatory framework knowledge, dossier organization
- Medical Writer → emphasize writing clarity, plain-language communication, first-pass quality, compliance tone
- QA Documentation → emphasize audit readiness, traceability, root cause rigor, process improvement
- Regulatory Operations → emphasize coordination, deadline management, cross-functional workflow efficiency
- Post-Market Surveillance → emphasize data synthesis, risk language, surveillance documentation completeness
- Digital Health Regulatory → emphasize bridging regulatory knowledge with tech product needs

Also include:
- 1 recommended case study (which project to present and how)
- Red-flag questions and how to answer them (e.g., "Do you have industry experience beyond internships?", "How familiar are you with [specific system]?")

---

## Post-Evaluation

**ALWAYS** after generating blocks A-F:

### 1. Save report .md

Save the complete evaluation to `reports/{###}-{company-slug}-{YYYY-MM-DD}.md`.

- `{###}` = next sequential number (3 digits, zero-padded)
- `{company-slug}` = company name in lowercase, no spaces (use hyphens)
- `{YYYY-MM-DD}` = current date

**Report format (KEEP REPORTS COMPACT — tables and bullets, no prose):**

```markdown
# {Company} — {Role}

**Date:** {YYYY-MM-DD} | **Archetype:** {detected} | **Score:** {X/5} | **Verdict:** {APPLY/CONSIDER/SKIP}
**URL:** {url}
**PDF:** {path or pending}

---

## A) Role Summary

| Field | Value |
|-------|-------|
| Archetype | ... |
| Domain | ... |
| Seniority | ... |
| Remote | ... |
| TL;DR | 1 sentence |

## B) CV Match

| JD Requirement | CV Evidence | Match |
|---------------|-------------|-------|
| ... | ... | ✅/⚠️/❌ |

**Gaps:** (bullet list, 1 line each with blocker/nice-to-have tag)

## C) Level

- JD level: ...
- Candidate level: ...
- Positioning: 1-2 sentences max

## D) Comp

| Data Point | Value | Source |
|-----------|-------|--------|
| Market range | ... | ... |
| Company rep | ... | ... |

## E) CV Tailoring

| # | Section | Change | Why |
|---|---------|--------|-----|
| 1 | ... | ... | ... |

## F) Interview Prep

| # | JD Requirement | STAR Story (1 line) |
|---|---------------|---------------------|
| 1 | ... | ... |

**Case study:** 1 line
**Red-flag Qs:** bullet list

## G) Draft Answers
(only if score >= 4.5 — 2-4 sentences per answer, no preamble)

---

## Keywords
(comma-separated list, no explanations)
```

**RULE: No paragraph-style writing in reports. Every section uses a table or bullet list. If it can't fit in a table row, it's too long.**

### 2. Register in tracker

**ALWAYS** register in `data/applications.md`:
- Next sequential number
- Current date
- Company
- Role
- Score: match average (1-5)
- Status: `Evaluated`
- PDF: ❌ (or ✅ if auto-pipeline generated PDF)
- Report: relative link to the report .md (e.g., `[001](reports/001-company-2026-01-01.md)`)

**Tracker format:**

```markdown
| # | Date | Company | Role | Score | Status | PDF | Report |
```

---

## User-Facing Output (CRITICAL — this is ALL the user sees)

**Do NOT print the full A-F blocks to the user.** Save them to the report file only. Show the user ONLY this compact summary:

```
## {Company} — {Role}

**Score: {X.X}/5** | {Archetype} | {Remote/Hybrid/Onsite}
**Verdict:** {APPLY / CONSIDER / SKIP} — {1 sentence why}

| Dimension | Score |
|-----------|-------|
| Reg/Quality Doc Relevance | X/5 |
| Writing Relevance | X/5 |
| CV Match | X/5 |
| North Star | X/5 |
| Industry Fit | X/5 |
| Seniority | X/5 |

**Top 3 matches:** {bullet list, 1 line each}
**Key gaps:** {bullet list, 1 line each, or "None"}
**PDF:** ✅ saved to output/... (or ❌ score too low)
**Report:** saved to reports/...
```

That's it. No Block A narrative, no Block C strategy text, no Block D salary research paragraphs, no Block F STAR stories shown. All of that goes into the report file for reference if needed.

If the user wants detail on a specific block, they ask — then show just that block.
