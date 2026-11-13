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
- node --version, npm --version and npx cypress version:
- Step 4.3, failure message for the wrong title:
- Step 4.6, tool and calories in the answer of POST /api/pizza:
- Step 4.7, the line of the admin list that shows your pizza:
- Step 4.8, run 1, result, duration and pizza name:
- Step 4.8, run 2, result, duration and pizza name:
- Step 4.9 (optional), browser and result:

## Part B
1.
2.
3.
4.
5.
6.
7.