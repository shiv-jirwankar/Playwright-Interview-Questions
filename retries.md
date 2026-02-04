![alt text](src/retries.png)

# 🃏 Playwright Test Retries — Complete Q&A Notes

> Covers **all sections** from
> [https://playwright.dev/docs/test-retries](https://playwright.dev/docs/test-retries)

---

## Basics

### Q: What are test retries in Playwright?

**A:** Test retries automatically re-run a failing test until it passes or the maximum retry count is reached.

---

### Q: Are retries enabled by default?

**A:** No. By default, Playwright does not retry failed tests.

---

## Configuration

### Q: How do you enable retries via CLI?

```bash
npx playwright test --retries=3
```

---

### Q: How do you configure retries globally in `playwright.config.ts`?

```ts
import { defineConfig } from '@playwright/test';

export default defineConfig({
  retries: 2,
});
```

---

### Q: Can retries be configured per project?

**A:** Yes. Each project can have its own retry count.

```ts
projects: [
  {
    name: 'chromium',
    retries: 2,
  },
  {
    name: 'firefox',
    retries: 0,
  },
];
```

---

### Q: Can retries be overridden per test file?

**A:** Yes, using `test.describe.configure()`.

```ts
test.describe.configure({ retries: 1 });
```

---

## Test Result States

### Q: What happens if a test passes after retrying?

**A:** The test is marked as **flaky**.

---

### Q: What are the possible test outcomes when retries are enabled?

**A:**

* **passed** → passed on first attempt
* **flaky** → failed initially but passed on retry
* **failed** → failed all retry attempts

---

## Runtime Awareness

### Q: How can a test detect it is running as a retry?

**A:** By using `testInfo.retry`.

---

### Q: What does `testInfo.retry === 0` mean?

**A:** The test is running for the first time.

---

### Q: What does `testInfo.retry > 0` mean?

**A:** The test is being retried after a previous failure.

---

## Serial vs Parallel Execution (CRITICAL SECTION)

### Q: How do retries behave in **parallel mode**?

**A:**
Only the **failed test** is retried. Other tests are not re-run.

---

### Q: How do retries behave in **serial mode**?

**A:**
If **any test fails**, the **entire serial group is retried**.

---

### Q: Why does Playwright retry the whole serial group?

**A:**
Because serial tests may share state or depend on execution order, retrying only one test could leave the system inconsistent.

---

### Q: How do you enable serial execution?

```ts
test.describe.configure( { mode: 'serial' });

test.describe('serial suite', () => {
  test('test 1', async () => {});
  test('test 2', async () => {});
});
```

---

### Q: How do retries behave inside `test.describe.configure( { mode: 'serial' });`?

**A:**

* Entire group is retried
* Retry count applies to the group
* Order is preserved

---

### Q: How do retries behave in `test.describe.configure( { mode: 'parallel' });`?

**A:**
Only the failing test is retried.

---

## CI Considerations

### Q: Why are retries commonly enabled in CI?

**A:**
To reduce failures caused by:

* Infrastructure instability
* Network delays
* Browser startup issues

---

### Q: Why might retries be disabled in CI?

**A:**
To surface flaky tests clearly instead of masking them.

---

## Performance Impact

### Q: Do retries increase execution time?

**A:** Yes. Failing tests may run multiple times.

---

### Q: Should retries be used as a fix for flaky tests?

**A:** No. Retries reduce noise but do not fix root causes.

---

## Reporting & Visibility

### Q: How are retries shown in Playwright reports?

**A:**

* Each retry attempt is logged
* Tests passing after retry are marked **flaky**

---

### Q: Are retries visible in HTML and CI reports?

**A:** Yes. Retry attempts and flaky status are clearly reported.

---

## Best Practices (From the Docs’ Intent)

### Q: When should retries be used?

**A:**

* CI environments
* Known flaky areas
* Temporary stabilization

---

### Q: When should retries be avoided?

**A:**

* Stable, deterministic tests
* As a replacement for fixing test flakiness

---

## Interview-Grade Summary ⭐

### Q: Explain Playwright retries in one sentence.

**A:**
Retries allow Playwright to re-run failed tests to handle flakiness while clearly distinguishing passed, flaky, and failed results.

---

### Q: Serial vs Parallel retries (must-know answer)

**A:**
In parallel mode only the failing test is retried, while in serial mode the entire test group is retried to maintain state consistency.

---