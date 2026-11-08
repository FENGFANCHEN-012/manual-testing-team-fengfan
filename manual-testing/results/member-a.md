# Manual Testing Results — Member A

Solo submission: member-a (FENGFANCHEN-012) executes every guided test, including the ones the brief allocates to Members B–E.

## Environment

| Item | Details |
|---|---|
| Tester identifier | member-a |
| Date and time | 8 Nov 2026 (Singapore time); each test records its own run time |
| Browser and version | Chromium 151.0.7922.34 (driven through Playwright, headless) |
| Operating system | Windows 11 Home (10.0.26200) |

> Execution note: tests are executed in a real Chromium browser through Playwright. Inputs are typed key by key and the Submit / Login buttons are clicked, as a user would. Screenshots are saved under [evidence/member-a](../evidence/member-a/).

## Login Tests

### Test ID: LOGIN-P01

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | SauceDemo |
| Status | Pass |

#### Purpose

Check that valid credentials give access to the product inventory.

#### Preconditions

SauceDemo login page is open, the user is logged out and both fields are empty.

#### Test Data

| Field | Value |
|---|---|
| Username | `standard_user` |
| Password | `secret_sauce` |

#### Steps

1. Follow the shared starting procedure (logged out, both fields empty).
2. Enter the username.
3. Enter the password.
4. Select `Login`.
5. Observe the page reached.
6. Check that products are visible.

#### Expected Result

The inventory page appears and products are visible.

#### Actual Result

Executed 8 Nov 2026, 2:17 pm. After selecting Login, the browser moved to `/inventory.html`. The page title showed "Products" and 6 product items were listed. No error message appeared.

#### Evidence

[View screenshot](../evidence/member-a/login-p01.png)
---

### Test ID: LOGIN-N01

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | SauceDemo |
| Status | Pass |

#### Purpose

Check that an incorrect password is rejected while the username stays valid.

#### Preconditions

SauceDemo login page is open, the user is logged out and both fields are empty.

#### Test Data

| Field | Value |
|---|---|
| Username | `standard_user` |
| Password | `wrong_password` |

#### Steps

1. Follow the shared starting procedure.
2. Enter the valid username.
3. Enter the incorrect password.
4. Select `Login`.
5. Observe the page and feedback.

#### Expected Result

Login is rejected, error feedback appears, and the inventory is not reached.

#### Actual Result

Executed 8 Nov 2026, 2:18 pm. The page stayed on the login page (`/`). An error banner appeared: "Epic sadface: Username and password do not match any user in this service". No products were shown, so the inventory was not reached. The rejection is the expected behaviour, so this negative test passes.

#### Evidence

[View screenshot](../evidence/member-a/login-n01.png)
---

### Test ID: LOGIN-N02

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | SauceDemo |
| Status | Pass |

#### Purpose

Check that a missing password is rejected.

#### Preconditions

SauceDemo login page is open, the user is logged out and both fields are empty.

#### Test Data

| Field | Value |
|---|---|
| Username | `standard_user` |
| Password | Empty |

#### Steps

1. Follow the shared starting procedure.
2. Enter the username.
3. Leave the password empty.
4. Select `Login`.
5. Observe the feedback.

#### Expected Result

The attempt is rejected with validation feedback. The inventory is not reached.

#### Actual Result

Executed 8 Nov 2026, 2:18 pm. The page stayed on the login page. An error banner appeared: "Epic sadface: Password is required". The inventory was not reached.

#### Evidence

[View screenshot](../evidence/member-a/login-n02.png)
---

### Test ID: LOGIN-N03

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | SauceDemo |
| Status | Pass |

#### Purpose

Check that a missing username is rejected.

#### Preconditions

SauceDemo login page is open, the user is logged out and both fields are empty.

#### Test Data

| Field | Value |
|---|---|
| Username | Empty |
| Password | `secret_sauce` |

#### Steps

