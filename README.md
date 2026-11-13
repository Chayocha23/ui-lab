# UI Testing Lab

This repository contains my work for the ITCS386 Software Verification and Validation UI Testing Lab.

I chose two tools for this lab:
- Part 3: Robot Framework
- Part 4: Cypress

The tests use the Selenium Web Form and QuickPizza websites to practice automated UI testing.

## Part 3: Robot Framework

The `robot/` folder contains the Robot Framework test files for the Web Form and QuickPizza scenarios.

The `robot/resources/` folder contains reusable keywords and locators. The `robot/results/` folder contains the test reports and logs from two test runs.

### How to Run

Install the required packages:

```powershell
pip install -r robot/requirements.txt
```

Set the ChromeDriver path in Windows PowerShell:

```powershell
$env:CHROMEDRIVER = "C:\path\to\chromedriver.exe"
```

Replace the example path with the actual location of ChromeDriver on your computer.

Run the tests from the repository root:

```powershell
robot --outputdir robot/results robot/
```

## Part 4: Cypress

The `cypress/` folder contains the Cypress project and its configuration files.

The `cypress/cypress/e2e/` folder contains the Web Form and QuickPizza test scripts. The `cypress/cypress/support/` folder contains custom commands, while the `cypress/cypress/screenshots/` and `cypress/cypress/videos/` folders contain evidence from the test runs.

### How to Run

Open the Cypress folder:

```bash
cd cypress
```

Install the dependencies:

```bash
npm install
```

Run all tests in Chrome:

```bash
npx cypress run --browser chrome
```

## Test Results

Both Robot Framework and Cypress tests passed in two runs.

The detailed results are recorded in `RESULTS.md`. Screenshots, videos, and Robot Framework reports are included as test evidence.