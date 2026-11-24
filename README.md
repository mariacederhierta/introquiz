# IntroQuiz

A simple learner app for training sessions with two activities:

- **Introduction** – warm-up questions with no right or wrong answers (expectations, experience, reflection).
- **Quiz** – knowledge check with hints, explanations after each answer and a score at the end.

Learners join by scanning a QR code or opening a link. **No sign-in, no app to install.**

**Learner address:** https://mariacederhierta.github.io/introquiz/

---

## Running a session

1. Open the learner address on your laptop and show it on the projector.
2. In the **Join on your device** panel, under **Trainer: where should learners start?**, pick:
   - **Introduction** – learners go straight to the introduction
   - **Quiz** – learners go straight to the quiz
   - **Let learners choose** – learners see both and pick one
3. The QR code and link update immediately. Learners scan the QR code (or you share the link with **Copy link**).
4. Use **Download QR code (PNG)** to put the QR code on a slide.

Learners can always tap **Home** to reach the other activity.

## Privacy

- Answers stay in the learner's own browser tab only.
- Nothing is saved, sent anywhere or linked to a person.
- Refreshing or closing the page clears all answers.
- The trainer cannot see learners' answers.

---

## Changing the questions (per course)

All questions and texts live in one file: **`activity.json`** in this repository.
You don't edit it by hand – use Excel and the **Trainer tools** page.

1. Open the learner address and select **Trainer tools: change the questions** (bottom of the start page).
2. Select **Download as Excel**.
3. Edit the workbook (see *Excel format* below) and save it.
4. In Trainer tools, select **Choose question file** and pick your Excel file.
   - If something is wrong, the page lists the problems by sheet and row. Fix them and upload again.
5. Select **Use in this browser** to try it out yourself (this only affects your own browser).
6. When you're happy, select **Download as activity.json**.
7. In this GitHub repository: **Add file › Upload files**, drop in the new `activity.json`, and select **Commit changes**.
8. After 1–2 minutes all learners get the new questions (press Ctrl+F5 if you still see the old ones).

Tip: keep one Excel file per course (for example `Copilot-basics.xlsx`, `Fabric-intro.xlsx`) on your OneDrive, and upload the matching `activity.json` before each session.

---

## Excel format

### Settings sheet

| Setting | What it does |
|---|---|
| title | Big heading on the start page |
| description | Text under the heading |
| startWith | Default start: `introduction`, `quiz` or `choice` (the picker on the start page overrides it) |
| publicUrl | Leave empty – the app uses its own address for the QR code |
| privacyMessage | Privacy text shown to learners |
| introduction.enabled / quiz.enabled | `TRUE` or `FALSE` to switch an activity on or off |
| introduction.title, quiz.title, …description | Titles and descriptions of each activity |
| introduction.completionTitle / completionMessage | Text shown when the introduction is finished |

### Introduction sheet – one row per question

| Column | Meaning |
|---|---|
| id | Unique text, e.g. `intro-1` (unique across both sheets) |
| order | Number; lower comes first |
| active | `TRUE` shows the question, `FALSE` hides it |
| responseType | `single-choice`, `multiple-choice`, `free-text`, `short-text`, `rating`, `yes-no`, `reflection` |
| text | The question |
| supportingText | Optional extra text under the question |
| options | Answer options, **one per line in the cell** (Alt+Enter for a new line) |
| required | `TRUE` if learners must answer |
| ratingMin / ratingMax / ratingMinLabel / ratingMaxLabel | For rating questions (default 1–5) |
| reflectionMode | For reflection questions: `think` or `discuss` |

### Quiz sheet – one row per question

| Column | Meaning |
|---|---|
| id, order, active, text, supportingText, options | Same as above |
| type | `single-choice`, `multiple-choice`, `true-false`, `free-text`, `scenario` |
| correctAnswers | Option **numbers**, e.g. `2` or `1, 3`. True-false: `true` or `false`. Free-text: every accepted answer, one per line |
| explanation | Shown after the learner checks their answer |
| hint | Optional hint learners can reveal |
| points | Points for the question (default 1) |

For **scenario** questions, put the scenario in *supportingText*.

### Feedback sheet

Messages on the quiz results screen, by score: `minPercent` (0–100) and `message`. The highest matching row is shown.

### Help sheet

A short reminder of all of the above.

---

## Updating the app itself

The files `index.html` and the `assets` folder are the app. Only replace them when you get a new version of IntroQuiz. Uploading new versions of them does **not** change your questions, as long as you don't also upload a different `activity.json`.

## Good to know

- This repository is public, so anyone who looks can read `activity.json`, including the quiz answers. Don't put confidential content in it.
- Anyone with the link can open Trainer tools, but they can only try files in their own browser. Only people with access to this repository can change the questions for everyone.
