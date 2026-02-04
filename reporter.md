This document contains **mind maps, cheat sheets, and interview Q&A** for **Playwright Test Reporters**, designed for **quick revision and interview preparation**.

# 🃏 Playwright Test Reporters — Revision & Interview Notes

## Flashcard 1

**Q:** What is a reporter in Playwright?
**A:** A reporter listens to test execution events and produces output such as logs or reports.

---

## Flashcard 2

**Q:** Does a reporter affect test execution or results?
**A:** No, reporters are passive and do not affect test behavior.

---

## Flashcard 3

**Q:** Where can reporters be configured?
**A:** In `playwright.config.ts` or via the CLI using `--reporter`.

---

## Flashcard 4

**Q:** How do you configure a reporter in `playwright.config.ts`?
**A:**

```ts
export default defineConfig({
  reporter: 'html',
});
```

---

## Flashcard 5

**Q:** How do you specify a reporter using CLI?
**A:**

```bash
npx playwright test --reporter=html
```

---

## Flashcard 6

**Q:** Can Playwright run multiple reporters at the same time?
**A:** Yes, multiple reporters can be configured and run simultaneously.

---

## Flashcard 7

**Q:** How do you configure multiple reporters?
**A:**

```ts
reporter: [
  ['dot'],
  ['html'],
  ['json', { outputFile: 'results.json' }]
]
```

---

## Flashcard 8

**Q:** What is the default reporter in local execution?
**A:** `list`

---

## Flashcard 9

**Q:** What is the default reporter in CI environments?
**A:** `dot`

---

## Flashcard 10

**Q:** What does the `list` reporter do?
**A:** Prints detailed test results line by line in the terminal.

---

## Flashcard 11

**Q:** What does the `line` reporter do?
**A:** Shows test progress in a single updating terminal line.

---

## Flashcard 12

**Q:** What does the `dot` reporter do?
**A:** Prints one dot per test for minimal CI-friendly output.

---

## Flashcard 13

**Q:** What does the `html` reporter generate?
**A:** An interactive HTML report with test results, screenshots, videos, and traces.

---

## Flashcard 14

**Q:** When should you use the HTML reporter?
**A:** For local debugging and detailed test analysis.

---

## Flashcard 15

**Q:** What does the `json` reporter generate?
**A:** A structured JSON file containing test results and metadata.

---

## Flashcard 16

**Q:** When is the JSON reporter useful?
**A:** For analytics, dashboards, and CI integrations.

---

## Flashcard 17

**Q:** What does the `junit` reporter generate?
**A:** A JUnit-compatible XML report.

---

## Flashcard 18

**Q:** Why is the JUnit reporter commonly used?
**A:** CI tools natively support JUnit XML format.

---

## Flashcard 19

**Q:** Can reporters generate output files?
**A:** Yes, reporters like HTML, JSON, and JUnit generate files.

---

## Flashcard 20

**Q:** Do reporters automatically include screenshots and videos?
**A:** Only if screenshots and videos are enabled in Playwright configuration.

---

## Flashcard 21

**Q:** What is a custom reporter?
**A:** A user-defined reporter built using Playwright’s Reporter API.

---

## Flashcard 22

**Q:** When would you need a custom reporter?
**A:** When integrating with custom systems or generating specialized reports.

---

## Flashcard 23

**Q:** Can reporters be configured differently for CI and local runs?
**A:** Yes, conditional configuration can be used.

---

## Flashcard 24

**Q:** What is a common reporter setup for CI pipelines?
**A:** `dot` + `junit`

---

## Flashcard 25

**Q:** What is a common reporter setup for local development?
**A:** `html` or `list`

---

## Flashcard 26 ⭐

**Q:** Give a one-line explanation of Playwright reporters (interview).
**A:** Reporters define how Playwright test results are collected and presented without affecting test execution.

---

If you want next (also in **pure Markdown**):

* `test-fixtures` flashcards
* `test-use-options` flashcards
* `test-configuration` flashcards
* A **full Playwright flashcards repo structure**

