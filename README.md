# Integrate App Automate with Harness

This repository demonstrates how to run Appium tests using [WebdriverIO](http://webdriver.io/) on BrowserStack App Automate, locally and through a Harness CI/CD pipeline.

---

## Prerequisites

* **Node.js 8.11.2+**: Download it from the [official Node.js website](https://nodejs.org/en/) if not already installed.
* **BrowserStack Account**: Active [BrowserStack App Automate](https://www.google.com/search?q=https://www.browserstack.com/app-automate) credentials (Username and Access Key).
* **Harness Account**: An active Harness account with pipeline configuration privileges.

---

## 1. Local Run Setup

### Dependency Installation

Navigate to the platform directory you wish to test and install the required packages:

* **Android:**
```bash
cd android
npm install

```


* **iOS:**
```bash
cd ios
npm install

```



### Getting Started & Running Tests Locally

* **First Test:**
* Test script location: `run-first-test` directory under [`./android`](https://www.google.com/search?q=./android) or [`./ios`](https://www.google.com/search?q=./ios).
* Follow the [BrowserStack First Test Guide](https://www.browserstack.com/docs/app-automate/appium/getting-started/nodejs/webdriverio).


* **Parallel Testing:**
* Test script location: `run-parallel-test` directory under [`./android`](https://www.google.com/search?q=./android) or [`./ios`](https://www.google.com/search?q=./ios).
* Run command: `npm run test`
* Follow the [BrowserStack Parallel Testing Guide](https://www.browserstack.com/docs/app-automate/appium/getting-started/nodejs/webdriverio/parallelize-tests).
* Use the [Parallel Test Calculator](https://www.browserstack.com/automate/parallel-calculator?ref=github) to estimate required sessions.


* **Local Testing (Private/Internal Environments):**
* Test script location: `run-local-test` directory under [`./android`](https://www.google.com/search?q=./android) or [`./ios`](https://www.google.com/search?q=./ios).
* Run command: `npm run local`
* Follow the [BrowserStack Local Testing Guide](https://www.browserstack.com/docs/app-automate/appium/getting-started/nodejs/webdriverio/local-testing).



---

## 2. CI/CD Setup with Harness

Integrate your Appium test suite into a Harness CI/CD pipeline to execute tests automatically on BrowserStack.

### References

* **Documentation:** [BrowserStack Harness Integration Guide](https://www.browserstack.com/docs/automate/selenium/harness?fw-lang=nodejs%2Fwebdriverio)
* **Video Walkthrough:** [Harness Setup Video Reference](https://zoom.us/clips/share/qevoVuX7TyeyVCP7fQBzXA)

---

### Step 1: Configure Harness Secrets & Environment Variables

Add your BrowserStack credentials and build metadata to your Harness Pipeline Environment Variables or Stage Variables using the following expression syntax:

| Environment Variable Name | Harness Secret Expression / Value |
| --- | --- |
| `BROWSERSTACK_USERNAME` | `<+secrets.getValue("browserstack_username")>` |
| `BROWSERSTACK_ACCESS_KEY` | `<+secrets.getValue("browserstack_access_key")>` |
| `BUILD_NUMBER` | `<+pipeline.sequenceId>` |

---

### Step 2: Add Pipeline Run Step

In your Harness pipeline stage, add a **Run** (or **Shell Script**) step to install dependencies and trigger test execution:

```bash
# Install dependencies and execute parallel WebdriverIO tests on App Automate
cd android && npm install && npx wdio run-parallel-test/parallel.conf.js --mochaOpts.grep "always passing"

```
