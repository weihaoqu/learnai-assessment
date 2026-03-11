# LearnAI Assessment Tool — Project Specification

## Initial Idea
Design objective, performance-based assessment instruments to directly measure client learning in the LearnAI Framework study. The current paper was rejected from ITiCSE 2026 primarily because it lacked direct measures of learning — only self-report satisfaction ratings (5/5 stars) and confidence scales. The goal is to create a short, gamified, drag-and-drop web assessment that tests knowledge and skills related to problem framing, tool-task mapping, prompt engineering, and output verification. Administered identically pre/post during Layer 2 co-creation sessions. Results provide paired, objective evidence of learning gain.

---

## 1. Overview

### Problem
The LearnAI paper was rejected from ITiCSE 2026. The #1 reviewer complaint: **"No direct measure of learning."** The existing data consists of:
- 5/5 satisfaction ratings (uniformly positive, analytically useless)
- Self-reported confidence (subjective, not a learning measure)
- Artifacts (evidence of output, not evidence of skill acquisition)

### Goal
Build a **3-minute, 4-question visual matching/sorting assessment** that objectively measures whether clients gained skills during a co-creation session. The same instrument is administered before and after the session, producing paired scores that can be analyzed with standard statistical tests.

### How This Fixes the Reviewer Complaint
| Reviewer said | This tool provides |
|---|---|
| "No direct measure of learning" | Performance-based pre/post scores on 4 skills |
| "Uniformly positive feedback" | Objective scores with variance (0-4 scale per skill) |
| "Claims about cognitive shift not supported" | Measurable improvement in problem framing & verification |
| "Self-selected, no real analysis" | Paired Wilcoxon signed-rank test with effect sizes |

---

## 2. Assessment Design

### Structure
- **When:** Pre-test before session starts, post-test immediately after session ends
- **Duration:** ~3 minutes each (6 minutes total)
- **Format:** 4 visual drag-and-drop matching/sorting tasks + 1 Likert scale + 1 open-ended question
- **Pre/Post design:** Identical questions both times
- **Rationale for identical:** With N≈25, statistical power is limited. Identical items enable clean paired analysis. Memory effect is minimal because (1) 50+ minutes separate the tests, (2) matching tasks are harder to memorize than MCQs, and (3) this is standard practice in computing education research.

### Skills Measured (Mapped to 5-Stage Pedagogical Script)

| Question | Skill | Stage | Task Type |
|---|---|---|---|
| Q1 | Problem Framing | Stage 1 | Match vague requests → decomposed specs |
| Q2 | Tool-Task Mapping | Stage 2 | Match tasks+constraints → best AI tool |
| Q3 | Prompt Quality | Stage 3 | Rank 4 prompts from weakest → strongest |
| Q4 | Verification | Stage 4 | Identify which AI outputs contain errors |

### Additional Items (Post-Test Only After Score Display)
| Item | Type | Purpose |
|---|---|---|
| Q5 | Likert 1-5 | "How confident are you using AI independently now?" |
| Q6 | Open text (1-2 sentences) | "What was the most useful thing you learned today?" |

### Demographic Item (Pre-Test Only)
| Item | Type | Purpose |
|---|---|---|
| D1 | 4-option single select | Coding background: None / Beginner / Intermediate / Advanced |

---

## 3. Question Specifications

### Q1: Problem Framing (Match)
**Instruction:** "Match each vague request to its properly decomposed specification."

**Left column (vague requests):**
1. "I need a website for my department"
2. "Can AI help me with my data?"
3. "I want to automate my emails"
4. "Make me an app for my class"

**Right column (decomposed specs) — shuffled:**
- A. "Build a responsive site with faculty profiles, news feed, and contact form; host on university domain with SSO login"
- B. "Clean CSV export of 500 student records: remove duplicates, standardize date formats, flag missing fields"
- C. "Auto-draft reply templates for 3 common inquiry types; human reviews before sending; integrate with Outlook"
- D. "Create a QR-based attendance tracker with role-based access, real-time dashboard, and CSV export for 5 course sections"

**Correct matches:** 1→A, 2→B, 3→C, 4→D

**Scoring:** 1 point per correct match (0-4 scale)