1. Follow the shared starting procedure.
2. Leave the username empty.
3. Enter the password.
4. Select `Login`.
5. Observe the feedback.

#### Expected Result

The attempt is rejected with validation feedback. The inventory is not reached.

#### Actual Result

Executed 8 Nov 2026, 2:19 pm. The page stayed on the login page. An error banner appeared: "Epic sadface: Username is required". The inventory was not reached.

#### Evidence

[View screenshot](../evidence/member-a/login-n03.png)
---

### Test ID: LOGIN-R01

| Item | Details |
|---|---|
| Test type | Recovery |
| Tester | member-a |
| Website | SauceDemo |
| Status | Pass |

#### Purpose

Check that a user can log in after correcting an invalid attempt, without resetting the page.

#### Preconditions

SauceDemo login page is open, the user is logged out and both fields are empty.

#### Test Data

| Field | Value |
|---|---|
| Username | `standard_user` (kept for both attempts) |
| Password | Attempt 1: `wrong_password`; attempt 2: `secret_sauce` |

#### Steps

1. Follow the shared starting procedure.
2. Enter `standard_user` and `wrong_password`.
3. Select `Login`.
4. Confirm rejection.
5. Replace the password with `secret_sauce`.
6. Keep the username unchanged.
7. Select `Login` again.
8. Check whether the inventory appears.

#### Expected Result

The invalid attempt is rejected. After correcting the password, login succeeds.

#### Actual Result

Executed 8 Nov 2026, 2:19 pm.

- Stage 1 (wrong password): the page stayed on the login page and showed "Epic sadface: Username and password do not match any user in this service". No products shown.
- Stage 2 (password replaced with `secret_sauce`, username left as typed, page not reloaded): the browser moved to `/inventory.html`, the title showed "Products" and 6 products were listed.

The invalid attempt did not block the later valid login.

#### Evidence

- [Stage 1 — rejected](../evidence/member-a/login-r01-stage1.png)
- [Stage 2 — inventory reached](../evidence/member-a/login-r01.png)
---

## Equivalence Partitioning

### Requirements Checked

