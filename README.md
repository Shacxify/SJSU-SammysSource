# SJSU Student Resource Navigator
### AI for Social Good | BUS4-110A | Spring 2026

**SDGs:** No Poverty (1) · Quality Education (4)
**AI Capability:** Text Generation
**Stack:** Python · Google Gemini API · Google Colab

---

## Problem

First-gen SJSU students in financial crisis can't navigate the system fast enough to get help before deadlines hit.

Here's the exact breakdown: a student gets a financial hold two weeks before fall registration closes. She's working 20 hours a week, her family earns under $40k, and her FAFSA hasn't disbursed yet. The answer exists somewhere on the SJSU website — spread across six departments, written in administrative language, with no clear path to action. She opens the Student Financial Services page, sees twelve programs, and closes the tab.

That's the failure point. Not missing information. Inaccessible information at the worst possible moment.

---

## AI Capability

Text generation (Lab 1) bridges the gap between a stressed student's plain-language description of their situation and a specific, ranked action plan.

The system prompt is the policy layer. One instruction determines whether the tool works for everyone or just students who already know how to navigate the system. Lab 1 proved this — a single line decided whether the 311 civic tool could serve Spanish, Vietnamese, and Cantonese speakers at all. Same principle applies here.

Text generation was chosen over structured extraction (Lab 2) because students in crisis don't fill out forms accurately under stress. They describe. The tool meets them where they are.

---

## Workflow
Student types situation in plain language
↓
Gemini reads input against system prompt
(7 SJSU resources, ranked by urgency)
↓
Returns 1-3 recommendations under 200 words
in the student's own language
↓
Peer advisor reviews flagged inputs before delivery
(non-English or vague messages)
↓
Student gets a specific next step, not a list of links

**What goes in:** Free-text description — no fields, no categories, no forms.

**What the AI does:** Matches the situation to the most relevant SJSU resources, ranks by urgency, gives specific actions — where to go, who to contact, what to bring.

**What comes out:** A response under 200 words in the student's language, ending with acknowledgment of their situation.

**Who acts on it:** A Basic Needs Center peer advisor reviews anything vague or non-English before it reaches the student. Everything else delivers directly.

![Test Case 1 — Financial Hold](screenshots/test1.png)
![Edge Case — Spanish Input Comparison](screenshots/edge_case.png)

---

## Failure Case

**The input:** A Spanish-speaking student sends a vague distress message with no specific detail about what kind of help she needs.
"Hola, necesito ayuda. No tengo dinero y no sé qué hacer.
Estoy en la universidad pero no entiendo los recursos."
**What Gemini returned:** [paste actual Cell 9 output here]

**The real-world consequence:** The system responds in English. The student can't act on it. She misses the Fee Deferral Program deadline. Her hold stays. She can't register for the following semester. The student the tool was built for is the first one it fails.

**The lab connection:** Lab 1 showed that a missing line in the system prompt locks out an entire population. When input is vague and non-English, the model either guesses wrong or defaults to English — same dynamic, different stakes.

---

## Oversight and Tradeoff

**Where human review sits:** Any response going to a student who wrote in a non-English language or sent a message too vague to route accurately gets held for peer advisor review at the Basic Needs Center before delivery.

**The one change:** A language detection instruction was added to the system prompt. Gemini now responds in the student's language and asks one clarifying question instead of guessing when input is unclear. Demonstrated in the notebook by re-running the same edge case against both prompts.

**What it costs:** Speed. Vague or non-English inputs now trigger a review queue — 4 to 24 hours depending on staffing. For a student with a registration deadline in two days, that's a real tradeoff. A wrong recommendation delivered instantly does more damage than a correct one delivered the next morning.

---

## Team

Built for BUS4-110A: Fundamentals of MIS · SJSU Lucas College of Business · Spring 2026