**Post-test explanation:** "Good problem framing means translating a vague need into specific requirements — who uses it, what it does, what constraints exist. This is the most critical step before touching any AI tool."

---

### Q2: Tool-Task Mapping (Match)
**Instruction:** "Match each task and constraint to the best AI tool."

**Left column (tasks + constraints):**
1. "Build a portfolio site quickly, no coding experience, needs to look professional"
2. "Generate and debug Python scripts for data analysis with full control over code"
3. "Deploy a web app with authentication and a database backend"
4. "Automate spreadsheet workflows on a locked-down work computer (no software installs allowed)"

**Right column (tools) — shuffled:**
- A. Lovable (no-code builder)
- B. Claude / ChatGPT (general-purpose LLM)
- C. Claude + Vercel + Supabase (LLM + deployment + database)
- D. Office Copilot (enterprise AI, runs in browser)

**Correct matches:** 1→A, 2→B, 3→C, 4→D

**Scoring:** 1 point per correct match (0-4 scale)

**Post-test explanation:** "Different tools have different strengths. No-code builders are fastest for visual projects. LLMs give you code control. Deployment platforms handle hosting. Enterprise tools work within IT restrictions. Choosing the right tool for the job is a core AI literacy skill."

---

### Q3: Prompt Quality (Rank/Sort)
**Instruction:** "Drag these 4 prompts into order from WEAKEST to STRONGEST for building a class attendance tracker."

**Prompts (presented in random order):**
1. **Weakest:** "Make me an attendance app"
2. **Weak:** "Build a web app where students can check in to class"
3. **Strong:** "Build a web-based attendance tracker where students scan a QR code to check in. Each class session generates a unique QR. Teachers see a real-time dashboard."
4. **Strongest:** "Build a web-based attendance tracker with these requirements: (1) Unique QR code per class session that expires after 15 minutes, (2) Student login via university SSO, (3) Teacher dashboard showing real-time check-ins with timestamps, (4) CSV export of attendance records per course section, (5) Mobile-responsive design. Tech stack: Next.js frontend, Supabase backend, deploy to Vercel."

**Correct order:** 1 → 2 → 3 → 4

**Scoring:** Kendall's tau or simple adjacency scoring:
- All 4 in correct order: 4 points
- 3 in correct relative order: 3 points
- 2 in correct relative order: 2 points
- 1 or 0 correct: 1 or 0 points

(Implementation: count the number of correctly ordered pairs out of 6 possible pairs, map to 0-4 scale)

**Post-test explanation:** "Effective prompts are specific, structured, and include requirements, constraints, and technical details. Think of prompting as writing a specification — the more precise your spec, the better the AI's output."

---

### Q4: Verification & Hallucination Detection (Identify)
**Instruction:** "You asked AI to build a student grade calculator. Review these 4 outputs. Drag the ones that contain errors or hallucinations to the 'Problems Found' zone."

**Output snippets:**
1. **Has error:** Code calculates average but divides by a hardcoded `5` instead of the actual number of assignments. *(Logic bug — AI assumed fixed count)*
2. **Correct:** Code properly validates input, calculates weighted average, and handles edge case of zero assignments.
3. **Has error:** AI claims "This code uses the university's official grading API to submit grades directly." *(Hallucination — no such API was mentioned or exists)*
4. **Has error:** Code looks correct but stores student grades in a publicly accessible URL with no authentication. *(Security flaw)*

**Correct answer:** Items 1, 3, 4 should be in "Problems Found." Item 2 is correct.

**Scoring:**
- Correctly categorize all 4: 4 points
- 3 correct: 3 points
- 2 correct: 2 points
- 1 correct: 1 point
- 0 correct: 0 points

**Post-test explanation:** "AI outputs can contain logic bugs (wrong assumptions), hallucinations (fabricated facts), and security flaws (missing protections). Always verify: check the logic, question claims about external systems, and review security before deploying."

---

## 4. Scoring System

### Per-Question Scoring
Each question scores 0-4 points. Total possible: **16 points**.

### Composite Score
| Score Range | Label |
|---|---|
| 0-4 | Novice |
| 5-8 | Developing |
| 9-12 | Proficient |
| 13-16 | Expert |

### Post-Test Feedback Display
After completing the post-test, the client sees:

