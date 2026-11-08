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

## 2-Point Boundary Tests

## 3-Point Boundary Tests
