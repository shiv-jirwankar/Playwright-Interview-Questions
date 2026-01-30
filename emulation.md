# **Playwright Emulation — Interview Questions & Answers**

## 📚 Table of Contents

1. [Introduction to Playwright Emulation](#introduction-to-playwright-emulation)
2. [Device Emulation](#device-emulation)
3. [Viewport Configuration](#viewport-configuration)
4. [User Agent Emulation](#user-agent-emulation)
5. [Touch & Mobile Emulation](#touch--mobile-emulation)
6. [Locale & Timezone Emulation](#locale--timezone-emulation)
7. [Permissions & Geolocation](#permissions--geolocation)
8. [Color Scheme Emulation](#color-scheme-emulation)
9. [Example Configurations](#example-configurations)
10. [Best Practices](#best-practices)

---

## **Introduction to Playwright Emulation**

### **1. What is device emulation in Playwright?**

**Answer:**
Device emulation with Playwright lets you **simulate browser behavior from real devices** such as phones, tablets, and desktops. It mimics things like viewport dimensions, user agent, screen size, device pixel ratio, and touchscreen support to test responsive layouts and device-specific behavior. ([Playwright][1])

---

### **2. Why do we use emulation in E2E tests?**

**Answer:**
Emulation is crucial to ensure your application **works correctly on different devices and environments** without requiring a real physical device or external emulators. It helps catch layout issues, UX regressions, and environment-specific behaviors early in tests. ([Playwright][1])

---

## **Device Emulation**

### **3. How does Playwright define emulated devices?**

**Answer:**
Playwright provides a built-in `devices` registry containing presets for desktop, tablet, and mobile devices. These presets bundle settings like `viewport`, `userAgent`, `deviceScaleFactor`, and `hasTouch` to simulate the target device. ([Playwright][1])

---

### **4. How do you use a device preset in Playwright config?**

**Answer:**
Import `devices` from `@playwright/test` and spread the desired device settings into your project `use` options:

```ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
  projects: [
    {
      name: 'Mobile Safari',
      use: {
        ...devices['iPhone 13'],
      },
    },
  ],
});
```

This configures tests to run with parameters emulating an iPhone 13. ([Playwright][1])

---

## **Viewport Configuration**

### **5. What is viewport emulation in Playwright?**

**Answer:**
Viewport emulation sets the **width and height of the browser viewport** to simulate screens of different sizes. This is part of device configuration but can also be overridden manually in test code if needed. ([Playwright][1])

---

### **6. How can you override the default viewport emulation?**

**Answer:**
You can override viewport size either in config or inside tests:

```ts
// In config
use: {
  viewport: { width: 1280, height: 720 },
}
```

Inside a test:

```ts
await page.setViewportSize({ width: 1600, height: 1200 });
```

This helps tailor screens for specific scenarios. ([Playwright][1])

---

## **User Agent Emulation**

### **7. What does user agent emulation do?**

**Answer:**
User agent emulation changes the **browser client string** sent to the server to match a specific device’s behavior (e.g., mobile Safari or desktop Chrome), allowing server-side logic or responsive CSS to trigger correctly. ([Playwright][1])

---

### **8. How do you set a custom user agent?**

**Answer:**
In config:

```ts
use: {
  userAgent: 'My Custom User Agent String',
}
```

Or as part of a device preset (which includes userAgent already). ([Playwright][1])

---

## **Touch & Mobile Emulation**

### **9. How does Playwright emulate touch support?**

**Answer:**
Device presets set `hasTouch` and other properties automatically. When a preset includes touch support, Playwright will emulate touch events such as tap, scroll, and pinch gestures in tests. ([Playwright][1])

---

### **10. What is the role of `deviceScaleFactor`?**

**Answer:**
`deviceScaleFactor` represents the **ratio of physical pixels to CSS pixels** and helps simulate high-density displays like Retina screens. It’s part of emulation settings in device presets. ([Playwright][2])

---

## **Locale & Timezone Emulation**

### **11. How can you emulate a specific locale?**

**Answer:**
Setting the `locale` option configures user language and formatting behavior in the browser context:

```ts
use: {
  locale: 'en-GB',
}
```

Useful to test i18n and localization features. ([Playwright][1])

---

### **12. How do you simulate a timezone?**

**Answer:**
Use the `timezoneId` option to emulate a specific timezone for your tests:

```ts
use: {
  timezoneId: 'Europe/Paris',
}
```

This tests features dependent on local time (e.g., relative dates). ([Playwright][1])

---

## **Permissions & Geolocation**

### **13. How does Playwright handle browser permissions in emulation?**

**Answer:**
Use the `permissions` option to automatically grant required permissions to pages:

```ts
use: {
  permissions: ['geolocation'],
}
```

This ensures tests don’t get blocked by permission prompts. ([Playwright][1])

---

### **14. How do you emulate geolocation in a test?**

**Answer:**
Set the `geolocation` option with coordinates while granting permission:

```ts
use: {
  geolocation: { latitude: 41.889938, longitude: 12.492507 },
  permissions: ['geolocation'],
}
```

This simulates position for features like location-based content. ([Playwright][3])

---

## **Color Scheme Emulation**

### **15. What is color scheme emulation?**

**Answer:**
Playwright can simulate the user’s preferred color scheme (`'light'` or `'dark'`), allowing testing of UI themes controlled by CSS media queries like `prefers-color-scheme`. ([Playwright][3])

---

### **16. How do you emulate dark mode?**

**Answer:**

```ts
use: {
  colorScheme: 'dark',
}
```

This tests UI components under dark mode conditions. ([Playwright][3])

---

## **Example Configurations**

### **17. Provide a full example of emulation settings in `playwright.config.ts`.**

**Answer:**
Here’s a sample config using multiple emulation options:

```ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
  use: {
    ...devices['Desktop Chrome'],
    locale: 'en-GB',
    timezoneId: 'Europe/Paris',
    colorScheme: 'dark',
    geolocation: { latitude: 41.889938, longitude: 12.492507 },
    permissions: ['geolocation'],
  },
});
```

This runs all tests with a desktop browser that simulates locale, timezone, dark theme, and geolocation. ([Playwright][3])

---

### **18. How do you combine device presets with custom overrides?**

**Answer:**
You can merge device presets with custom settings:

```ts
use: {
  ...devices['iPhone 13'],
  colorScheme: 'dark',
}
```

This retains all iPhone 13 emulation and adds dark mode. ([Playwright][1])

---

## **Best Practices**

### **19. Why should emulation be part of test suite configuration instead of individual tests?**

**Answer:**
Setting emulation globally ensures consistency across the suite, reduces boilerplate in individual tests, and prevents version skew between test cases. Group-level overrides are used only for specific test variations. ([Playwright][3])

---

### **20. What common pitfalls should be avoided when using emulation?**

**Answer:**

* Running too many combinations unnecessarily (slows tests)
* Not validating responsive behavior on real devices for critical UI
* Missing permission grants, causing unexpected popup blocks

Emulation is fast and efficient, but testing on real hardware setup can catch deeper platform-specific issues. ([Playwright][1])

---

## **Summary**

Playwright’s emulation capabilities allow you to simulate:

🔹 Device viewport and DPI
🔹 User agent strings
🔹 Touch and mobile behavior
🔹 Geolocation and permissions
🔹 Locale and timezone
🔹 Color schemes (dark/light)

all within test contexts configured via `playwright.config.ts`. ([Playwright][1])

---

If you want, I can convert this into a **developer cheat sheet**, **multiple-choice quiz**, or a **ready-to-use config template** with emulation presets!

[1]: https://playwright.dev/docs/emulation"
[2]: https://playwright.dev/docs/api/class-browser"
[3]: https://playwright.dev/docs/test-use-options"