```
Your Results
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Overall: 12/16 — Proficient

Problem Framing:    ████░  3/4
Tool Mapping:       █████  4/4
Prompt Quality:     ███░░  3/4
Verification:       ██░░░  2/4

[Brief explanation for each question shown below]
```

The pre-test does NOT show feedback — only records answers silently.

### Pre/Post Comparison (For Research, Not Shown to Client)
Data exported to Google Sheets includes:
- Session booking ID
- Coding background (None/Beginner/Intermediate/Advanced)
- Timestamp
- Test type (pre/post)
- Q1-Q4 individual scores
- Total score
- Q5 Likert response (post only)
- Q6 open text (post only)

---

## 5. Technical Architecture

### Stack
- **Frontend:** Single self-contained HTML file with vanilla JS + CSS
- **Drag-and-drop:** HTML5 Drag and Drop API (with touch support for mobile via a polyfill or pointer events)
- **Backend:** None — data submission via Google Apps Script web endpoint
- **Data storage:** Google Sheets (one sheet for pre-test, one for post-test, paired by booking ID)
- **Hosting:** Can be served from any static host (GitHub Pages, Vercel, or even opened as a local file)

### Why Single HTML File
- Zero dependencies, zero build step
- Works offline (except for data submission)
- Easy for the tutor team to deploy — just share a URL or QR code
- Can be versioned in Git as a single file

### Google Apps Script Endpoint
```
POST https://script.google.com/macros/s/{SCRIPT_ID}/exec
Content-Type: application/json

{
  "booking_id": "LEA-047",
  "test_type": "pre",
  "coding_background": "Beginner",
  "timestamp": "2026-03-15T14:30:00Z",
  "q1_score": 3,
  "q1_answers": {"1":"A", "2":"B", "3":"C", "4":"D"},
  "q2_score": 4,
  "q2_answers": {"1":"A", "2":"B", "3":"C", "4":"D"},
  "q3_score": 4,
  "q3_order": [1, 2, 3, 4],
  "q4_score": 3,
  "q4_answers": {"1":"problem", "2":"correct", "3":"problem", "4":"correct"},
  "total_score": 14,
  "q5_likert": null,
  "q6_open": null
}
```

### Mobile Support
- Mobile-first responsive design
- Touch-friendly drag targets (minimum 44px hit area)
- Fallback: tap-to-select + tap-to-place for devices where drag is awkward
- Tested on iPhone Safari + Android Chrome

---

## 6. Visual Design

### Style: Gamified & Playful
- **Colors:** Bright, friendly palette — teal/blue primary, warm accent colors for feedback
- **Progress bar:** Shows Q1/Q2/Q3/Q4 progress at the top
- **Animations:**
  - Smooth drag-and-drop with snap-to-target
  - Correct match: subtle green glow + checkmark animation
  - Score reveal: animated counter that counts up (post-test only)
- **Cards:** Rounded corners, light shadows, clear visual hierarchy
- **Typography:** Clean sans-serif (system font stack), large enough for phone screens

### Layout
```
┌──────────────────────────────────────┐
│  LearnAI Assessment    [Q2 of 4]     │
│  ━━━━━━━━━━░░░░░░  (progress bar)    │
├──────────────────────────────────────┤
│                                      │
│  Match each task to the best tool:   │
│                                      │
│  ┌─────────────┐   ┌─────────────┐   │
│  │ Task Card 1 │──▶│ Tool Card A │   │
│  └─────────────┘   └─────────────┘   │
│  ┌─────────────┐   ┌─────────────┐   │
│  │ Task Card 2 │   │ Tool Card B │   │
│  └─────────────┘   └─────────────┘   │
│  ┌─────────────┐   ┌─────────────┐   │
│  │ Task Card 3 │   │ Tool Card C │   │
│  └─────────────┘   └─────────────┘   │
│  ┌─────────────┐   ┌─────────────┐   │
│  │ Task Card 4 │   │ Tool Card D │   │
│  └─────────────┘   └─────────────┘   │
│                                      │
│           [ Next → ]                 │
└──────────────────────────────────────┘
```

