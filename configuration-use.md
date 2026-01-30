Great — I found the official **Playwright Test Use Options** documentation and related API info. Using that, here is a **complete interview-ready Markdown guide** covering the *entire page* at:

🔗 [https://playwright.dev/docs/test-use-options](https://playwright.dev/docs/test-use-options) ([Playwright][1])

This includes all possible topics, **questions + detailed answers + examples**.

---

# Playwright Test Use Options — Interview Questions & Answers

## 📚 Table of Contents

1. [What *Use Options* Are](#what-use-options-are)
2. [Where Use Options Are Applied](#where-use-options-are-applied)
3. [Available Use Options](#available-use-options)
4. [Overriding Use Options](#overriding-use-options)
5. [Resetting Use Options](#resetting-use-options)
6. [Mobile & Emulation Settings](#mobile--emulation-settings)
7. [Context Options](#context-options)
8. [Browser Launch Options](#browser-launch-options)
9. [Storage State & Authentication](#storage-state--authentication)
10. [Timeouts in Use Options](#timeouts-in-use-options)
11. [Practical Interview Scenarios](#practical-interview-scenarios)

---

## 🧩 What Use Options Are

### **1. What are *Use Options* in Playwright Test?**

**Answer:**
Use options (provided via the `use` field in the Playwright config) configure **environmental and browser/context settings** that are applied when tests run. They help control browser behavior (like viewport, locale, baseURL, userAgent) and test behavior (like screenshots, trace, video). ([Playwright][1])

---

### **2. Why are *Use Options* important?**

**Answer:**
They provide a centralized way to configure things like **navigation behavior, emulation, and debugging artifacts** across all tests — essential for consistent test execution. ([Playwright][1])

---

## 📍 Where Use Options Are Applied

### **3. Where can you set Use Options?**

**Answer:**
Use options can be set at three scopes:

1. **Globally** in the Playwright config
2. **Per project** in the config
3. **Per test or test group** using `test.use(...)` ([Playwright][1])

---

### **4. What is the hierarchy of Use Options?**

**Answer:**

1. **Global config** applies to all tests
2. **Project config** overrides global
3. **Per-test `test.use`** overrides project/global ([Playwright][1])

---

## 🧰 Available Use Options

**Note:** Playwright supports *many* options in the `use` section; here are the most commonly used ones (source: Playwright API TestOptions summary). ([Playwright][2])

---

### **5. What is `baseURL` and how do you use it?**

**Answer:**
`baseURL` sets a base path so tests can use relative URLs:

```ts
use: {
  baseURL: 'https://example.com',
},
```

This lets you write:

```ts
await page.goto('/login');
```

which becomes `https://example.com/login`. ([Playwright][2])

---

### **6. How do you control screenshot capture via use options?**

**Answer:**

```ts
use: {
  screenshot: 'only-on-failure',
}
```

This captures screenshots only when a test fails. ([Playwright][2])

---

### **7. What are trace options?**

**Answer:**

```ts
use: {
  trace: 'on-first-retry',
}
```

This collects execution trace only on first retry, helpful for debugging. ([Playwright][2])

---

### **8. How does the `headless` option work?**

**Answer:**

```ts
use: {
  headless: false,
}
```

Runs tests with visible browsers instead of headless. ([Playwright][2])

---

### **9. Give examples of viewport settings.**

**Answer:**
You can set viewport dimensions:

```ts
use: {
  viewport: { width: 1280, height: 720 },
}
```

Useful for responsive tests. ([Playwright][2])

---

### **10. What is `ignoreHTTPSErrors`?**

**Answer:**
Allow tests to run even if HTTPS certificates are invalid:

```ts
use: {
  ignoreHTTPSErrors: true,
}
```

Useful for local dev or staging. ([Playwright][2])

---

### **11. How to accept downloaded files automatically?**

**Answer:**

```ts
use: {
  acceptDownloads: true,
}
```

This instructs Playwright to automatically accept downloads. ([Playwright][2])

---

### **12. How to set HTTP credentials?**

**Answer:**

```ts
use: {
  httpCredentials: { username: 'admin', password: 'pass' }
}
```

Used for basic auth. ([Playwright][2])

---

### **13. What does `extraHTTPHeaders` do?**

**Answer:**
Adds custom headers to every request:

```ts
use: {
  extraHTTPHeaders: { 'x-api-token': 'abc123' }
}
```

Used for API auth/test headers. ([Playwright][2])

---

## 🔄 Overriding Use Options

### **14. How do you override options for a specific test?**

**Answer:**

```ts
import { test } from '@playwright/test';

test.use({ locale: 'fr-FR' });

test('French locale test', async ({ page }) => {
  // ...
});
```

This runs that test with French locale. ([Playwright][1])

---

### **15. Can you override options inside `test.describe` blocks?**

**Answer:**
Yes — you can group multiple tests and apply use options to all of them:

```ts
test.describe('Locale group', () => {
  test.use({ locale: 'de-DE' });
  // tests here will use German locale
});
```

This is useful for grouping related config. ([Playwright][1])

---

## 🔁 Resetting Use Options

### **16. How do you reset an overridden option to config default?**

**Answer:**
You can set the option to `undefined` to go back to the config default:

```ts
test.describe(() => {
  test.use({ baseURL: undefined });
  // resets to config setting
});
```

This is how you “opt out” of overrides. ([Playwright][1])

---

## 📱 Mobile & Emulation Settings

### **17. How do you emulate a mobile device using use options?**

**Answer:**
You use Playwright’s `devices` presets:

```ts
import { devices } from '@playwright/test';

use: {
  ...devices['iPhone 13'],
}
```

This sets viewport, user agent, etc., like a real device. ([Playwright][1])

---

### **18. What mobile features can be emulated?**

**Answer:**

* Viewport
* Touch support
* User agent
* Device scale
* Geolocation
* Color scheme ([Playwright][3])

---

## 🌐 Context Options

### **19. What are context options in the use section?**

**Answer:**
Context options define the browser context behavior, such as locale, timezoneId, colorScheme, geolocation, permissions, extraHTTPHeaders, and more. These are passed to `browser.newContext()` automatically. ([Playwright][2])

---

### **20. Give an example of setting geolocation.**

**Answer:**

```ts
use: {
  geolocation: { latitude: 40.7128, longitude: -74.0060 },
  permissions: ['geolocation'],
}
```

This simulates GPS location and allows geolocation prompts. ([Playwright][2])

---

## 🧠 Browser Launch Options

### **21. Can you set launch options via use options?**

**Answer:**
Yes — many browser launch options can be set in use, like channel, slowMo, viewport, etc. However, not all launch options should be in use; some need to be in `launchOptions`. (See API TestOptions doc for specifics.) ([Playwright][2])

---

### **22. What does slowMo do?**

**Answer:**
Not strictly part of use, but via `launchOptions` you can slow down actions:

```ts
use: {
  launchOptions: { slowMo: 100 },
}
```

This slows automation speed for debugging. ([Playwright][2])

---

## 🗄️ Storage State & Authentication

### **23. What is `storageState`?**

**Answer:**
Specifies a file that stores authenticated state (cookies/localStorage). Useful to reuse login session across tests:

```ts
use: {
  storageState: 'auth.json',
}
```

This avoids logging in every time. ([CircleCI][4])

---

## ⏱️ Timeouts in Use Options

### **24. What is `actionTimeout`?**

**Answer:**
Sets maximum time (ms) each action (like `click()`) can take:

```ts
use: {
  actionTimeout: 5000,
}
```

This is applied before failing the action. ([Playwright][2])

---

### **25. What does `navigationTimeout` control?**

**Answer:**
The maximum time a navigation (`page.goto()`) can take. Often set separately from `timeout`. ([Playwright][2])

---

## 🧪 Practical Interview Scenarios

### **26. How do you run only selected use options for a group of tests?**

**Answer:**
By using `test.describe` with `test.use` inside:

```ts
test.describe('feature A', () => {
  test.use({ colorScheme: 'dark' });
  // tests here use dark theme
});
```

Useful when components behave differently under themes. ([Playwright][1])

---

### **27. When would you override `baseURL` locally?**

**Answer:**
When some tests target a different environment, like staging or a section of your app:

```ts
test.use({ baseURL: 'https://staging.example.com' });
```

Overrides the global setting. ([Playwright][1])

---

### **28. How can you combine multiple use options?**

**Answer:**
You can set many use options together:

```ts
use: {
  baseURL: 'https://example.com',
  viewport: { width: 800, height: 600 },
  trace: 'on-first-retry',
},
```

Each option composes to customize the environment. ([Playwright][2])

---

## 📌 Summary

Use options allow deep customization of the Playwright test environment, including:

✅ Browsers
✅ Context settings
✅ Timeouts
✅ Authentication state
✅ Screenshots & trace collection
✅ Emulation & device simulation ([Playwright][1])

---
