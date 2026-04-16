# Mode: pdf — ATS-Optimized PDF Generation

## Full Pipeline

1. Read `cv.md` as source of truth
2. Ask the user for the JD if not in context (text or URL)
3. Extract 15-20 keywords from the JD
4. Detect JD language → CV language (EN default)
5. Detect company location → paper format:
   - US/Canada → `letter`
   - Rest of world → `a4`
6. Detect role archetype → adapt framing
7. Rewrite Professional Summary injecting JD keywords + exit narrative bridge ("Regulatory affairs trained medical writer bridging clinical writing, quality rigor, and submission-ready documentation in [JD domain].")
8. Select top 3-4 most relevant projects for the offer
9. Reorder experience bullets by relevance to JD
10. Build competency grid from JD requirements (6-8 keyword phrases)
11. Inject keywords naturally into existing achievements (NEVER invent)
12. Generate complete HTML from template + personalized content
13. Write HTML to `/tmp/cv-candidate-{company}.html`
14. Execute: `node generate-pdf.mjs /tmp/cv-candidate-{company}.html output/cv-candidate-{company}-{YYYY-MM-DD}.pdf --format={letter|a4}`
15. Report: PDF path, number of pages, % keyword coverage

## ATS Rules (clean parsing)

- Single-column layout (no sidebars, no parallel columns)
- Standard headers: "Professional Summary", "Work Experience", "Education", "Skills", "Certifications", "Projects"
- No text in images/SVGs
- No critical info in PDF headers/footers (ATS ignores them)
- UTF-8, selectable text (not rasterized)
- No nested tables
- JD keywords distributed: Summary (top 5), first bullet of each role, Skills section

## PDF Design

- **Fonts**: Space Grotesk (headings, 600-700) + DM Sans (body, 400-500)
- **Fonts self-hosted**: `fonts/`
- **Header**: name in Space Grotesk 24px bold + gradient line `linear-gradient(to right, hsl(187,74%,32%), hsl(270,70%,45%))` 2px + contact row
- **Section headers**: Space Grotesk 13px, uppercase, letter-spacing 0.05em, cyan primary color
- **Body**: DM Sans 11px, line-height 1.5
- **Company names**: accent purple color `hsl(270,70%,45%)`
- **Margins**: 0.6in
- **Background**: pure white

## Section Order (optimized for "6-second recruiter scan")

1. Header (large name, gradient, contact, portfolio link)
2. Professional Summary (3-4 lines, keyword-dense — bridge regulatory + writing + quality)
3. Core Competencies (6-8 keyword phrases in flex-grid — tailor per archetype)
4. Work Experience (reverse chronological — reorder bullets per JD relevance)
5. Projects (top 3-4 most relevant to detected archetype)
6. Education & Certifications (M.S. Regulatory Affairs prominently — key differentiator)
7. Skills (regulatory tools, documentation tools, frameworks, languages)

**Archetype-specific competency grid examples:**
- Regulatory Affairs: CTD/eCTD, Regulatory Submissions, 510(k) Support, FDA 21 CFR, EU MDR, Regulatory Intelligence, Dossier Organization, Labeling
- Medical Writing: ICF Authoring, Protocol Writing, Safety Narratives, Plain-Language Communication, Literature Review, Scientific Communication
- QA Documentation: CAPA Documentation, SOP Writing, Root Cause Analysis, Document Control, Change Control, Audit Readiness, ISO 14971
- Submission Support: eCTD Publishing, Cross-Functional Coordination, Submission Tracking, Dossier Assembly, Regulatory Project Management
- PMS Documentation: Post-Market Surveillance, MAUDE Analysis, Complaint Documentation, Safety Signals, Vigilance Reporting, Risk Narratives
- Digital Health: SaMD Regulatory, RPM Documentation, Digital Health Content, Patient Education, Connected Device Labeling

## Keyword Injection Strategy (ethical, truth-based)

Legitimate reformulation examples:
- JD says "regulatory submissions" and CV says "organized technical documentation for submission workflows" → change to "regulatory submission support including dossier organization and cross-functional coordination"
- JD says "CAPA management" and CV says "documented corrective actions that reduced repeat deviations" → change to "CAPA documentation and corrective action tracking with root cause analysis (5 Whys, Fishbone)"
- JD says "medical writing" and CV says "drafted clinical research communications" → change to "medical writing across clinical communications, safety narratives, and regulatory content"
- JD says "document control" and CV says "maintained controlled document states and trackers" → change to "document control including version management, change control support, and audit-ready documentation"
- JD says "post-market surveillance" and CV says "authored post-market reports" → change to "post-market surveillance documentation including PMS plans, safety summaries, and MAUDE data synthesis"

**NEVER add skills the candidate does not have. Only reformulate real experience with the exact vocabulary of the JD.**

## HTML Template

Use the template in `cv-template.html`. Replace the `{{...}}` placeholders with personalized content:

| Placeholder | Content |
|-------------|---------|
| `{{LANG}}` | `en` |
| `{{PAGE_WIDTH}}` | `8.5in` (letter) or `210mm` (A4) |
| `{{NAME}}` | (from profile.yml) |
| `{{EMAIL}}` | (from profile.yml) |
| `{{LINKEDIN_URL}}` | (from profile.yml) |
| `{{LINKEDIN_DISPLAY}}` | (from profile.yml) |
| `{{PORTFOLIO_URL}}` | (from profile.yml) |
| `{{PORTFOLIO_DISPLAY}}` | (from profile.yml) |
| `{{LOCATION}}` | (from profile.yml) |
| `{{SECTION_SUMMARY}}` | Professional Summary |
| `{{SUMMARY_TEXT}}` | Personalized summary with keywords |
| `{{SECTION_COMPETENCIES}}` | Core Competencies |
| `{{COMPETENCIES}}` | `<span class="competency-tag">keyword</span>` × 6-8 |
| `{{SECTION_EXPERIENCE}}` | Work Experience |
| `{{EXPERIENCE}}` | HTML of each job with reordered bullets |
| `{{SECTION_PROJECTS}}` | Projects |
| `{{PROJECTS}}` | HTML of top 3-4 projects |
| `{{SECTION_EDUCATION}}` | Education |
| `{{EDUCATION}}` | HTML of education |
| `{{SECTION_CERTIFICATIONS}}` | Certifications |
| `{{CERTIFICATIONS}}` | HTML of certifications |
| `{{SECTION_SKILLS}}` | Skills |
| `{{SKILLS}}` | HTML of skills |

## Post-Generation

Update tracker if the offer is already registered: change PDF from ❌ to ✅.
