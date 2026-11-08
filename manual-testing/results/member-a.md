# Manual Testing Results — Member A

I did this practical on my own, so I ran all the guided tests myself, including the ones the brief gives to Members B to E.

## Environment

| Item | Details |
|---|---|
| Tester identifier | member-a |
| Date and time | 8 Nov 2026, around 2:15 pm to 2:25 pm (SGT). I put the time for each test in its actual result. |
| Browser and version | Chromium 151.0.7922.34 |
| Operating system | Windows 11 Home (10.0.26200) |

Note: I used a small Playwright script to open Chromium and type the inputs into the pages, then click Login or Submit. Every test was really run against the live websites, and I took a screenshot after each one. The screenshots are in [evidence/member-a](../evidence/member-a/).

## Login Tests

For every login test I started from the login page, logged out, with both fields empty.

### Test ID: LOGIN-P01

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | SauceDemo |
| Status | Pass |

#### Purpose

I want to check that a valid username and password let me into the product page.

#### Preconditions

I am on the SauceDemo login page, logged out, and both fields are empty.

#### Test Data

| Field | Value |
|---|---|
| Username | `standard_user` |
| Password | `secret_sauce` |

#### Steps

1. Open the login page and make sure I am logged out.
2. Type the username.
3. Type the password.
4. Click `Login`.
5. Check which page I land on and whether products show.

#### Expected Result

I should get to the inventory page and see the products.

#### Actual Result

Ran at 2:17 pm. After I clicked Login, it went to `/inventory.html`. The title said "Products" and I could see 6 products. No error came up.

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

I want to check that a wrong password does not let me in. I keep the username correct so only the password is wrong.

#### Preconditions

I am on the SauceDemo login page, logged out, and both fields are empty.

#### Test Data

| Field | Value |
|---|---|
| Username | `standard_user` |
| Password | `wrong_password` |

#### Steps

1. Open the login page and make sure I am logged out.
2. Type the correct username.
3. Type the wrong password.
4. Click `Login`.
5. Look at the page and any error.

#### Expected Result

Login should be rejected, an error should show, and I should not see the inventory.

#### Actual Result

Ran at 2:18 pm. I stayed on the login page and a red error showed: "Epic sadface: Username and password do not match any user in this service". No products were shown. This is what I expected, so the negative test passes.

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

I want to check that I cannot log in without a password.

#### Preconditions

I am on the SauceDemo login page, logged out, and both fields are empty.

#### Test Data

| Field | Value |
|---|---|
| Username | `standard_user` |
| Password | (left empty) |

#### Steps

1. Open the login page and make sure I am logged out.
2. Type the username.
3. Leave the password empty.
4. Click `Login`.
5. Look at the error.

#### Expected Result

Login should be rejected with a message, and I should not see the inventory.

#### Actual Result

Ran at 2:18 pm. I stayed on the login page and the error said "Epic sadface: Password is required". The inventory did not open.

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

I want to check that I cannot log in without a username.

#### Preconditions

I am on the SauceDemo login page, logged out, and both fields are empty.

#### Test Data

| Field | Value |
|---|---|
| Username | (left empty) |
| Password | `secret_sauce` |

#### Steps

1. Open the login page and make sure I am logged out.
2. Leave the username empty.
3. Type the password.
4. Click `Login`.
5. Look at the error.

#### Expected Result

Login should be rejected with a message, and I should not see the inventory.

#### Actual Result

Ran at 2:19 pm. I stayed on the login page and the error said "Epic sadface: Username is required". The inventory did not open.

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

I want to check that after a failed login, I can fix the password and log in without reloading the page.

#### Preconditions

I am on the SauceDemo login page, logged out, and both fields are empty.

#### Test Data

| Field | Value |
|---|---|
| Username | `standard_user` (same for both tries) |
| Password | 1st try `wrong_password`, 2nd try `secret_sauce` |

#### Steps

1. Open the login page and make sure I am logged out.
2. Type `standard_user` and `wrong_password`.
3. Click `Login`.
4. Check that it is rejected.
5. Clear the password and type `secret_sauce`.
6. Leave the username as it is.
7. Click `Login` again.
8. Check if the inventory shows.

