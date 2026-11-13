# UI lab results

Tool parts that I chose: Part 3: Robot Framework and Part 4: Cypress

## Part 0
- Step 0.1, Chrome version: 157.0.8103.78
- Step 0.3, ChromeDriver version: 157.0.8103.78
- Step 0.4, locator of Pizza, Please!: `button[name="pizza-please"]`
- Step 0.4, locator of Excluded tools: `select`
- Step 0.4, locator of Must be vegetarian: `input#default-checkbox`
- Step 0.4, locator of Custom Pizza Name: `input#pizza-name`
- Step 0.4, Duplicate ID verification after clicking "Pizza, Please!":
  - `$$('#pizza-name').length` → 2 elements
  - `$$('input#pizza-name').length` → 1 element
  - Explanation: The ID `pizza-name` is used by two elements after generating a pizza. Using `input#pizza-name` selects only the input field and avoids ambiguity.

- Step 0.5, pizza name, tool and calories of the run by hand:
  - Pizza name: Lab Pizza 20261113-123500
  - Tool: Pizza cutter
  - Calories per slice: 450

| Step | Actual result | Pass or fail |
|------|---------------|--------------|
| 1 | QuickPizza home page opened. The heading "Looking to break out of your pizza routine?" was displayed. | PASS |
| 2 | Advanced mode was enabled. Max Calories per Slice, Excluded tools, Must be vegetarian, and Custom Pizza Name appeared. | PASS |
| 3 | Entered 600 calories, excluded Knife, checked Must be vegetarian, and entered Lab Pizza 20261113-123500. All values were displayed correctly. | PASS |
| 4 | The recommendation displayed Lab Pizza 20261113-123500, tool Pizza cutter, and 450 calories per slice. Knife was not used and calories were within the limit. | PASS |
| 5 | Clicked Love it! without logging in. The message "Please log in first." appeared. | PASS |
| 6 | Opened /admin and signed in using admin credentials. The "Latest pizza recommendations" list appeared. | PASS |
| 7 | Found Lab Pizza 20261113-123500 in the admin list with tool=Pizza cutter and ingredients_number=7, matching the latest recommendation in Step 4. | PASS |


## Part 3: Robot Framework
- robot --version: Robot Framework 7.5.1 (Python 3.13.17 on win32)
- Step 3.2, failure message for the wrong title: Title should have been 'Web Form' but was 'Web form'.
- Step 3.8, run 1, result, elapsed time and pizza name: PASS (1 test, 1 passed, 0 failed), 9.963 s, Lab Pizza 20261113-143508
- Step 3.8, run 2, result, elapsed time and pizza name: PASS (1 test, 1 passed, 0 failed), 10.058 s, Lab Pizza 20261113-143838

## Part 4: Cypress

- node --version, npm --version and npx cypress version: Node.js v26.13.1, npm 11.20.0, Cypress 16.2.1.
- Step 4.3, failure message for the wrong title: `Timed out retrying after 10000ms` — Expected `Wrong title`, but the actual page title was `Web form`. (Intentional failure; the correct title was restored and the test passed.)
- Step 4.6, tool and calories in the answer of POST /api/pizza: Tool = Pizza cutter, Calories per slice = 550.
- Step 4.7, the line of the admin list that shows your pizza: `Lab Pizza 20261113-163108 (tool=Pizza cutter, ingredients_number=6)`
- Step 4.8, run 1, result, duration and pizza name: PASS (2 passed, 0 failed), 00:18, Lab Pizza 20261113-163108.
- Step 4.8, run 2, result, duration and pizza name: PASS (2 passed, 0 failed), 00:19, Lab Pizza 20261113-164119.
- Step 4.9 (optional), browser and result: Not performed (optional).

## Part B

**1. Explain why the tests locate Max Calories per Slice through its label instead of its id. Propose a change to the page that would let a test use an id, and state why that change helps a tester.**

The tests use the label because the Max Calories per Slice input does not have a unique id that we can use. We can find the input by its label text instead. I would add an id such as `max-calories` to the input and connect the label to it using `for="max-calories"`. This would make the element easier to locate and reduce problems if the page layout changes.

**2. Step 7 of QP-01 compares the tool in the admin list with the tool in the recommendation. Identify the kind of test oracle that this check is, and describe one fault in QuickPizza that it would catch.**

This is a consistency test oracle because it compares the tool shown in two different places. In our Cypress test, the recommended tool was Pizza cutter, and the admin list also showed Pizza cutter. If the admin list saved or displayed a different tool, the test would fail. This helps us check that the recommendation data stays consistent.

**3. QP-01 never checks that the pizza is vegetarian. Propose a check that would, and state what the test would need from the page or from another source.**

I would add a check after receiving the pizza recommendation to verify that all ingredients are vegetarian. The test could compare the ingredient list with a list of allowed vegetarian ingredients. It would need the ingredient names from the API response or the page and a reliable source that identifies which ingredients are vegetarian. If a non-vegetarian ingredient is found, the test should fail.

**4. Compare the two tools that you used. Describe how each one waited for QuickPizza, how quickly you could write QP-01 with it, and how readable its report, log or video was.**

Robot Framework used SeleniumLibrary keywords and waits to check that elements were ready before continuing. Cypress automatically retried commands and assertions, and we also used `cy.wait('@pizza')` to wait for the API response. I found Cypress easier to write for QP-01 because the commands and assertions were in one JavaScript test, while Robot Framework needed keywords and a resource file. Robot Framework had useful HTML reports and logs, but Cypress videos and screenshots made it easier to see what happened during the test.

**5. Choose the tool that you would use for the automated UI tests of Project 2, and justify the choice with two reasons from this lab.**

I would choose Cypress for Project 2. First, Cypress automatically waits and retries assertions, so I did not need to write many manual waits. Second, it can intercept API requests and check the response together with the UI, like we did with `POST /api/pizza`. It also recorded screenshots and videos, which helped me check the test results.

**6. For Part 3, explain where you would change the locator of the calories box if QuickPizza changed it, and how the resource file keeps that change out of the test file.**

I would change the locator in `robot/resources/quickpizza.resource`, where the page locators and reusable keywords are defined. The test file `pizza_scenario.robot` uses those keywords instead of repeating the locator directly. If QuickPizza changes the calories input, I can update the locator in the resource file without changing the main test steps. This makes the test easier to maintain.

**7. For Part 4, explain why QP-01 has to be a single test in Cypress, which clears the cookies before each test, and what would go wrong if steps 6 and 7 were a second test.**

QP-01 needs to be a single Cypress test because its steps depend on the data and state from earlier steps. Cypress clears cookies between tests, so the login session would not automatically continue into another test. If steps 6 and 7 were moved to a second test, the pizza name and tool stored in the first test would also not be available through the same aliases. The second test could fail because it would not have the same data and session needed to check the admin list.