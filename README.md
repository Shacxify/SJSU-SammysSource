# Sammy's Source

### SJSU Student Resource Navigator · AI for Social Good · BUS4-110A · Spring 2026

> Built for the student who has 48 hours before registration closes, a financial hold on her account, and no idea which office to call first.

![Python](https://img.shields.io/badge/Python-3.12-blue?style=flat-square&logo=python)
![Gemini](https://img.shields.io/badge/Google-Gemini_API-orange?style=flat-square&logo=google)
![Colab](https://img.shields.io/badge/Google-Colab-yellow?style=flat-square&logo=googlecolab)
![SDG1](https://img.shields.io/badge/SDG-No_Poverty-red?style=flat-square)
![SDG4](https://img.shields.io/badge/SDG-Quality_Education-darkred?style=flat-square)

---

## The Problem

SJSU has the resources. Students in crisis cannot find them fast enough.

A first-generation student gets a financial hold two weeks before fall registration closes. She works 20 hours a week, her family earns under $40k, her FAFSA has not disbursed, and the clock is running. The answer is somewhere on the SJSU website, buried across six departments, written for administrators rather than students. She opens Student Financial Services, sees twelve programs with overlapping eligibility requirements, and closes the tab.

That is the moment Sammy's Source is built for. Not the student who knows how to navigate the system. The one who does not, and cannot afford to figure it out.

**The failure:** information exists but cannot be understood or acted on under pressure. That gap costs students their semester.

---

## How It Works

    Student describes the situation in plain language
                        ↓
          Sammy's Source reads it against the system prompt
           (7 SJSU resources, prioritized by urgency)
                        ↓
          1 to 3 recommendations returned under 200 words
                 in the student's own language
                        ↓
          Flagged inputs held for peer advisor review
            (non-English or too vague to route)
                        ↓
       Student receives a next step, not another list of links

| Stage | Detail |
|---|---|
| **Input** | Plain-language description. No forms, no fields, no categories. |
| **AI step** | Matches the situation to SJSU resources, ranks by urgency, returns specific actions with locations and contacts. |
| **Output** | Under 200 words, in the student's language, closing with direct acknowledgment of the situation. |
| **Human in the loop** | A Basic Needs Center peer advisor reviews non-English and vague inputs before anything reaches the student. |

---

## Why Text Generation

Structured extraction requires input that is already clean and categorized. A student in crisis does not write that way. Image recognition does not apply. Text generation is the only capability that meets people where they actually are.

The system prompt is where the real decisions live. One line determines whether the tool serves Spanish, Vietnamese, and Cantonese speakers at all. Remove it and you quietly exclude a large share of the population the tool was built for.

---

## Test Coverage

| Case | Scenario | What It Tests |
|---|---|---|
| 1 | Financial hold blocking registration | Most common crisis path, deadline awareness |
| 2 | Food insecurity | Whether the tool surfaces resources the student does not know exist |
| 3 | Overlapping housing, food, and balance crises | Prioritization under multiple simultaneous needs |
| 4 | Circumstances changed after FAFSA submission | Knowledge of the appeal process |
| Edge | Spanish-language input | Language matching, the documented failure point |

Screenshots for every case live in `screenshots/`.

---

## The Failure Case

**Input tested:**

    "Hola, necesito ayuda. No tengo dinero y no sé qué hacer.
     Estoy en la universidad pero no entiendo los recursos."

**Original behavior:** the system returned an accurate, well-structured answer in English. She cannot act on it. She misses the Fee Deferral deadline. The hold stays. She loses her seat in fall classes.

The student Sammy's Source was designed to reach is the first one it failed, and she is also the least likely to try again.

**The fix:** a language detection instruction was added to the system prompt. The tool now matches the student's language and asks one clarifying question when input is too vague to route, instead of guessing. The notebook shows before and after on the same input.

---

## Oversight and Tradeoff

| Tradeoff | Detail |
|---|---|
| Speed | Non-English and vague inputs queue for human review, 4 to 24 hours depending on staffing |
| Immediacy vs. accuracy | A confident wrong answer in seconds does more damage than the right answer the next morning |

The cost is real. For a student with two days until registration closes, a 24-hour queue matters. Accuracy was prioritized anyway, because the students most likely to write in Spanish or send a vague message are also the least likely to have a backup plan when the tool routes them to the wrong office.

---

## Repository Structure

```
BUS4_110A_Project_3.ipynb   Full implementation: system prompt, call function, 4 test cases, edge case
screenshots/                Captured outputs for every test and the before/after edge case
README.md
```

---

## Running It

1. Open `BUS4_110A_Project_3.ipynb` in Google Colab.
2. Add a Colab secret named `GEMINI_API_KEY` and toggle notebook access on.
3. Run all cells. The first cell installs `google-genai`; the third defines the system prompt, which is where every meaningful policy decision lives.

Edit the system prompt to change which resources the tool knows about, how it ranks urgency, and which inputs get flagged for human review.

---

## Project Info

| Field | Detail |
|---|---|
| **Course** | BUS4-110A: Fundamentals of MIS |
| **Institution** | SJSU Lucas College of Business · Spring 2026 |
| **AI tool** | Google Gemini API, `gemini-2.0-flash` |
| **SDGs** | No Poverty (1) · Quality Education (4) |
| **Team 5** | [Cash Johnson](https://www.linkedin.com/in/cash-johnson/) · [Fatima Zehra Shaikh](https://www.linkedin.com/in/fatimazehra-shaikh/) · [James Doan](https://www.linkedin.com/in/jamesdoan/) · Wilson Lin · Jackie Li |
