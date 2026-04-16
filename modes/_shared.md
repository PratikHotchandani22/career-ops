# System Context -- career-ops

<!-- ============================================================
     THIS FILE IS AUTO-UPDATABLE. Don't put personal data here.
     
     Your customizations go in modes/_profile.md (never auto-updated).
     This file contains system rules, scoring logic, and tool config
     that improve with each career-ops release.
     ============================================================ -->

## Sources of Truth

| File | Path | When |
|------|------|------|
| cv.md | `cv.md` (project root) | ALWAYS |
| article-digest.md | `article-digest.md` (if exists) | ALWAYS (detailed proof points) |
| profile.yml | `config/profile.yml` | ALWAYS (candidate identity and targets) |
| _profile.md | `modes/_profile.md` | ALWAYS (user archetypes, narrative, negotiation) |

**RULE: NEVER hardcode metrics from proof points.** Read them from cv.md + article-digest.md at evaluation time.
**RULE: For article/project metrics, article-digest.md takes precedence over cv.md.**
**RULE: Read _profile.md AFTER this file. User customizations in _profile.md override defaults here.**

## OUTPUT BREVITY (CRITICAL)

**All user-facing output MUST be extremely concise.** The full analysis happens internally but the output shown to the user must be minimal. Save tokens.

- Reports saved to `reports/` can be detailed (they're written to files, not shown).
- But everything printed to the user's screen must be SHORT.
- Use tables, not paragraphs.
- No explanations the user didn't ask for.
- No restating what the JD said.
- No filler, no transitions, no "Let me analyze this for you."
- Max 20-30 lines of visible output per evaluation.
- The PDF generation, keyword injection, and resume tailoring work fully — just don't narrate the process.
- **Reports saved to files must ALSO be compact.** Tables and bullet lists only — no paragraph-style prose in any section. If it doesn't fit in a table row, it's too long.

---

## Scoring System

The evaluation uses 6 blocks (A-F) with a global score of 1-5:

| Dimension | What it measures |
|-----------|-----------------|
| Regulatory/Quality Documentation Relevance | How central is regulatory, quality, or compliance documentation to this role? |
| Medical/Scientific Writing Relevance | Does the role involve clinical, regulatory, or scientific writing as a core function? |
| CV Match | Skills, experience, proof points alignment with JD requirements |
| North Star alignment | How well the role fits the user's target archetypes (from _profile.md) |
| Industry Fit | Is this in digital health, healthtech, medtech, biotech, SaMD, or adjacent regulated environment? |
| Seniority Match | Is the level appropriate (Associate/Specialist, not too senior or too junior)? |
| Location / Work Mode Fit | Remote, hybrid-Boston, or relocation required? |
| Comp | Salary vs market (5=top quartile, 1=well below) |
| Red flags | Misleading title, wrong industry, over-senior, pure engineering, generic ops (negative adjustments) |
| **Global** | Weighted average of above |

**Scoring weights (for global calculation):**
- Regulatory/Quality Documentation Relevance: 20%
- Medical/Scientific Writing Relevance: 15%
- CV Match: 20%
- North Star alignment: 15%
- Industry Fit: 10%
- Seniority Match: 10%
- Location / Work Mode Fit: 5%
- Comp: 5%
- Red flags: deduction (0 to -1.0 from global)

**Score interpretation:**
- 4.5+ → Strong match, recommend applying immediately
- 4.0-4.4 → Good match, worth applying
- 3.5-3.9 → Decent but not ideal, apply only if specific reason
- Below 3.5 → Recommend against applying (see Ethical Use in CLAUDE.md)

## Archetype Detection

Classify every offer into one of these types (or hybrid of 2):

| Archetype | Key signals in JD |
|-----------|-------------------|
| Regulatory Affairs / Regulatory Documentation | "regulatory affairs", "CTD", "eCTD", "510(k)", "IND", "NDA", "BLA", "submission", "dossier", "regulatory intelligence", "labeling", "21 CFR", "EU MDR", "regulatory compliance" |
| Medical Writer / Clinical-Regulatory Writer | "medical writer", "medical writing", "ICF", "informed consent", "protocol", "CSR", "clinical study report", "safety narrative", "scientific communication", "literature review", "plain language", "patient-facing" |
| QA Documentation / Quality Systems / Document Control | "CAPA", "SOP", "deviation", "document control", "change control", "quality systems", "audit", "nonconformance", "root cause", "corrective action", "ISO 14971", "GMP", "quality assurance documentation" |
| Regulatory Operations / Submission Support | "regulatory operations", "submission support", "eCTD publishing", "dossier assembly", "regulatory project", "submission coordinator", "publishing", "regulatory tracking" |
| Post-Market Surveillance Documentation | "post-market", "PMS", "vigilance", "complaint", "MAUDE", "adverse event reporting", "MDR reporting", "safety signal", "surveillance plan", "surveillance report" |
| Digital Health Regulatory / Content | "SaMD", "digital health", "connected device", "RPM", "remote patient monitoring", "AI in healthcare", "digital therapeutics", "clinical software", "health tech regulatory" |

**Deprioritization signals (down-rank or exclude):**
- Software/product engineering roles (even at healthcare companies)
- Pure AI/ML engineering, data science, model training roles
- Generic operations without regulatory/quality/documentation focus
- Generic content marketing or copywriting without regulated/scientific context
- Senior Director / VP / Head of Regulatory Strategy (too senior for candidate level)
- CRA / clinical monitoring roles (field-based, not documentation)
- Sales, BD, or commercial roles

After detecting archetype, read `modes/_profile.md` for the user's specific framing and proof points for that archetype.

## Global Rules

### NEVER

1. Invent experience or metrics
2. Modify cv.md or portfolio files
3. Submit applications on behalf of the candidate
4. Share phone number in generated messages
5. Recommend comp below market rate
6. Generate a PDF without reading the JD first
7. Use corporate-speak
8. Ignore the tracker (every evaluated offer gets registered)

### ALWAYS

0. **Cover letter:** If the form allows it, ALWAYS include one. Same visual design as CV. JD quotes mapped to proof points. 1 page max.
1. Read cv.md, _profile.md, and article-digest.md (if exists) before evaluating
1b. **First evaluation of each session:** Run `node cv-sync-check.mjs`. If warnings, notify user.
2. Detect the role archetype and adapt framing per _profile.md
3. Cite exact lines from CV when matching
4. Use WebSearch for comp and company data
5. Register in tracker after evaluating
6. Generate content in the language of the JD (EN default)
7. Be direct and actionable -- no fluff
8. Native tech English for generated text. Short sentences, action verbs, no passive voice.
8b. Case study URLs in PDF Professional Summary (recruiter may only read this).
9. **Tracker additions as TSV** -- NEVER edit applications.md directly. Write TSV in `batch/tracker-additions/`.
10. **Include `**URL:**` in every report header.**

### Tools

| Tool | Use |
|------|-----|
| WebSearch | Comp research, trends, company culture, LinkedIn contacts, fallback for JDs |
| WebFetch | Fallback for extracting JDs from static pages |
| Playwright | Verify offers (browser_navigate + browser_snapshot). **NEVER 2+ agents with Playwright in parallel.** |
| Read | cv.md, _profile.md, article-digest.md, cv-template.html |
| Write | Temporary HTML for PDF, applications.md, reports .md |
| Edit | Update tracker |
| Bash | `node generate-pdf.mjs` |

### Time-to-offer priority
- Working demo + metrics > perfection
- Apply sooner > learn more
- 80/20 approach, timebox everything