### Post-Test Results Screen
```
┌──────────────────────────────────────┐
│        🎯 Your Results               │
│                                      │
│    ┌────────────────────────┐        │
│    │   12 / 16              │        │
│    │   ██████████████░░░░   │        │
│    │   Proficient           │        │
│    └────────────────────────┘        │
│                                      │
│  Problem Framing    ████░  3/4       │
│  Tool Mapping       █████  4/4       │
│  Prompt Quality     ███░░  3/4       │
│  Verification       ██░░░  2/4       │
│                                      │
│  ▼ See explanations                  │
│  [expandable section per question]   │
│                                      │
│  ─────────────────────────────────   │
│  How confident are you using AI      │
│  independently now?                  │
│  ① ② ③ ④ ⑤                          │
│                                      │
│  What was the most useful thing      │
│  you learned today?                  │
│  ┌──────────────────────────┐        │
│  │                          │        │
│  └──────────────────────────┘        │
│                                      │
│           [ Submit ]                 │
└──────────────────────────────────────┘
```

---

## 7. Data Flow

### Pre-Test Flow
```
Client arrives → Tutor shares QR code / URL
→ Client enters Session Booking ID
→ Client selects coding background (None/Beginner/Intermediate/Advanced)
→ Client completes Q1-Q4 (drag-and-drop, ~3 min)
→ Answers submitted silently to Google Sheets (no feedback shown)
→ "Thank you! Your session will begin now."
→ Co-creation session starts
```

### Post-Test Flow
```
Session ends → Tutor says "One last thing — same quick assessment"
→ Client enters Session Booking ID (pre-filled if same device)
→ Client completes Q1-Q4 (identical questions, ~3 min)
→ Score + skill breakdown + explanations displayed
→ Client answers Q5 (Likert confidence) + Q6 (open text)
→ All data submitted to Google Sheets
→ "Thanks for helping us improve! Here's your score summary."
```

### Google Sheets Structure

**Sheet 1: "Pre-Test"**
| booking_id | coding_bg | timestamp | q1 | q2 | q3 | q4 | total |
|---|---|---|---|---|---|---|---|
| LEA-047 | Beginner | 2026-03-15 14:30 | 2 | 1 | 1 | 1 | 5 |

**Sheet 2: "Post-Test"**
| booking_id | timestamp | q1 | q2 | q3 | q4 | total | q5_likert | q6_open |
|---|---|---|---|---|---|---|---|---|
| LEA-047 | 2026-03-15 15:35 | 4 | 3 | 3 | 3 | 13 | 4 | "Learned to decompose my needs before prompting" |

**Sheet 3: "Paired Analysis" (auto-computed)**
| booking_id | coding_bg | pre_total | post_total | gain | q1_gain | q2_gain | q3_gain | q4_gain |
|---|---|---|---|---|---|---|---|---|
| LEA-047 | Beginner | 5 | 13 | +8 | +2 | +2 | +2 | +2 |

---

## 8. Validation Plan

### Phase 1: Expert Review (Days 1-3)
- Share the 4 questions with 2-3 CS education faculty
- Ask them to evaluate:
  - **Content validity:** Do these questions actually measure the claimed skills?
  - **Clarity:** Are the instructions and items unambiguous?
  - **Difficulty:** Are the questions appropriate for the mixed-ability audience (nursing faculty to CS majors)?
  - **Distractors:** Are wrong answers plausibly wrong (not obviously incorrect)?
- Revise based on feedback

### Phase 2: Pilot Test (Days 4-7)
- Run the assessment with 5-8 members of the tutor team
- Measure:
  - **Completion time:** Does it actually take ~3 minutes?
  - **Usability:** Any confusion with drag-and-drop on different devices?
  - **Item analysis:** Are any questions too easy (everyone gets it right) or too hard (everyone gets it wrong)?
  - **Think-aloud:** Ask 2-3 pilot participants to narrate their reasoning while completing
- Revise based on findings

### Phase 3: Deploy (Day 8+)
- Go live with all new Layer 2 sessions
- Monitor first 5 submissions for data quality issues

### Reporting in Paper
In the methodology section, write:
> "The assessment instrument was developed through iterative expert review with [N] computing education faculty and piloted with [N] facilitators. Items were revised based on content validity feedback and pilot usability testing. The final instrument demonstrated face and content validity for the target population."

---

## 9. Research Methodology Notes

### Statistical Analysis Plan
With N≈25 paired observations:

