# Mode: deep — Deep Research Prompt

Generates a structured prompt for Perplexity/Claude/ChatGPT with 6 axes:

```
## Deep Research: [Company] — [Role]

Context: I am evaluating an application for [role] at [company]. I need actionable information for the interview.

### 1. Regulatory and Quality Landscape
- What products/services does this company have under regulatory oversight?
- What regulatory frameworks apply (FDA, EU MDR, ICH, etc.)?
- Do they have FDA clearances/approvals? 510(k)s? PMA? De Novo?
- What does their quality system look like? Any FDA warning letters or recalls?
- Do they have a medical writing or regulatory affairs team?

### 2. Recent Moves (last 6 months)
- Relevant hires in regulatory, quality, medical writing, or clinical?
- Acquisitions or partnerships?
- Product launches, FDA submissions, or regulatory milestones?
- Funding rounds or leadership changes?

### 3. Company Culture and Team
- How do they ship? (regulated cadence, design controls, etc.)
- What documentation systems do they use? (Veeva, MasterControl, etc.)
- Remote-first or office-first?
- Glassdoor/Blind reviews about quality/regulatory culture?

### 4. Likely Challenges
- What regulatory challenges are they facing?
- Any compliance issues, warning letters, or audit findings?
- Are they expanding into new markets (EU, APAC)?
- What pain points do people mention in reviews?

### 5. Competitors and Differentiation
- Who are their main competitors?
- What is their moat/differentiator?
- How do they position vs competition?

### 6. Candidate Angle
Given my profile (read from cv.md and profile.yml for specific experience):
- What unique value do I bring to this team?
- Which of my projects are most relevant?
- What story should I tell in the interview?
```

Customize each section with the specific context of the evaluated offer.
