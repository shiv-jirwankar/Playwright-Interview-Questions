# Playwright Test Annotations – Interview Questions & Answers

This document contains **detailed interview questions and answers** related to **Playwright Test Annotations**, strictly based on the official Playwright documentation:

🔗 [https://playwright.dev/docs/test-annotations](https://playwright.dev/docs/test-annotations)

Useful for:

* Interview preparation
* Playwright revision
* Team knowledge sharing

---

## 📚 Table of Contents

1. [General Concepts](#general-concepts)
2. [Built-in Annotations](#built-in-annotations)
3. [Focus / Exclusive Execution](#focus--exclusive-execution)
4. [Skipping Tests](#skipping-tests)
5. [Grouping Tests](#grouping-tests)
6. [Tags](#tags)
7. [Annotating Tests](#annotating-tests)
8. [Conditional & Runtime Annotations](#conditional--runtime-annotations)
9. [Command-Line Execution](#command-line-execution)
10. [Reporting & Visibility](#reporting--visibility)
11. [Advanced Concepts](#advanced-concepts)

---

## General Concepts

### 1. What are annotations in Playwright Test?

Annotations are metadata attached to tests or test groups to control execution or provide additional context. They are shown in Playwright reports and are accessible to custom reporters.

---

### 2. How are tags and annotations different?

* **Tags** are simple labels used for filtering tests.
* **Annotations** are structured metadata objects containing a `type` and an optional `description`.

---

### 3. Why are annotations displayed in test reports?

They explain why a test was skipped, marked slow, expected to fail, or linked to an issue.

---

### 4. Can annotations be added dynamically at runtime?

Yes. Runtime annotations can be added using `test.info().annotations`.

---

### 5. Where are annotations available for custom reporters?

They are exposed via `TestCase.annotations` in the reporter API.

---

## Built-in Annotations

### 6. What built-in annotations does Playwright support?

* `test.skip()`
* `test.fail()`
* `test.fixme()`
* `test.slow()`

---

### 7. What does `test.skip()` do?

Skips the test entirely.

```ts
test.skip('skipped test', async ({ page }) => {});
```

---

### 8. What is the purpose of `test.fail()`?

Marks the test as **expected to fail**. If it passes, Playwright reports it as unexpected.

```ts
test('expected failure', async () => {
  test.fail();
});
```

---

### 9. Difference between `test.fixme()` and `test.fail()`?

* **fixme** → test is not executed
* **fail** → test executes and is expected to fail

---

### 10. What does `test.slow()` do?

It increases the test timeout to **3× the default value**.

```ts
test('slow test', async () => {
  test.slow();
});
```

---

## Focus / Exclusive Execution

### 11. What does `test.only()` do?

Runs only the marked test(s) and skips all others.

```ts
test.only('run only this test', async () => {});
```

---

### 12. What if multiple tests use `test.only()`?

All tests marked with `only` will be executed.

---

### 13. Can `test.only()` be used in hooks?

No. It can only be used on test declarations.

---

## Skipping Tests

### 14. How do you skip tests conditionally?

By evaluating conditions at runtime.

```ts
test('conditional skip', async ({ browserName }) => {
  test.skip(browserName === 'firefox', 'Not supported in Firefox');
});
```

---

### 15. What is the role of the condition in `test.skip()`?

It determines whether the test should be skipped based on runtime values.

---

### 16. Can test groups be skipped?

Yes, by applying conditional logic inside grouped tests.

---

### 17. Skipping at declaration vs inside test?

* **Declaration** → static skip
* **Inside test** → runtime decision

---

## Grouping Tests

### 18. How do you group tests?

Using `test.describe()`.

```ts
test.describe('Login tests', () => {
  test('valid login', async () => {});
});
```

---

### 19. Can annotations be applied to groups?

Yes. Group-level annotations apply to all nested tests.

---

### 20. Advantages of grouping with annotations?

* Shared metadata
* Better organization
* Cleaner reports

---

## Tags

### 21. How do you tag a test?

Using `@tag` in the title or the `tag` option.

---

### 22. Tag syntax requirement?

Tags must start with `@`.

---

### 23. How to filter tests using tags?

Using the `--grep` CLI option.

```bash
npx playwright test --grep @smoke
```

---

### 24. Can a test have multiple tags?

Yes.

```ts
test('test', { tag: ['@smoke', '@fast'] }, async () => {});
```

---

### 25. Where are tags displayed?

In Playwright reports and CLI output.

---

## Annotating Tests

### 26. How do you add annotations at declaration?

Using the `annotation` option.

```ts
test('issue linked test', {
  annotation: {
    type: 'issue',
    description: 'https://github.com/org/repo/issues/123'
  }
}, async () => {});
```

---

### 27. Annotation object properties?

* `type`
* `description` (optional)

---

### 28. Can multiple annotations be added?

Yes, by passing an array of annotation objects.

---

### 29. How to annotate test groups?

Provide annotations in the `test.describe()` options.

---

### 30. Importance of `type` and `description`?

They define the category and context displayed in reports.

---

## Conditional & Runtime Annotations

### 31. How do built-in annotations become conditional?

By applying them based on runtime conditions.

---

### 32. Can annotations depend on fixtures?

Yes, for example using `browserName`.

---

### 33. What does configuration-based annotation mean?

Annotations can behave differently across projects or environments.

---

### 34. How to add runtime annotations?

By pushing into `test.info().annotations`.

```ts
test.info().annotations.push({
  type: 'note',
  description: 'Runtime metadata'
});
```

---

### 35. When should runtime annotations be used?

When metadata depends on runtime behavior or test outcome.

---

## Command-Line Execution

### 36. How to run tagged tests?

Using `--grep`.

---

### 37. How to skip tests using tags?

Using `--grep-invert`.

```bash
npx playwright test --grep-invert @slow
```

---

### 38. How to handle AND / OR logic with tags?

* **OR** → `@fast|@smoke`
* **AND** → `(?=.*@fast)(?=.*@smoke)`

---

## Reporting & Visibility

### 39. How are annotations shown in HTML reports?

They appear alongside test results.

---

### 40. Are annotations visible in all reporters?

HTML reporter shows them by default; custom reporters can access them programmatically.

---

### 41. How do annotations help debugging?

They explain test intent, failures, skips, and known issues.

---

## Advanced Concepts

### 42. How do annotations interact with `browserName`?

They enable browser-specific skips or markings.

---

### 43. Can `test.fixme()` be used in hooks?

Yes. Calling it inside hooks will skip the test.

---

### 44. How to control CI vs local execution?

Use environment-based conditions inside annotations.

---

### 45. Tagging via title vs options?

* **Title** → quick and visible
* **Options** → cleaner and structured

---

## ✅ Conclusion

Playwright Test Annotations are essential for:

* Controlling execution
* Improving reporting
* Managing flaky or environment-specific tests

Mastering them is a **must-have skill for Playwright interviews and real-world automation** 🚀
