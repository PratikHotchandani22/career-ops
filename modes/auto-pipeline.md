# Mode: auto-pipeline — Full Automatic Pipeline

## OUTPUT RULE: Be extremely brief. Do all work internally (evaluation, PDF, tracker). Show the user ONLY the compact summary from oferta.md "User-Facing Output" section. Never narrate the process.

When the user pastes a JD (text or URL) without an explicit sub-command, run the ENTIRE pipeline in sequence:

## Step 0 — Extract JD

If the input is a **URL** (not pasted JD text), follow this strategy to extract the content:

**Priority order:**

1. **Playwright (preferred):** Most job portals (Lever, Ashby, Greenhouse, Workday) are SPAs. Use `browser_navigate` + `browser_snapshot` to render and read the JD.
2. **WebFetch (fallback):** For static pages (ZipRecruiter, WeLoveProduct, company career pages).
3. **WebSearch (last resort):** Search the role title + company on secondary portals that index the JD in static HTML.

**If no method works:** Ask the candidate to paste the JD manually or share a screenshot.

**If the input is JD text** (not a URL): use directly, no fetch needed.

## Step 1 — Evaluation A-F
Run exactly as in the `oferta` mode (read `modes/oferta.md` for all blocks A-F).

## Step 2 — Save Report .md
Save the complete evaluation to `reports/{###}-{company-slug}-{YYYY-MM-DD}.md` (see format in `modes/oferta.md`).

## Step 3 — Generate PDF
Run the complete `pdf` pipeline (read `modes/pdf.md`).

## Step 4 — Draft Application Answers (only if score >= 4.5)

If the final score is >= 4.5, generate draft answers for the application form:

1. **Extract form questions**: Use Playwright to navigate to the form and take a snapshot. If extraction fails, use generic questions.
2. **Generate answers** following the tone (see below).
3. **Save in the report** as section `## G) Draft Application Answers`.

### Generic questions (use if form questions cannot be extracted)

- Why are you interested in this role?
- Why do you want to work at [Company]?
- Tell us about a relevant project or achievement
- What makes you a good fit for this position?
- How did you hear about this role?

### Tone for Form Answers

**Positioning: "I'm choosing you."** The candidate has options and is choosing this company for concrete reasons.

**Tone rules:**
- **Confident without arrogance**: "I've spent the past year building regulatory documentation across FDA and EU MDR frameworks — your role is where I want to apply that experience next"
- **Selective without conceit**: "I've been intentional about finding a team where I can contribute meaningfully from day one"
- **Specific and concrete**: Always reference something REAL from the JD or the company, and something REAL from the candidate's experience
- **Direct, no fluff**: 2-4 sentences per answer. No "I'm passionate about..." or "I would love the opportunity to..."
- **The hook is the proof, not the claim**: Instead of "I'm great at X", say "I authored X that achieved Y"

**Framework per question:**
- **Why this role?** → "Your [specific thing] maps directly to [specific thing I've done]."
- **Why this company?** → Mention something concrete about the company. "I've been following [company's work in X area]."
- **Relevant experience?** → A quantified proof point. "Authored PMS plans and safety summaries aligned to FDA and EU MDR at a medtech company."
- **Good fit?** → "I sit at the intersection of [A] and [B], which is exactly where this role lives."
- **How did you hear?** → Honest: "Found through [portal/scan], evaluated against my criteria, and it scored highest."

**Language**: Always in the language of the JD (EN default).

## Step 5 — Update Tracker
Register in `data/applications.md` with all columns including Report and PDF as ✅.

**If any step fails**, continue with the remaining steps and mark the failed step as pending in the tracker.

## User-Facing Output

After all steps complete, show ONLY the compact summary (see `modes/oferta.md` "User-Facing Output" section). Do not print step-by-step progress. Do not print the full evaluation blocks. Just the score card + verdict + PDF/report paths.