Read on 8 Nov 2026 from the [instructions page](https://testpages.eviltester.com/apps/client-server-form-validation/client-server-form-validation-instructions/): firstname must be filled and be less than 90 chars; surname between 11 and 79 chars; age between 18 and 80; notes max 2000; country from list. Classroom model used: **age is a whole number, 18 ≤ age ≤ 80**.

### Baseline Check

| Attempt | First name | Result |
|---|---|---|
| Brief's baseline | `Alex` | Submitted, but the server returned **"Firstname Error — Firstname too short"**. [Screenshot](../evidence/member-a/base-01-alex.png) |
| Adjusted baseline | `Alexa` | Submitted, server returned **"Valid Input — Your Input passed validation"**. [Screenshot](../evidence/member-a/base-02-alexa.png) |

The brief's baseline failed although `Alex` (4 characters) meets the published rule "firstname must be filled". So the baseline was changed to `Alexa` (5 characters), with every other field unchanged, so that age tests are not affected by a first-name error. Requirement question raised in [team-plan.md](../team-plan.md#agreed-baseline-data). The first-name behaviour is investigated further in my [self-designed tests](../exploratory/member-a.md).

### Partitions

| Partition | Whole-number age group | Representative | Test type | Expected |
|---|---|---:|---|---|
| EP-01 | Below 18 | 10 | Negative | Reject |
| EP-02 | 18–80 inclusive | 30 | Positive | Accept |
| EP-03 | Above 80 | 90 | Negative | Reject |

"Reject" means successful submission is prevented, or the server returns a validation error for age.

### Test ID: AGE-EP-30-A

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Equivalence partitioning (EP-02: 18–80) |
| Status | Pass |

#### Purpose

Check that a representative age inside the valid partition is accepted.

#### Preconditions

The validation form is open in a fresh page. All other fields use the agreed valid baseline (First name `Alexa`, Surname `TestingStudent`, Country `Singapore`, Notes `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `30` |
| Other fields | Agreed valid baseline |

#### Steps

1. Open (restore) the validation form.
2. Enter the agreed baseline.
3. Replace age with `30` (typed).
4. Select Submit.
5. Observe the response.

#### Expected Result

Age 30 is accepted: the form submits and the server reports valid input with Age 30.

#### Actual Result

Executed 8 Nov 2026, 2:20:33 pm. The form submitted to the server (`/submit`). The server's Validation Report said: "Valid Input | Your Input passed validation". The "You submitted" section listed Age `30`. The input passed server validation.

#### Evidence

[View screenshot](../evidence/member-a/age-ep-30-a.png)

---

### Test ID: AGE-EP-10-A

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Equivalence partitioning (EP-01: below 18) |
| Status | Pass |

#### Purpose

Check that a representative age below the valid partition is rejected.

#### Preconditions

The validation form is open in a fresh page. All other fields use the agreed valid baseline (First name `Alexa`, Surname `TestingStudent`, Country `Singapore`, Notes `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `10` |
| Other fields | Agreed valid baseline |

#### Steps

1. Open (restore) the validation form.
2. Enter the agreed baseline.
3. Replace age with `10` (typed).
4. Select Submit.
5. Observe the response.

#### Expected Result

Age 10 is rejected because it is below the minimum of 18 (submission prevented or a validation error returned).

#### Actual Result

Executed 8 Nov 2026, 2:20:39 pm. Selecting Submit did **not** send the form: the page stayed on the form URL and no Validation Report appeared. The browser's built-in (HTML5) validation blocked it with the message `age`: "Value must be greater than or equal to 18." The age field contained `10` at submit time. This rejection came from the browser, not from the server.

#### Evidence

[View screenshot](../evidence/member-a/age-ep-10-a.png)

---

### Test ID: AGE-EP-90-A

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Equivalence partitioning (EP-03: above 80) |
| Status | Pass |

#### Purpose

Check that a representative age above the valid partition is rejected.

#### Preconditions

The validation form is open in a fresh page. All other fields use the agreed valid baseline (First name `Alexa`, Surname `TestingStudent`, Country `Singapore`, Notes `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `90` |
| Other fields | Agreed valid baseline |

#### Steps

1. Open (restore) the validation form.
2. Enter the agreed baseline.
3. Replace age with `90` (typed).
4. Select Submit.
5. Observe the response.

#### Expected Result

Age 90 is rejected because it is above the maximum of 80 (submission prevented or a validation error returned).

#### Actual Result

Executed 8 Nov 2026, 2:20:45 pm. Selecting Submit did **not** send the form: the page stayed on the form URL and no Validation Report appeared. The browser's built-in (HTML5) validation blocked it with the message `age`: "Value must be less than or equal to 80." The age field contained `90` at submit time. This rejection came from the browser, not from the server.

#### Evidence

[View screenshot](../evidence/member-a/age-ep-90-a.png)

---

### Test ID: AGE-FMT-BLANK-A

| Item | Details |
|---|---|
| Test type | Negative (input-format observation) |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Input-format observation |
| Status | Observation only |

#### Purpose

Observe how the form handles a blank age.

#### Preconditions

The validation form is open in a fresh page. All other fields use the agreed valid baseline (First name `Alexa`, Surname `TestingStudent`, Country `Singapore`, Notes `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | Empty |
| Other fields | Agreed valid baseline |

#### Steps

1. Open (restore) the validation form.
2. Enter the agreed baseline.
3. Clear the age field and leave it empty.
4. Select Submit.
5. Observe the response.

#### Expected Result

Requirement question: the published requirements say "age between 18 and 80" but do not say whether age is mandatory. Observe whether blank age is prevented, cleared or rejected, and what feedback appears.

#### Actual Result

Executed 8 Nov 2026, 2:20:51 pm. Selecting Submit did **not** send the form: the page stayed on the form URL and no Validation Report appeared. The browser's built-in (HTML5) validation blocked it with the message `age`: "Please fill out this field." The age field contained `(empty)` at submit time. This rejection came from the browser, not from the server.

Observation: blank age is treated as required. The `required` attribute on the age field (HTML5) is what blocks it. The published requirement list does not state that age is required, so this is recorded as an observation, not Pass/Fail.

#### Evidence

[View screenshot](../evidence/member-a/age-fmt-blank-a.png)

---

### Test ID: AGE-FMT-ABC-A

| Item | Details |
|---|---|
| Test type | Negative (input-format observation) |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Input-format observation |
| Status | Observation only |

#### Purpose

Observe how the form handles non-numeric age input.

#### Preconditions

The validation form is open in a fresh page. All other fields use the agreed valid baseline (First name `Alexa`, Surname `TestingStudent`, Country `Singapore`, Notes `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `abc` (typed key by key) |
| Other fields | Agreed valid baseline |

#### Steps

1. Open (restore) the validation form.
2. Enter the agreed baseline.
3. Clear the age field and type `abc`.
4. Select Submit.
5. Observe the response.

#### Expected Result

Requirement question: the requirements do not describe non-numeric input. Observe whether `abc` can be entered and how it is handled.

#### Actual Result

Executed 8 Nov 2026, 2:20:57 pm. Selecting Submit did **not** send the form: the page stayed on the form URL and no Validation Report appeared. The browser's built-in (HTML5) validation blocked it with the message `age`: "Please fill out this field." The age field contained `(empty)` at submit time. This rejection came from the browser, not from the server.

Observation: the letters could not be entered. The age field is an HTML `type="number"` input, so the browser discarded the typed letters and the field stayed empty. The form was then blocked as an empty required field. The input was **prevented by the browser**; the server never saw `abc`.

#### Evidence

[View screenshot](../evidence/member-a/age-fmt-abc-a.png)

---


### Discussion Checkpoint

Testing only 25, 40 and 60 would choose three values from the **same** valid partition (18–80). Each would be expected to behave the same way, so they add almost nothing, and the two invalid partitions (below 18 and above 80) would never be exercised. A form that accepted every age would pass all three tests.


## 2-Point Boundary Tests

Transitions: `17 → 18` (invalid → valid) and `80 → 81` (valid → invalid). Values tested: 17, 18, 80, 81. In this solo submission member-a executes all four (the brief splits them across A–D).

### Test ID: AGE-2P-17-A

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | 2-point boundary testing |
| Status | Pass |

#### Purpose

Check that age 17, immediately below the minimum of 18, is rejected.

#### Preconditions

The validation form is open in a fresh page. All other fields use the agreed valid baseline (First name `Alexa`, Surname `TestingStudent`, Country `Singapore`, Notes `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `17` |
| Other fields | Agreed valid baseline |

#### Steps

1. Open (restore) the validation form.
2. Enter the agreed baseline.
3. Replace age with `17` (typed).
4. Select Submit.
5. Observe the response.

#### Expected Result

Age 17 is rejected because it is below 18 (submission prevented or a validation error returned).

#### Actual Result

Executed 8 Nov 2026, 2:22:19 pm. Selecting Submit did **not** send the form: the page stayed on the form URL and no Validation Report appeared. The browser's built-in (HTML5) validation blocked it with the message `age`: "Value must be greater than or equal to 18." The age field contained `17` at submit time. This rejection came from the browser, not from the server.

#### Evidence

[View screenshot](../evidence/member-a/age-2p-17-a.png)

---

### Test ID: AGE-2P-18-A

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | 2-point boundary testing |
| Status | Pass |

#### Purpose

Check that age 18, the minimum valid age, is accepted.

#### Preconditions

The validation form is open in a fresh page. All other fields use the agreed valid baseline (First name `Alexa`, Surname `TestingStudent`, Country `Singapore`, Notes `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `18` |
| Other fields | Agreed valid baseline |

#### Steps

1. Open (restore) the validation form.
2. Enter the agreed baseline.
3. Replace age with `18` (typed).
4. Select Submit.
5. Observe the response.

#### Expected Result

Age 18 is accepted: the form submits and the server reports valid input with Age 18.

#### Actual Result

Executed 8 Nov 2026, 2:22:25 pm. The form submitted to the server (`/submit`). The server's Validation Report said: "Valid Input | Your Input passed validation". The "You submitted" section listed Age `18`. The input passed server validation.

#### Evidence

[View screenshot](../evidence/member-a/age-2p-18-a.png)

---

### Test ID: AGE-2P-80-A

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | 2-point boundary testing |
| Status | Pass |

#### Purpose

Check that age 80, the maximum valid age, is accepted.

#### Preconditions

The validation form is open in a fresh page. All other fields use the agreed valid baseline (First name `Alexa`, Surname `TestingStudent`, Country `Singapore`, Notes `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `80` |
| Other fields | Agreed valid baseline |

#### Steps

1. Open (restore) the validation form.
2. Enter the agreed baseline.
3. Replace age with `80` (typed).
4. Select Submit.
5. Observe the response.

#### Expected Result

Age 80 is accepted: the form submits and the server reports valid input with Age 80.

#### Actual Result

Executed 8 Nov 2026, 2:22:31 pm. The form submitted to the server (`/submit`). The server's Validation Report said: "Valid Input | Your Input passed validation". The "You submitted" section listed Age `80`. The input passed server validation.

#### Evidence

[View screenshot](../evidence/member-a/age-2p-80-a.png)

---

### Test ID: AGE-2P-81-A

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | 2-point boundary testing |
| Status | Pass |

#### Purpose

Check that age 81, immediately above the maximum of 80, is rejected.

#### Preconditions

The validation form is open in a fresh page. All other fields use the agreed valid baseline (First name `Alexa`, Surname `TestingStudent`, Country `Singapore`, Notes `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `81` |
| Other fields | Agreed valid baseline |

#### Steps

1. Open (restore) the validation form.
2. Enter the agreed baseline.
3. Replace age with `81` (typed).
4. Select Submit.
5. Observe the response.

#### Expected Result

Age 81 is rejected because it is above 80 (submission prevented or a validation error returned).

#### Actual Result

Executed 8 Nov 2026, 2:22:37 pm. Selecting Submit did **not** send the form: the page stayed on the form URL and no Validation Report appeared. The browser's built-in (HTML5) validation blocked it with the message `age`: "Value must be less than or equal to 80." The age field contained `81` at submit time. This rejection came from the browser, not from the server.

#### Evidence

[View screenshot](../evidence/member-a/age-2p-81-a.png)

---


### Interpretation

- **Why is 18 a positive boundary test?** 18 is a valid input (the lowest allowed age), so the expected result is acceptance. It would catch a mistake such as `age > 18` instead of `age >= 18`; testing 30 would not.
- **Why is 17 a negative boundary test?** 17 is invalid input. The test passes when the form rejects it, which it did.
- **Why is testing only 18 and 80 incomplete?** They only show that the valid edges are accepted. Without 17 and 81 we would not know whether the invalid side of each edge is rejected (for example a check written as `age >= 17` would still accept 18).

Observation: on this form the rejections of 17 and 81 came from the browser's HTML5 `min="18" max="80"` attributes, before the request reached the server. The page's own JavaScript check (visible in the page source) only rejects ages below 16 or above 100, so the three layers of validation do not agree. Server-side behaviour for 17 and 81 was **not** tested, because that needs requests outside normal browser use.

## 3-Point Boundary Tests