Just tell me the next doc URL 👌

---

## 🧠 1. Mind Map — Playwright Test Reporters

```
Playwright Test Reporters
│
├── What is a Reporter
│   ├── Observes test execution
│   ├── Generates output
│   └── Does NOT affect test behavior
│
├── Configuration
│   ├── playwright.config.ts
│   ├── CLI (--reporter)
│   └── Single or multiple reporters
│
├── Built-in Reporters
│   ├── list
│   ├── line
│   ├── dot
│   ├── html
│   ├── json
│   └── junit
│
├── Output Types
│   ├── Console output
│   ├── HTML report
│   ├── JSON file
│   └── XML (JUnit)
│
├── Use Cases
│   ├── Local debugging
│   ├── CI pipelines
│   ├── Test analytics
│   └── Reporting dashboards
│
├── Multiple Reporters
│   ├── Run simultaneously
│   └── Combined outputs
│
├── Attachments
│   ├── Screenshots
│   ├── Videos
│   └── Traces
│
└── Custom Reporters
    ├── Built using Reporter API
    ├── Listen to test lifecycle
    └── Custom integrations
```

---

## 🧾 2. One-Page Cheat Sheet — Playwright Reporters

### 🔹 What is a Reporter?

A **reporter** listens to Playwright test lifecycle events and produces results in **console output or files**.

---

### 🔹 Configuration

```ts
// playwright.config.ts
import { defineConfig } from '@playwright/test';

export default defineConfig({
  reporter: 'html',
});
```

OR

```bash
npx playwright test --reporter=html
```

---

### 🔹 Multiple Reporters Example

```ts
reporter: [
  ['dot'],
  ['html'],
  ['json', { outputFile: 'results.json' }]
]
```

---

### 🔹 Built-in Reporters (Quick Recall)

| Reporter | Purpose                          |
| -------- | -------------------------------- |
| list     | Detailed terminal output         |
| line     | Single-line progress             |
| dot      | Minimal CI output                |
| html     | Interactive visual report        |
| json     | Structured machine-readable data |
| junit    | CI-friendly XML                  |

---

### 🔹 Default Behavior

* **Local execution:** `list`
* **CI execution:** `dot`

---

### 🔹 Best Practices

* **Local debugging:** `html`, `list`
* **CI pipelines:** `dot` + `junit`
* **Analytics / dashboards:** `json`
* **Custom needs:** Custom reporter

---

### 🔹 Key Interview Sentence ⭐

> Playwright reporters observe test execution and control how results are presented without impacting test logic.

---

## 🎯 3. Interview Flash Q&A — Playwright Reporters

### Q1. What is a reporter in Playwright?

A reporter formats and outputs test execution results by listening to test lifecycle events.

---

### Q2. Does a reporter affect test execution?

No. Reporters are passive observers.

---

### Q3. Where can reporters be configured?

In `playwright.config.ts` or via the CLI.

---

### Q4. Can Playwright use multiple reporters?

Yes, multiple reporters can run simultaneously.

---

### Q5. Which reporter is best for CI?

`dot` for logs and `junit` for CI integration.

---

### Q6. Which reporter is best for debugging failures?

`html`, because it includes screenshots, videos, and traces.

---

### Q7. What does the JSON reporter provide?

Structured test result data suitable for analytics or dashboards.

---

### Q8. Why use JUnit reporter?

Most CI tools natively understand JUnit XML format.

---

### Q9. How do reporters handle screenshots and videos?

They attach artifacts if screenshots and videos are enabled in configuration.

---

### Q10. What is a custom reporter?

A reporter built using Playwright’s Reporter API for custom outputs or integrations.

---

### Q11. Can reporters be environment-specific?

Yes, reporters can be configured conditionally (local vs CI).

---

### Q12. Real-world setup example?

* Local → `html`
* CI → `dot` + `junit`

---

### Q13. One-line explanation (Interview Gold ⭐)

> Playwright reporters define how test results are consumed by humans or systems without changing test behavior.

---
