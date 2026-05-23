Playwright Java Automation Portfolio

A progressive series of automation projects built with
**Playwright for Java** and **TestNG**, starting from a single
end-to-end test and evolving into a full multi-browser, multi-layer
automation framework with API testing, trace debugging, and HTML reporting.

Each project in this portfolio builds directly on the previous one —
the same SauceDemo application is tested throughout so the focus stays
on the framework evolution, not on learning a new app with each task.

---

## 📁 Projects

| Project | Focus |
|---|---|
| [Multi-Browser Parallel Runs](#) | Chromium, Firefox, WebKit in parallel with ThreadLocal isolation |
| [User Workflow Automation](#) | Auth, forms, navigation, and data entry as reusable workflow classes |
| [Trace Viewer Integration](#) | Step-by-step debug traces and screenshots per test method |
| [API + UI Combined Tests](#) | Playwright APIRequestContext alongside browser tests |

---

## 🛠️ Core Stack

| Tool | Purpose |
|---|---|
| **Playwright 1.44** | Browser automation — Chromium, Firefox, WebKit bundled |
| **Java 21** | Core language |
| **TestNG 7.11** | Test framework, parallel execution, listeners |
| **ExtentReports 5** | HTML report with screenshots and trace links |
| **Jackson Databind** | JSON parsing for API responses |
| **Maven** | Build and dependency management |

---

## 🔑 Key Concepts Across the Portfolio

**Page Object Model** — every page has a dedicated class owning its
locators and interactions. Test classes never contain CSS selectors.

**Workflow layer** — sits above page objects and below tests. A workflow
method represents a complete user intention, not individual clicks.
`auth.loginAsStandardUser()` is one line in a test; the full interaction
sequence lives in `AuthWorkflow`.

**ThreadLocal parallelism** — `ThreadLocal<Page>` and
`ThreadLocal<BrowserContext>` ensure parallel browser runs are
completely isolated. Chromium, Firefox, and WebKit run simultaneously
without sharing any state.

**Playwright vs Selenium** — no WebDriver, no WebDriverManager, no
ChromeDriver. Playwright bundles its own browsers. `page.fill()` clears
before typing. `page.waitForLoadState()` replaces `Thread.sleep()`.
`setSlowMo()` paces every action globally.

**Trace Viewer** — every test method produces a `.zip` trace with
before/after DOM snapshots, screenshots, network requests, and Java
source references. Failed tests open the viewer automatically.

**API + UI combined** — `APIRequestContext` makes real HTTP calls
inside the same Playwright instance as the browser. Tests use the API
to set up state, drive the UI to interact with it, and assert both
layers agree.

**WebKit coverage** — Safari's browser engine is tested without
owning a Mac. Playwright's bundled WebKit runs on Windows and Linux.

---

## 🚀 Getting Started

```bash
# Clone any project
git clone <repo-url>
cd <project-folder>

# Install Playwright browsers — one-time per machine
mvn exec:java -e -D exec.mainClass=com.microsoft.playwright.CLI -D exec.args="install"

# Run all browsers in parallel
mvn test

# Run one browser
mvn test -Dsuite=testng-chromium
mvn test -Dsuite=testng-firefox
mvn test -Dsuite=testng-webkit
```

---

## 📊 Output Per Run

```
traces/
├── chromium/ └── <testName>.zip    # Open with: playwright show-trace
├── firefox/  └── ...
└── webkit/   └── ...

screenshots/
└── chromium/ └── <testName>_<timestamp>.png   # Failure only

reports/
└── ExtentReport.html               # Open in any browser
```
