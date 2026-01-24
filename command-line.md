# Playwright Test CLI – Interview Questions & Answers

This document is a complete Q&A guide covering the **Playwright CLI** section of the official documentation with detailed explanations and code examples.
It is ideal for interview preparation, deep learning, or team knowledge sharing.

📌 Source: Playwright Test CLI docs ([Playwright][1])

---

## 📚 Table of Contents

1. [General CLI Concepts](#general-cli-concepts)
2. [Running Tests Using CLI](#running-tests-using-cli)
3. [CLI Filters & Patterns](#cli-filters--patterns)
4. [Debug & Interactive Modes](#debug--interactive-modes)
5. [Show Report Command](#show-report-command)
6. [Browser Installation via CLI](#browser-installation-via-cli)
7. [Advanced CLI Options](#advanced-cli-options)
8. [FAQs & Best Practices](#faqs--best-practices)

---

## General CLI Concepts

### **1. What is the Playwright Test CLI?**

**Answer:**
The Playwright Test CLI is a powerful command-line interface used to run tests, filter test execution, debug tests, generate reports, and manage configuration all via terminal commands. ([Playwright][1])

It’s the primary way developers and CI/CD systems execute and interact with Playwright tests.

---

### **2. How do you get help for all available CLI commands?**

**Answer:**
Run:

```bash
npx playwright --help
```

This displays the full list of supported commands and options. ([Playwright][1])

---

## Running Tests Using CLI

### **3. How do you run all Playwright tests using CLI?**

**Answer:**
Use the base test command:

```bash
npx playwright test
```

This runs all tests according to your configuration. ([Playwright][1])

---

### **4. How can you run a specific test file?**

**Answer:**
Pass the file path to the test CLI:

```bash
npx playwright test tests/todo-page.spec.ts
```

Only that file’s tests execute. ([Playwright][1])

---

### **5. How do you run tests only in a specific directory or set of directories?**

**Answer:**
Pass multiple directories:

```bash
npx playwright test tests/login/ tests/dashboard/
```

Playwright runs tests found in those folders. ([Playwright][1])

---

### **6. How can you run tests starting at a specific line number?**

**Answer:**

```bash
npx playwright test my-spec.ts:42
```

This runs the specific test at/near the defined line. ([Playwright][1])

---

### **7. How do you run tests by their test title?**

**Answer:**

Use the `-g` flag with a regular expression.

```bash
npx playwright test -g "login success"
```

Only tests with matching names run. ([Playwright][1])

---

## CLI Filters & Patterns

### **8. What is the role of grep in CLI?**

**Answer:**
`--grep` filters tests whose titles match a given regex.

Example:

```bash
npx playwright test --grep @smoke
```

Only smoke tests run. ([Playwright][1])

---

### **9. How do you exclude tests using CLI?**

**Answer:**
Use `--grep-invert` with a regex:

```bash
npx playwright test --grep-invert @slow
```

Tests matching `@slow` are skipped. ([Playwright][1])

---

## Debug & Interactive Modes

### **10. How do you disable parallel workers?**

**Answer:**
Use `--workers`:

```bash
npx playwright test --workers=1
```

This runs tests sequentially in one worker. ([Playwright][1])

---

### **11. How do you run tests in interactive UI mode?**

**Answer:**

```bash
npx playwright test --ui
```

This opens a UI where you can visually manage test runs. ([Playwright][1])

---

### **12. How do you debug tests using Playwright Inspector?**

**Answer:**

```bash
npx playwright test --debug
```

This supplies a debugging session with inspectors and pauses on failure. ([Playwright][1])

---

## Show Report Command

### **13. How do you view an HTML report after a test run?**

**Answer:**

```bash
npx playwright show-report
```

This opens the interactive HTML report from the latest run. ([Playwright][1])

---

### **14. How do you serve the report on a specific port?**

**Answer:**

```bash
npx playwright show-report --port 8080
```

This serves the report on port 8080. ([Playwright][1])

---

## Browser Installation via CLI

### **15. How do you install supported browsers via CLI?**

**Answer:**

```bash
npx playwright install
```

This installs all browsers for your project. ([Playwright][1])

---

### **16. How do you install browser system dependencies?**

**Answer:**

```bash
npx playwright install --with-deps
```

This also installs required OS system dependencies. ([Playwright][1])

---

### **17. How do you install specific browsers only?**

**Answer:**

```bash
npx playwright install chromium webkit
```

Only Chromium and WebKit are installed. ([Playwright][1])

---

## Advanced CLI Options

### **18. What does `--fail-on-flaky-tests` do?**

**Answer:**
Fails the entire test run if any tests are flagged as flaky. ([Playwright][1])

---

### **19. How do you specify a custom configuration file?**

**Answer:**

```bash
npx playwright test --config=custom.config.ts
```

Playwright uses the custom config file. ([Playwright][1])

---

### **20. How do you re-run only last-failed tests?**

**Answer:**

```bash
npx playwright test --last-failed
```

This re-runs tests that failed in the previous run. ([Playwright][1])

---

### **21. What does `--only-changed` do?**

**Answer:**
Runs test files that changed since the last Git commit:

```bash
npx playwright test --only-changed
```

This can speed up feedback loops. ([Playwright][1])

---

### **22. What are test list flags?**

**Answer:**

* `--list`: Lists all discovered tests but does not execute them.
* `--test-list <file>`: Runs only tests from that list file.
* `--test-list-invert <file>`: Excludes tests from that list. ([Playwright][1])

---

### **23. How do you control retries from CLI?**

**Answer:**

```bash
npx playwright test --retries=2
```

This retries failing tests up to 2 times. ([Playwright][1])

---

## FAQs & Best Practices

### **24. Can you fail a test suite if someone left `test.only` in code?**

**Answer:**

```bash
npx playwright test --forbid-only
```

This is useful for CI to avoid accidentally committing focused tests. ([Playwright][1])

---

### **25. How do you specify the output directory for artifacts via CLI?**

**Answer:**

```bash
npx playwright test --output=./my-results
```

Playwright saves artifacts like traces/screenshots there. ([Playwright][1])

---

### **26. How do you repeat each test multiple times?**

**Answer:**

```bash
npx playwright test --repeat-each=3
```

Each test runs three times. ([Playwright][1])

---

### **27. What is the default worker count when running tests?**

**Answer:**
By default, Playwright uses workers equal to **50% of logical CPU cores**. ([Playwright][1])

---

## 📌 Summary

The Playwright CLI is an extremely **rich and flexible interface** for:

* Running selective test executions
* Debugging tests
* Viewing reports
* Managing parallelism
* Specifying config behavior

[1]: https://playwright.dev/docs/test-cli "Command line | Playwright"
