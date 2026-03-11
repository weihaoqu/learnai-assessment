# LearnAI Assessment — Scenario-Based Design (v2)

## Design: Parallel-Form Pre/Post
- **Pre-Test** (before session): S1, S3, S5, S7, S9 — one per category
- **Post-Test** (after session): S2, S4, S6, S8, S10 — different scenarios, same categories
- Different scenarios eliminate memory effect after ~50 min LAI session

## Scoring Logic
Each scenario has 4 choices mapped to mastery levels 1-4.
Per test: 5 scenarios × 4 points max = **20 points**.

| Points | Level | Label | Description |
|---|---|---|---|
| 1 | L1 | Passive Consumer | Treats AI as magic oracle, no planning/verification |
| 2 | L2 | Developing User | Some awareness, falls back on workarounds |
| 3 | L3 | Proficient Creator | Good instincts, somewhat vague execution |
| 4 | L4 | Process Partner | Defines problem, picks tools, specific prompts, verifies |

| Score Range | Level | Interpretation |
|---|---|---|
| 5-9 | L1: Passive Consumer | Needs foundational AI literacy |
| 10-13 | L2: Developing User | Has awareness, needs guided practice |
| 14-17 | L3: Proficient Creator | Good grasp, semi-independent |
| 18-20 | L4: Process Partner | Strong mastery, independent workflow |

## Pairing Logic
- Participant IDs auto-generated from timestamp (no manual entry)
- Pre/Post matched by **calendar date** (same session day)
- Gain = Post - Pre. Positive = improvement after LAI session
- Analysis: Wilcoxon signed-rank test + Cohen's d effect size

---

## CATEGORY 1: FIRST INSTINCT (Problem Framing)

### Scenario 1: "The Starting Point"
**Situation:** You want to build a website for your club. What's your first move?

| Choice | Text | Level |
|---|---|---|
| A | Tell AI: "Make me a website" | 1 |
| B | Search Google for a website template | 2 |
| C | Write down what pages you need, who visits, and what they do | 4 |
| D | Ask a friend who knows coding to help | 2 |

### Scenario 2: "The Unclear Request"
**Situation:** Your boss says "Use AI to help with our department data." What do you do first?

| Choice | Text | Level |
|---|---|---|
| A | Upload everything to ChatGPT and say "analyze this" | 1 |
| B | Ask your boss what specific problem they want solved | 4 |
| C | Watch a YouTube tutorial on AI data analysis | 2 |
| D | Try a few different AI tools to see what happens | 3 |

---

## CATEGORY 2: TOOL SELECTION (Tool-Task Mapping)

### Scenario 3: "Right Tool, Right Job"
**Situation:** A nursing professor (no coding experience) wants a newsletter website with login. Best approach?

| Choice | Text | Level |
|---|---|---|
| A | Teach her HTML and CSS first | 1 |
| B | Use a no-code builder like Lovable | 4 |
| C | Ask ChatGPT to write all the code, then figure out hosting | 2 |
| D | Suggest she just use email instead | 1 |

### Scenario 4: "Locked Down"
**Situation:** You need to automate Excel reports at work, but your computer blocks all software installs. What do you use?

| Choice | Text | Level |
|---|---|---|
| A | Give up — you can't use AI without installing software | 1 |
| B | Use Office Copilot or Excel's built-in AI features | 4 |
| C | Do it manually — it's faster than figuring out AI | 2 |
| D | Ask IT to install Python on your machine | 3 |

---

## CATEGORY 3: PROMPT CRAFT (Prompt Engineering)

### Scenario 5: "The Prompt Upgrade"
**Situation:** You asked AI: "Make me a quiz app" and got a basic, ugly result. What do you do next?

| Choice | Text | Level |
|---|---|---|
| A | Ask: "Make it better" | 1 |
| B | Ask: "Add 10 questions about biology with a timer and score tracking. Use a clean blue theme." | 4 |
| C | Try a completely different AI tool | 2 |
| D | Ask: "Make it look nicer and add more features" | 3 |

### Scenario 6: "The Conversation"
**Situation:** You're building an app and AI's output is 80% right but has wrong colors and missing a button. Best next prompt?

| Choice | Text | Level |
|---|---|---|
| A | Start over with a new prompt from scratch | 1 |
| B | "Fix it" | 1 |
| C | "Change the header to navy blue (#001f3f), and add a 'Back' button in the top-left that returns to the home page" | 4 |
| D | "The colors are wrong and there's a missing button, please fix" | 3 |

---

## CATEGORY 4: VERIFICATION (Catching Errors)

### Scenario 7: "Trust but Verify"
**Situation:** AI generated a working web app for you. Before sharing it with others, you should...

| Choice | Text | Level |
|---|---|---|
| A | Share it immediately — it works! | 1 |
| B | Test it on your phone and computer, check all buttons and links | 4 |
| C | Ask AI "Is this code safe and correct?" | 2 |
| D | Have a friend look at it quickly | 3 |

### Scenario 8: "The Hallucination"
**Situation:** You asked AI to write about your university's grading policy. It produced a confident, well-written paragraph. You should...

| Choice | Text | Level |
|---|---|---|
| A | Use it — AI is usually accurate about factual information | 1 |
| B | Check every claim against the actual university policy document | 4 |
| C | Ask AI: "Are you sure this is correct?" | 2 |
| D | Use it but add a disclaimer that it was AI-generated | 2 |

---

## CATEGORY 5: MINDSET & INDEPENDENCE (Oracle → Process Partner)

### Scenario 9: "After the Session"
**Situation:** You just built an email tool with a tutor's help using AI. Now you want to build a personal budget tracker. What do you do?

| Choice | Text | Level |
|---|---|---|
| A | Book another session — I can't do it alone | 2 |
| B | Follow the same workflow: define requirements → pick tools → prompt → verify → deploy | 4 |
| C | Ask AI to "make me a budget tracker" and see what happens | 1 |
| D | Search for an existing budget app instead of building one | 2 |

### Scenario 10: "The Role of AI"
**Situation:** You just finished building a portfolio website using AI tools. Someone asks: "Did AI do all the work?" Best answer?

| Choice | Text | Level |
|---|---|---|
| A | "Yes, AI built the whole thing for me" | 1 |
| B | "I designed the requirements, chose the tools, wrote the prompts, verified the output, and deployed it. AI generated the code." | 4 |
| C | "It's a team effort — me and AI together" | 3 |
| D | "No, I did it all myself" (hides AI use) | 1 |
