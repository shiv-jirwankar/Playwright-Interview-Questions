# 🧠 Playwright Test Configuration — Interview Questions & Answers

## 📚 Table of Contents

1. [Introduction to Playwright Configuration](#introduction-to-playwright-configuration)
2. [Basic Configuration Options](#basic-configuration-options)
3. [Configuration File Structure & Syntax](#configuration-file-structure--syntax)
4. [Test Execution Control](#test-execution-control)
5. [Use Options (Browser / Context Settings)](#use-options-browser--context-settings)
6. [Projects Configuration](#projects-configuration)
7. [Web Server Configuration](#web-server-configuration)
8. [Advanced Config Concepts](#advanced-config-concepts)
9. [Environment Variables & Dynamic Configuration](#environment-variables--dynamic-configuration)
10. [Practical Scenarios](#practical-scenarios)

---

## 📌 Introduction to Playwright Configuration

### **1. What is the purpose of the Playwright configuration file?**

**Answer:**
The Playwright config file (`playwright.config.ts` or `playwright.config.js`) centralizes how tests are discovered and executed — such as test directories, timeouts, retries, reporting, emulation settings, projects, and more — so you don’t need to repeat settings in every test. ([Playwright][1])

---

### **2. What does the `defineConfig()` function do?**

**Answer:**
`defineConfig()` is a helper that wraps your configuration object to ensure proper type checking and editor IntelliSense. It’s imported from `@playwright/test`. Example:

```ts
import { defineConfig } from '@playwright/test';

export default defineConfig({
  testDir: 'tests',
});
```

([Playwright][1])

---

## 🛠️ Basic Configuration Options

### **3. What is `testDir` and why is it important?**

**Answer:**
`testDir` specifies the folder where Playwright should look for test files. Without this, Playwright will search default locations, but explicitly setting it keeps test discovery predictable. ([Playwright][1])

---

### **4. What does `fullyParallel` control?**

**Answer:**
When `fullyParallel: true`, tests in *all files* run in parallel (as opposed to parallelization only between files). Useful for speeding large suites. ([Playwright][1])

---

### **5. What is `forbidOnly`?**

**Answer:**
If `forbidOnly` is enabled (often in CI, e.g., `!!process.env.CI`), Playwright will error if any tests are marked with `test.only`, preventing accidental exclusion of tests. ([Playwright][1])

---

### **6. What does `retries` do?**

**Answer:**
`retries` configures how many times Playwright should re-run a test that fails before marking it as permanently failed. Example:

```ts
retries: process.env.CI ? 2 : 0,
```

([Playwright][1])

---

### **7. What is the `reporter` option?**

**Answer:**
`reporter` sets the reporter(s) Playwright uses to output results, such as `'list'`, `'html'`, or combining them:

```ts
reporter: [['list'], ['html', { open: 'never' }]],
```

([Playwright][1])

---

## 📐 Configuration File Structure & Syntax

### **8. How do you configure timeouts globally?**

**Answer:**
Use the `timeout` property in config to set maximum duration (in ms) for each test:

```ts
timeout: 30 * 1000, // 30s per test
```

([Playwright][1])

---

### **9. Can configuration values accept environment variables?**

**Answer:**
Yes — a config can reference environment variables, letting you dynamically adjust behavior:

```ts
forbidOnly: !!process.env.CI,
```

([Playwright][1])

---

## ▶️ Test Execution Control

### **10. How do you control number of workers via config?**

**Answer:**
The `workers` property defines how many parallel processes run tests. Set it to `1` for sequential runs or use an environment variable to adapt across environments. ([Playwright][1])

---

### **11. What’s the difference between `timeout` and `globalTimeout`?**

**Answer:**

* `timeout` applies to **individual tests**.
* `globalTimeout` applies to the **entire suite**, useful to prevent CI timeouts stalling indefinitely. ([Playwright][2])

---

## 🌐 Use Options (Browser / Context Settings)

The `use` field customizes Playwright contexts and browser behavior for every test. ([Playwright][3])

### **12. What is `baseURL` used for?**

**Answer:**
`baseURL` lets you navigate using relative paths inside tests:

```ts
use: { baseURL: 'http://localhost:3000' }
```

([Playwright][3])

---

### **13. How do you enable trace or video capture?**

**Answer:**
Inside `use`, you can specify:

```ts
trace: 'on-first-retry',
video: 'retain-on-failure',
screenshot: 'only-on-failure',
```

These capture traces, videos, or screenshots on failure, aiding debugging. ([Playwright][3])

---

### **14. How do emulation options work in config?**

**Answer:**
You can emulate mobile settings, locale, color scheme, geolocation, etc., via fields like `viewport`, `colorScheme`, `locale`, and more inside `use`. ([Playwright][3])

---

### **15. What is `storageState` useful for?**

**Answer:**
`storageState` allows you to set authenticated state (e.g., cookies) globally for tests, avoiding repeat logins. ([Playwright][3])

---

## 🧩 Projects Configuration

Projects let you run tests across multiple configurations — like different browsers or devices. ([Playwright][1])

### **16. What is a Playwright project?**

**Answer:**
A project groups tests with specific options, usually a browser and device combination, enabling cross-environment testing from a single config. ([Playwright][1])

---

### **17. How do you define a project for a specific browser?**

**Answer:**
Example of a Chromium project:

```ts
projects: [
  {
    name: 'chromium',
    use: { ...devices['Desktop Chrome'] },
  },
],
```

([Playwright][1])

---

### **18. How would you add a mobile emulation project?**

**Answer:**
Using device descriptors, e.g., Pixel 5:

```ts
{
  name: 'Mobile Chrome',
  use: { ...devices['Pixel 5'] },
}
```

([Playwright][4])

---

### **19. Can different projects have different use settings?**

**Answer:**
Yes — each project can override `use` options. For instance, you might set different locales per project. ([Playwright][3])

---

## 🔥 Web Server Configuration

### **20. What is `webServer` in config?**

**Answer:**
`webServer` lets Playwright start a local dev server before running tests:

```ts
webServer: {
  command: 'npm run start',
  url: 'http://localhost:3000',
  reuseExistingServer: true,
}
```

([Playwright][1])

---

### **21. How does `reuseExistingServer` work?**

**Answer:**
If `true`, Playwright won’t start a server if one is already running — useful in local dev or hot reload scenarios. ([Playwright][1])

---

## 📈 Advanced Config Concepts

### **22. What is the `expect` option in config?**

**Answer:**
`expect.timeout` globally configures how long assertion checks (like `toHaveText`) wait before failing. Example:

```ts
expect: { timeout: 5000 }
```

([timdeschryver.dev][5])

---

### **23. How can you exclude or include tests through config?**

**Answer:**
While test filtering is usually done via CLI flags, `testMatch` patterns or `testIgnore` can be used in config to change which files are discovered. ([Playwright][1])

---

### **24. What is `captureGitInfo`?**

**Answer:**
`captureGitInfo` configures whether to store commit and diff info in test metadata. Useful for traceability. ([Playwright][2])

---

### **25. What is `build.external`?**

**Answer:**
The `build.external` property excludes paths from Playwright’s transpilation, useful for large pre-bundled bundles. ([Playwright][2])

---

## 🚀 Environment Variables & Dynamic Configuration

### **26. Why use environment variables in config?**

**Answer:**
Environment variables allow configuration to change dynamically for CI vs local, staging vs production, etc. Example:

```ts
baseURL: process.env.BASE_URL
```

([Playwright][1])

---

### **27. How can environment variables drive retries or workers?**

**Answer:**
Often CI environments adjust retry counts and worker count:

```ts
workers: process.env.CI ? 1 : undefined,
```

([Playwright][1])

---

## 🧪 Practical Scenarios

### **28. How would you configure Playwright to run tests with video capture on failure?**

**Answer:**
In `use`:

```ts
video: 'retain-on-failure'
```

([Playwright][3])

---

### **29. How do you configure a base URL for all tests?**

**Answer:**
Set `baseURL` in `use`, so tests can navigate using relative paths.

```ts
use: { baseURL: 'https://staging.example.test' }
```

([Playwright][3])

---

### **30. How do projects help with cross-browser testing?**

**Answer:**
Projects let you define multiple browser targets in one config, and Playwright will run the test suite for each — e.g. Chromium, Firefox, WebKit. ([Playwright][1])

---

## 📌 Conclusion

Playwright’s configuration system is highly flexible, enabling:

✅ Centralized test suite settings
✅ Cross-browser & emulation projects
✅ Fine-grained control over `use`, timeouts, and retries
✅ Dynamic behavior via environment variables
✅ Integration with dev servers and CI pipelines

This Q&A set should prepare you deeply for interviews or real-world usage of Playwright Test Configuration. ([Playwright][1])

---
