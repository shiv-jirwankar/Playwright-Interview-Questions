# Playwright Test CLI — Complete Interview Questions & Answers

This document covers **all topics and sub-topics from the Playwright Test CLI docs**, with detailed explanations and examples.
Source: Playwright Official Docs — Test CLI ([Playwright][1])

---

## 📚 Table of Contents

1. [Overview of Playwright CLI](#overview-of-playwright-cli)
2. [Running Tests Using CLI](#running-tests-using-cli)
3. [Common CLI Options for Test Runs](#common-cli-options-for-test-runs)
4. [All CLI Options Explained](#all-cli-options-explained)
5. [Test Listing & Filtering Files](#test-listing--filtering-files)
6. [Show Report Command](#show-report-command)
7. [Browser Installation Commands](#browser-installation-commands)
8. [Code Generation (codegen)](#code-generation-codegen)
9. [Trace Viewer (show-trace)](#trace-viewer-show-trace)
10. [Specialized Commands](#specialized-commands)
11. [Practical Interview Scenarios](#practical-interview-scenarios)

---

---

## Overview of Playwright CLI

### **1. What is the Playwright Test CLI and why is it important?**

**Answer:**
The Playwright Test CLI is the command-line interface that provides powerful control over test execution, filtering, debugging, reporting, and browser management. It’s the primary way developers and CI systems interact with Playwright tests. ([Playwright][1])

---

### **2. How do you view all commands and options supported by the CLI?**

**Answer:**

```bash
npx playwright --help
```

This prints all available commands and flags supported by the CLI. ([Playwright][1])

---

---

## Running Tests Using CLI

### **3. What’s the basic syntax to run Playwright tests via CLI?**

**Answer:**

```bash
npx playwright test [options] [test-filter...]
```

This command runs all tests matching optional patterns. ([Playwright][1])

---

### **4. How do you run all tests?**

**Answer:**

```bash
npx playwright test
```

This executes all tests discovered in the project. ([Playwright][1])

---

### **5. How do you run a specific test file or directory?**

**Answer:**

```bash
npx playwright test tests/example.spec.ts  
npx playwright test tests/login/ tests/home/
```

You can specify multiple paths or directories to run selected tests. ([Playwright][1])

---

### **6. How do you run a test at a specific line number?**

**Answer:**

```bash
npx playwright test my-spec.ts:42
```

This helps run a test at a particular line. ([Playwright][1])

---

### **7. How do you run tests by name/title?**

**Answer:**

```bash
npx playwright test -g "test title here"
```

This runs only tests matching the regex in the title. ([Playwright][1])

---

---

## Common CLI Options for Test Runs

### **8. What is the purpose of `--debug`?**

**Answer:**
Runs tests with Playwright Inspector enabled. It’s equivalent to setting environment variables and specific options to disable timeouts and run tests one at a time. ([Playwright][1])

---

### **9. What does `--headed` do?**

**Answer:**
Runs tests in headed browsers (browser windows visible) instead of headless mode. ([Playwright][1])

---

### **10. How do you limit the number of workers?**

**Answer:**

```bash
npx playwright test --workers=1
```

This forces tests to run sequentially. ([Playwright][1])

---

### **11. What does `--project` do?**

**Answer:**
Runs tests only from the specified project(s), useful when multiple projects (like different browsers) are defined in config. ([Playwright][1])

---

---

## All CLI Options Explained

### **12. How do you specify a custom config file?**

**Answer:**

```bash
npx playwright test --config=playwright.config.custom.ts
```

This lets you run tests with a non-standard config file. ([Playwright][1])

---

### **13. What does `--fail-on-flaky-tests` do?**

**Answer:**
Makes the entire test suite fail if any test was marked as flaky. ([Playwright][1])

---

### **14. Why would you use `--forbid-only`?**

**Answer:**
It fails the test run if any test has `test.only`, preventing accidental commits that focus only a subset of tests. ([Playwright][1])

---

### **15. What is `--fully-parallel`?**

**Answer:**
Runs all tests in parallel across all workers regardless of default settings. ([Playwright][1])

---

### **16. What does `--global-timeout` do?**

**Answer:**
Sets a maximum time (in ms) for the whole test suite to finish. ([Playwright][1])

---

### **17. How does `--grep` work?**

**Answer:**
Filters tests by name using a regular expression. ([Playwright][1])

---

### **18. What does `--grep-invert` do?**

**Answer:**
Runs tests *not* matching the pattern. ([Playwright][1])

---

### **19. Why use `--ignore-snapshots`?**

**Answer:**
Ignores all snapshot and screenshot comparisons during execution. ([Playwright][1])

---

### **20. What is `--last-failed`?**

**Answer:**
Re-runs only tests that failed in the last run. ([Playwright][1])

---

### **21. What does `--list` do?**

**Answer:**
Lists all discovered tests without running them. ([Playwright][1])

---

### **22. How do you stop after first failure?**

**Answer:**
Use:

```bash
npx playwright test --max-failures=1
```

Or shorter:

```bash
npx playwright test -x
```

This stops after the first failure. ([Playwright][1])

---

### **23. What is `--no-deps`?**

**Answer:**
Ignores project dependencies defined in config for that run. ([Playwright][1])

---

### **24. How do you set the output directory for artifacts?**

**Answer:**

```bash
npx playwright test --output=./my-results
```

This saves artifacts (screenshots/traces) to the specified folder. ([Playwright][1])

---

### **25. What is `--only-changed`?**

**Answer:**
Runs only files that have changed compared to the Git HEAD or a given ref. ([Playwright][1])

---

### **26. What does `--pass-with-no-tests` do?**

**Answer:**
Treats a run with no tests found as a success instead of failure. ([Playwright][1])

---

### **27. What is `--quiet`?**

**Answer:**
Suppresses all output to the terminal. ([Playwright][1])

---

### **28. How does `--tsconfig` work?**

**Answer:**
Specifies a single TypeScript config file for all imports. ([Playwright][1])

---

### **29. How do you update snapshots from CLI?**

**Answer:**

```bash
npx playwright test --update-snapshots
```

You can pass modes like `all`, `changed`, or `missing`. ([Playwright][1])

---

---

## Test Listing & Filtering Files

### **30. What is the format of a test list file used by `--test-list`?**

**Answer:**
A plain text listing of test file paths, test suites, and full test titles; used to include/exclude specific tests. ([Playwright][1])

---

### **31. How does `--test-list-invert` work?**

**Answer:**
Excludes tests listed in the specified test list file. ([Playwright][1])

---

---

## Show Report Command

### **32. What is `show-report`?**

**Answer:**
Opens the HTML test report from the latest test suite run. ([Playwright][1])

---

### **33. How do you show a specific report directory?**

**Answer:**

```bash
npx playwright show-report my-report/
```

This serves that report directory in a browser. ([Playwright][1])

---

### **34. How do you serve the report on a custom host/port?**

**Answer:**

```bash
npx playwright show-report --host 0.0.0.0 --port 8080
```

You can customize both parameters. ([Playwright][1])

---

---

## Browser Installation Commands

### **35. How do you install all supported browsers?**

**Answer:**

```bash
npx playwright install
```

Installs Chromium, Firefox, and WebKit. ([Playwright][1])

---

### **36. How do you install only specific browsers?**

**Answer:**

```bash
npx playwright install chromium webkit
```

Installs only those browsers. ([Playwright][1])

---

### **37. What flags do `install` support?**

**Answer:**

* `--with-deps`: installs OS dependencies
* `--force`: forces reinstallation
* `--dry-run`: prints without executing
* `--only-shell / --no-shell` options change shell behavior ([Playwright][1])

---

### **38. How do you install browser dependencies only?**

**Answer:**

```bash
npx playwright install-deps
```

Installs system libraries required by browsers. ([Playwright][1])

---

### **39. How do you uninstall browsers?**

**Answer:**

```bash
npx playwright uninstall
```

Removes installed browsers. ([Playwright][1])

---

---

## Code Generation (codegen)

### **40. What does the `codegen` command do?**

**Answer:**
Records your browser interactions into generated test code. ([Playwright][1])

---

### **41. How do you start codegen for a URL?**

**Answer:**

```bash
npx playwright codegen https://example.com
```

This opens an interactive recorder. ([Playwright][1])

---

### **42. What `codegen` flags are important?**

**Answer:**

* `-b, --browser`: choose browser
* `--target`: language/framework
* `-o, --output`: output file ([Playwright][1])

---

---

## Trace Viewer (show-trace)

### **43. What does `show-trace` do?**

**Answer:**
Opens the trace viewer to analyze saved trace files. ([Playwright][1])

---

### **44. How do you specify a trace file?**

**Answer:**

```bash
npx playwright show-trace trace.zip
```

You can open specific trace files or folders. ([Playwright][1])

---

### **45. What options does `show-trace` support?**

**Answer:**

* `-b`: browser choice
* `-h`, `-p`: custom host/port ([Playwright][1])

---

---

## Specialized Commands

### **46. What is `merge-reports`?**

**Answer:**
Combines multiple test report blobs into a unified output. ([Playwright][1])

---

### **47. Explain `clear-cache`.**

**Answer:**

```bash
npx playwright clear-cache
```

Clears Playwright’s downloaded caches. ([Playwright][1])

---

---

## Practical Interview Scenarios

### **48. How would you run tests only on changed test files since last commit?**

**Answer:**

```bash
npx playwright test --only-changed
```

This uses Git to detect changed files. ([Playwright][1])

---

### **49. How do you rerun only failed tests?**

**Answer:**

```bash
npx playwright test --last-failed
```

Reruns only the tests that failed most recently. ([Playwright][1])

---

### **50. How to combine UI mode with other flags?**

**Answer:**

```bash
npx playwright test --ui --headed --workers=1
```

Useful for debug sessions when visually inspecting the tests. ([checklyhq.com][2])

---

## 📌 Conclusion

This README covers **every topic and flag from the official Playwright Test CLI docs** with detailed interview questions, answers, and examples.
Always reference `npx playwright --help` for the latest options in your installed Playwright version. ([Playwright][1])
[1]: https://playwright.dev/docs/test-cli?utm_source=chatgpt.com "Command line"
[2]: https://www.checklyhq.com/blog/five-playwright-cli-features-you-should-know/?utm_source=chatgpt.com "Top 5 Playwright CLI Features to Streamline Testing"