1. **Primary analysis:** Wilcoxon signed-rank test on total pre/post scores
   - Non-parametric (doesn't assume normal distribution, appropriate for small N and ordinal-ish data)
   - Reports: Z statistic, p-value, effect size (r = Z / √N)

2. **Per-skill analysis:** Wilcoxon signed-rank on each Q1-Q4 individually
   - Shows which skills improved most
   - Apply Bonferroni correction for 4 comparisons (α = 0.05/4 = 0.0125)

3. **Effect size:** Report Cohen's d or rank-biserial correlation
   - Small: 0.2, Medium: 0.5, Large: 0.8
   - Even with small N, a large effect size is publishable

4. **Descriptive statistics:**
   - Median and IQR for pre and post scores (overall and per-skill)
   - Bar chart showing pre vs. post for each skill
   - Histogram of gain scores

5. **Exploratory subgroup analysis:**
   - Compare gains by coding background (None/Beginner vs. Intermediate/Advanced)
   - Compare gains by discipline (if sample allows)
   - Note: these are exploratory, not confirmatory — state this clearly

6. **Correlation:**
   - Correlate objective score gain with Q5 subjective confidence
   - If they correlate: strengthens the finding
   - If they don't: interesting in itself (people may learn without feeling confident, or vice versa)

### What to Write in the Paper

**Methodology section:**
> "To address the limitation of self-report measures identified in prior work, we developed a performance-based assessment aligned with the 5-Stage Pedagogical Script. The instrument comprises four drag-and-drop matching tasks measuring problem framing, tool-task mapping, prompt quality evaluation, and output verification. Each task is scored 0-4, yielding a composite score of 0-16. The identical instrument was administered immediately before and after each co-creation session, producing paired observations. Instrument validity was established through expert review by [N] computing education researchers and piloted with [N] facilitators."

**Results section:**
> "Pre/post paired analysis (N=X) using the Wilcoxon signed-rank test revealed a statistically significant increase in total assessment score (Mdn_pre = X, Mdn_post = X, Z = X, p = X, r = X). Per-skill analysis showed the largest gains in [skill] (Mdn gain = X) and [skill] (Mdn gain = X)."

---

## 10. Implementation Timeline

```
Day 1 (Today)    → Build the HTML assessment tool (all 4 questions + scoring + Google Sheets integration)
Day 2            → Test on mobile + desktop, fix drag-and-drop edge cases
Day 3            → Send to 2-3 CS education faculty for expert review
Day 4-5          → Incorporate expert feedback, revise questions
Day 6            → Pilot with 5-8 tutors, collect timing + usability data
Day 7            → Final revisions based on pilot
Day 8+           → Deploy to all new Layer 2 co-creation sessions
Ongoing          → Monitor data quality, pair pre/post in Google Sheets
```

### Parallel Track
While the tool is being reviewed/piloted:
- Continue all other data collection from the LearnAI Team Plan (follow-up emails, Layer 1 QR surveys, tutor write-ups)
- The assessment tool is one piece of the larger data collection strategy

---

## 11. Success Criteria

| Metric | Target |
|---|---|
| Completion time | ≤ 3 minutes per test |
| Completion rate | ≥ 90% of clients who start finish the assessment |
| Paired responses | ≥ 20 pairs (minimum for publishable analysis) |
| Pre/post score difference | Statistically significant (p < 0.05) on Wilcoxon |
| Effect size | Medium or large (r ≥ 0.3) |
| Mobile usability | Works on iPhone Safari + Android Chrome without issues |
| Data quality | < 5% missing or malformed submissions |

---

## 12. Open Questions

1. **Exact tool names in Q2:** Should we include specific tool versions (e.g., "Claude 3.5 Sonnet") or just brand names ("Claude")? → Probably just brand names for longevity.
2. **Q3 scoring nuance:** The Kendall's tau approach vs. simple "number of correct adjacent pairs" — need to decide during implementation.
3. **Accessibility:** Should we provide a non-drag-and-drop fallback (dropdown menus) for accessibility? → Yes, include as progressive enhancement.
4. **Language:** Is the assessment in English only, or do any clients need other languages? → Assume English for now.
5. **IRB amendment:** Does adding this new instrument require an IRB amendment or is it covered under the existing protocol? → Check with research lead immediately.