#### Expected Result

The first try should be rejected. After fixing the password, the second try should log me in.

#### Actual Result

Ran at 2:19 pm.

- 1st try: I stayed on the login page with the error "Epic sadface: Username and password do not match any user in this service".
- 2nd try: after I changed only the password, it went to `/inventory.html`, the title said "Products" and 6 products showed.

So the failed try did not stop me from logging in afterwards.

#### Evidence

- [1st try, rejected](../evidence/member-a/login-r01-stage1.png)
- [2nd try, logged in](../evidence/member-a/login-r01.png)

---

## Equivalence Partitioning

### Requirements I checked

I read the [instructions page](https://testpages.eviltester.com/apps/client-server-form-validation/client-server-form-validation-instructions/) on 8 Nov 2026. It says the first name must be filled and be less than 90 chars, the surname should be 11 to 79 chars, age between 18 and 80, notes max 2000, and the country must be from the list. For age I used the classroom model: a whole number from 18 to 80, both included.

### Baseline check

Before testing age I submitted the baseline from the brief to make sure it passes.

| Try | First name | What happened |
|---|---|---|
| Brief's baseline | `Alex` | The server said "Firstname Error: Firstname too short". [Screenshot](../evidence/member-a/base-01-alex.png) |
| My changed baseline | `Alexa` | The server said "Valid Input: Your Input passed validation". [Screenshot](../evidence/member-a/base-02-alexa.png) |

This surprised me. `Alex` is filled in and is shorter than 90 characters, so by the published rules it should be fine. Since the baseline has to pass, I changed the first name to `Alexa` and kept everything else the same. That way, if an age gets rejected, I know it is because of the age and not the first name. I wrote this down as a question in the [team plan](../team-plan.md#agreed-baseline-data) and looked into it more in my [own tests](../exploratory/member-a.md).

### Partitions

| Partition | Ages | Value I picked | Type | Expected |
|---|---|---:|---|---|
| EP-01 | below 18 | 10 | Negative | Reject |
| EP-02 | 18 to 80 | 30 | Positive | Accept |
| EP-03 | above 80 | 90 | Negative | Reject |

"Reject" here means the form is stopped from submitting, or the server returns an error for age.

### Test ID: AGE-EP-30-A

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Equivalence partitioning (EP-02) |
| Status | Pass |

#### Purpose

I want to check that an age in the middle of the valid range is accepted.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `30` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `30`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 30 should be accepted. The form should submit and the server should say the input is valid.

#### Actual Result

Ran at 2:20 pm. The form went through to the server. The Validation Report said "Valid Input: Your Input passed validation" and under "You submitted" the age was 30.

#### Evidence

[View screenshot](../evidence/member-a/age-ep-30-a.png)

---

### Test ID: AGE-EP-10-A

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Equivalence partitioning (EP-01) |
| Status | Pass |

#### Purpose

I want to check that an age below the valid range is rejected.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `10` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `10`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 10 should be rejected because it is below 18. Either the form is blocked or the server gives an error.

#### Actual Result

Ran at 2:20 pm. The form did not submit. The browser popped up "Value must be greater than or equal to 18." next to the age box and I stayed on the form page. This was the browser's own check (the HTML `min`/`max` on the field), so the server never got this value.

#### Evidence

[View screenshot](../evidence/member-a/age-ep-10-a.png)

---

### Test ID: AGE-EP-90-A

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Equivalence partitioning (EP-03) |
| Status | Pass |

#### Purpose

I want to check that an age above the valid range is rejected.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `90` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `90`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 90 should be rejected because it is above 80. Either the form is blocked or the server gives an error.

#### Actual Result

Ran at 2:20 pm. The form did not submit. The browser popped up "Value must be less than or equal to 80." next to the age box and I stayed on the form page. This was the browser's own check (the HTML `min`/`max` on the field), so the server never got this value.

#### Evidence

[View screenshot](../evidence/member-a/age-ep-90-a.png)

---

### Test ID: AGE-FMT-BLANK-A

| Item | Details |
|---|---|
| Test type | Negative (observation) |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Input format observation |
| Status | Observation only |

#### Purpose

I want to see what the form does when age is left empty.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | (left empty) |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to empty.
4. Click Submit.
5. See what happens.

#### Expected Result

I am not sure. The rules say "age between 18 and 80" but do not say age is required. I just want to see what happens.

#### Actual Result

Ran at 2:20 pm. The form did not submit. The browser showed "Please fill out this field." on the age box.

So in practice age is required, because the field has the HTML `required` attribute. The published rules do not say this, so I am recording it as an observation and not giving it a Pass or Fail.

#### Evidence

[View screenshot](../evidence/member-a/age-fmt-blank-a.png)

---

### Test ID: AGE-FMT-ABC-A

| Item | Details |
|---|---|
| Test type | Negative (observation) |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Input format observation |
| Status | Observation only |

#### Purpose

I want to see what happens if I type letters into the age box.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `abc` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `abc`.
4. Click Submit.
5. See what happens.

#### Expected Result

The rules do not cover letters, so I do not have a clear expected result. I want to see if I can even type them.

#### Actual Result

Ran at 2:20 pm. I could not type the letters. The age box is a number field, so it just stayed empty. When I clicked Submit, the browser said "Please fill out this field."

So `abc` was blocked by the browser while typing. The server never saw it.

#### Evidence

[View screenshot](../evidence/member-a/age-fmt-abc-a.png)

---

### Discussion

If I only tested 25, 40 and 60, all three are in the same valid group (18 to 80). They would all behave the same, and I would never test what happens below 18 or above 80. A form that accepts every age would still pass those three tests.

## 2-Point Boundary Tests

The two edges are 17 to 18 (invalid to valid) and 80 to 81 (valid to invalid), so I tested 17, 18, 80 and 81.

### Test ID: AGE-2P-17-A

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | 2-point boundary testing |
| Status | Pass |

#### Purpose

I want to check age 17, which is just below the minimum.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `17` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `17`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 17 should be rejected because it is below 18. Either the form is blocked or the server gives an error.

#### Actual Result

Ran at 2:22 pm. The form did not submit. The browser popped up "Value must be greater than or equal to 18." next to the age box and I stayed on the form page. This was the browser's own check (the HTML `min`/`max` on the field), so the server never got this value.

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

I want to check age 18, which is the lowest valid age.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `18` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `18`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 18 should be accepted. The form should submit and the server should say the input is valid.

#### Actual Result

Ran at 2:22 pm. The form went through to the server. The Validation Report said "Valid Input: Your Input passed validation" and under "You submitted" the age was 18.

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

I want to check age 80, which is the highest valid age.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `80` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `80`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 80 should be accepted. The form should submit and the server should say the input is valid.

#### Actual Result

Ran at 2:22 pm. The form went through to the server. The Validation Report said "Valid Input: Your Input passed validation" and under "You submitted" the age was 80.

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

I want to check age 81, which is just above the maximum.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `81` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `81`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 81 should be rejected because it is above 80. Either the form is blocked or the server gives an error.

#### Actual Result

Ran at 2:22 pm. The form did not submit. The browser popped up "Value must be less than or equal to 80." next to the age box and I stayed on the form page. This was the browser's own check (the HTML `min`/`max` on the field), so the server never got this value.

#### Evidence

[View screenshot](../evidence/member-a/age-2p-81-a.png)

---

### What I learned

- 18 is a positive test because it is a valid age. It is the value that would catch a bug like `age > 18` instead of `age >= 18`. Testing 30 would never find that.
- 17 is a negative test because it is invalid. The test passes because the form correctly rejected it.
- Testing only 18 and 80 is not enough. They only show that the valid edges work. Without 17 and 81 I would not know if the invalid side is really blocked.

One thing I noticed: 17 and 81 were blocked by the browser (the HTML `min="18"` and `max="80"`), not by the server. When I looked at the page source, the JavaScript check only rejects ages under 16 or over 100. So the browser, the JavaScript and the published rule do not all agree. I did not test what the server does with 17 or 81, because that would mean going around the browser, which is outside normal use.

## 3-Point Boundary Tests

I used the ISTQB 3-value way: for each boundary value (17, 18, 80, 81), test the value before it, the value itself and the value after it. Without repeats that gives 16, 17, 18, 19, 79, 80, 81, 82.

I already tested 17, 18, 80 and 81, so this time I only needed to run 16, 19, 79 and 82.

### Ages 17, 18, 80 and 81 (reused)

- Original tests: `AGE-2P-17-A`, `AGE-2P-18-A`, `AGE-2P-80-A`, `AGE-2P-81-A`
- Tester: `member-a` (me)
- Record: [2-Point Boundary Tests](#2-point-boundary-tests) in this same file
- Why I reused them: same browser, same baseline, same steps, done a few minutes earlier on the same day.

### Test ID: AGE-3P-16-A

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | 3-point boundary testing |
| Status | Pass |

#### Purpose

I want to check age 16, which is next to boundary value 17.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `16` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `16`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 16 should be rejected because it is below 18. Either the form is blocked or the server gives an error.

#### Actual Result

Ran at 2:22 pm. The form did not submit. The browser popped up "Value must be greater than or equal to 18." next to the age box and I stayed on the form page. This was the browser's own check (the HTML `min`/`max` on the field), so the server never got this value.

#### Evidence

[View screenshot](../evidence/member-a/age-3p-16-a.png)

---

### Test ID: AGE-3P-19-A

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | 3-point boundary testing |
| Status | Pass |

#### Purpose

I want to check age 19, which is just inside the minimum.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `19` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `19`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 19 should be accepted. The form should submit and the server should say the input is valid.

#### Actual Result

Ran at 2:22 pm. The form went through to the server. The Validation Report said "Valid Input: Your Input passed validation" and under "You submitted" the age was 19.

#### Evidence

[View screenshot](../evidence/member-a/age-3p-19-a.png)

---

### Test ID: AGE-3P-79-A

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | 3-point boundary testing |
| Status | Pass |

#### Purpose

I want to check age 79, which is just inside the maximum.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `79` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `79`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 79 should be accepted. The form should submit and the server should say the input is valid.

#### Actual Result

Ran at 2:22 pm. The form went through to the server. The Validation Report said "Valid Input: Your Input passed validation" and under "You submitted" the age was 79.

#### Evidence

[View screenshot](../evidence/member-a/age-3p-79-a.png)

---

### Test ID: AGE-3P-82-A

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | 3-point boundary testing |
| Status | Pass |

#### Purpose

I want to check age 82, which is next to boundary value 81.

#### Preconditions

The validation form is open in a fresh page. All the other fields use our baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Age | `82` |
| Other fields | Baseline |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the age to `82`.
4. Click Submit.
5. See what happens.

#### Expected Result

Age 82 should be rejected because it is above 80. Either the form is blocked or the server gives an error.

#### Actual Result

Ran at 2:23 pm. The form did not submit. The browser popped up "Value must be less than or equal to 80." next to the age box and I stayed on the form page. This was the browser's own check (the HTML `min`/`max` on the field), so the server never got this value.

#### Evidence

[View screenshot](../evidence/member-a/age-3p-82-a.png)

---

### Comparing the three methods

| Method | Valid values | Invalid values | Result |
|---|---|---|---|
| Equivalence partitioning | 30 | 10, 90 | All as expected |
| 2-point boundary | 18, 80 | 17, 81 | All as expected |
| 3-point boundary | 18, 19, 79, 80 | 16, 17, 81, 82 | All as expected |

### Discussion

3-point testing added the values just inside the range (19 and 79) and one step further out (16 and 82). These would catch off-by-one mistakes that 2-point might miss. But it still does not prove every input works. I only tried 12 whole numbers, in one browser, through the normal page. I did not try decimals like 18.5, negative numbers, very big numbers, or what the server does if the browser check is skipped.
