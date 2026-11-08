# Self-Designed Testing — Member A

## Testing Idea

Investigate the **length rules for First name and Surname** on the Test Pages validation form, at both ends of each allowed range.

## Reason

The brief's own baseline first name `Alex` was rejected by the server with "Firstname too short", even though the published rule only says the first name must be filled and be under 90 characters. That suggests the length checks are not what the requirements say. Surname has a clear published range (11–79), so it is a good place to apply boundary testing to a second field (brief section 18.2).

## Test Basis

Published requirements (instructions page, read 8 Nov 2026):

- firstname must be filled
- firstname must be less than 90 chars
- surname should be between 11 and 79 chars

Assumptions and unclear points:

- "Must be filled" gives no minimum length, so any non-empty name is treated as valid.
- "Between 11 and 79" is read as inclusive (11 and 79 are valid).
- The requirement does not say whether surname is mandatory; I assume empty is invalid because 0 is outside 11–79.
- Length is counted in plain ASCII characters only (no spaces, accents or emoji in this round).

## Approach

Boundary value analysis on text length. First name: lower end (2, 3, 4, 5 characters, because the exact minimum is unknown) and upper end (89, 90). Surname: 2-point boundaries 10/11 and 79/80, plus empty. All other fields stay at the agreed baseline so that any rejection can be linked to the field under test. For every case I record which layer reacted: browser (HTML5), the page's JavaScript, or the server's Validation Report.

## Test Cases

### Test ID: OWN-A-01

| Item | Details |
|---|---|
| Test type | Negative? — see expected |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Fail |

#### Purpose

Check whether a 2-character first name is accepted.

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Firstname | `Al` (2 chars) |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the firstname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Per the published rule (must be filled, < 90 chars) a 2-character name should be **accepted**. Question: the brief's baseline `Alex` was rejected, so is there an unpublished minimum?

#### Actual Result

Executed 8 Nov 2026, 2:24:02 pm. Selecting Submit did not send the form. The page's JavaScript showed the red message "Firstname provided is too short" under the field. The browser's HTML5 checks did not object. No request reached the server. This contradicts the published rule (only "must be filled"), so it is a Fail against the published requirement — or the requirement is missing a minimum length.

#### Evidence

[View screenshot](../evidence/member-a/own-a-01.png)
---

### Test ID: OWN-A-02

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Fail |

#### Purpose

Check whether a 3-character first name is accepted.

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Firstname | `Ali` (3 chars) |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the firstname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Accepted (filled and < 90 chars).

#### Actual Result

Executed 8 Nov 2026, 2:24:08 pm. The browser and the page's JavaScript allowed the form through and it was submitted. The server's Validation Report said "Firstname Error — Firstname too short". So the JavaScript accepted 3 characters but the **server** rejected them: client and server disagree.

#### Evidence

[View screenshot](../evidence/member-a/own-a-02.png)
---

### Test ID: OWN-A-03

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Fail |

#### Purpose

Re-check the 4-character name that failed the baseline, to confirm the result is repeatable.

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Firstname | `Alex` (4 chars) |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the firstname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Accepted (filled and < 90 chars).

#### Actual Result

Executed 8 Nov 2026, 2:24:14 pm. The browser and the page's JavaScript allowed the form through and it was submitted. The server's Validation Report said "Firstname Error — Firstname too short". Same result as the baseline check, so the rejection of `Alex` is repeatable.

#### Evidence

[View screenshot](../evidence/member-a/own-a-03.png)
---

### Test ID: OWN-A-04

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Pass |

#### Purpose

Check the 5-character name used as the adjusted baseline.

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Firstname | `Alexa` (5 chars) |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the firstname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Accepted.

#### Actual Result

Executed 8 Nov 2026, 2:24:20 pm. The browser and the page's JavaScript allowed the form through and it was submitted. The server's Validation Report said "Valid Input — Your Input passed validation".

#### Evidence

[View screenshot](../evidence/member-a/own-a-04.png)
---

### Test ID: OWN-A-05

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Pass |

#### Purpose

Check the longest allowed first name (upper boundary, valid side).

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Firstname | `A` × 89 (89 chars) |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the firstname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Accepted (89 < 90).

#### Actual Result

Executed 8 Nov 2026, 2:24:26 pm. The browser and the page's JavaScript allowed the form through and it was submitted. The server's Validation Report said "Valid Input — Your Input passed validation". The 89-character name was listed in "You submitted".

#### Evidence

[View screenshot](../evidence/member-a/own-a-05.png)
---

### Test ID: OWN-A-06

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Pass |

#### Purpose

Check the shortest too-long first name (upper boundary, invalid side).

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Firstname | `A` × 90 (90 chars) |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the firstname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Rejected (90 is not less than 90).

#### Actual Result

Executed 8 Nov 2026, 2:24:32 pm. Selecting Submit did not send the form. The page's JavaScript showed the red message "Firstname provided is too long" under the field. The browser's HTML5 checks did not object. No request reached the server.

#### Evidence

[View screenshot](../evidence/member-a/own-a-06.png)
---

### Test ID: OWN-A-07

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Pass |

#### Purpose

Check a surname one character below the minimum.

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Surname | `S` × 10 (10 chars) |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the surname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Rejected (surname must be 11–79 chars).

#### Actual Result

Executed 8 Nov 2026, 2:24:38 pm. Selecting Submit did not send the form. The page's JavaScript showed the red message "Surname provided is too short" under the field. The browser's HTML5 checks did not object. No request reached the server.

#### Evidence

[View screenshot](../evidence/member-a/own-a-07.png)
---

### Test ID: OWN-A-08

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Pass |

#### Purpose

Check the minimum valid surname length.

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Surname | `S` × 11 (11 chars) |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the surname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Accepted.

#### Actual Result

Executed 8 Nov 2026, 2:24:44 pm. The browser and the page's JavaScript allowed the form through and it was submitted. The server's Validation Report said "Valid Input — Your Input passed validation".

#### Evidence

[View screenshot](../evidence/member-a/own-a-08.png)
---

### Test ID: OWN-A-09

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Pass |

#### Purpose

Check the maximum valid surname length.

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Surname | `S` × 79 (79 chars) |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the surname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Accepted.

#### Actual Result

Executed 8 Nov 2026, 2:24:50 pm. The browser and the page's JavaScript allowed the form through and it was submitted. The server's Validation Report said "Valid Input — Your Input passed validation".

#### Evidence

[View screenshot](../evidence/member-a/own-a-09.png)
---

### Test ID: OWN-A-10

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Pass |

#### Purpose

Check a surname one character above the maximum.

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Surname | `S` × 80 (80 chars) |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the surname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Rejected.

#### Actual Result

Executed 8 Nov 2026, 2:24:57 pm. Selecting Submit did not send the form. The page's JavaScript showed the red message "Surname provided is too long" under the field. The browser's HTML5 checks did not object. No request reached the server.

#### Evidence

[View screenshot](../evidence/member-a/own-a-10.png)
---

### Test ID: OWN-A-11

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Observation only |

#### Purpose

Check whether an empty surname is accepted.

#### Preconditions

Validation form open in a fresh page; all other fields use the agreed baseline (`Alexa` / `TestingStudent` / age `30` / `Singapore` / notes).

#### Test Data

| Field | Value |
|---|---|
| Surname | Empty |

#### Steps

1. Open the validation form.
2. Enter the agreed baseline.
3. Replace the surname with the test value (typed).
4. Select Submit.
5. Record whether the browser blocks it, whether the page's JavaScript shows an error, and what the server's Validation Report says.

#### Expected Result

Rejected, because 0 characters is not between 11 and 79. Assumption: "between 11 and 79" also means the surname is required (the requirement does not say so explicitly).

#### Actual Result

Executed 8 Nov 2026, 2:25:02 pm. The browser and the page's JavaScript allowed the form through and it was submitted. The server's Validation Report said "Valid Input — Your Input passed validation". The empty surname was accepted by the browser, the JavaScript and the server. My expected result relied on an **assumption** that surname is required; the requirement does not say this, so I record it as an observation and a requirement question rather than a defect.

#### Evidence

[View screenshot](../evidence/member-a/own-a-11.png)
---

## Overall Observations

| Length | First name: JavaScript | First name: server | Matches published rule? |
|---|---|---|---|
| 2 | Rejected ("too short") | Not reached | No — rule has no minimum |
| 3 | Allowed | Rejected ("too short") | No |
| 4 | Allowed | Rejected ("too short") | No |
| 5 | Allowed | Accepted | Yes |
| 89 | Allowed | Accepted | Yes |
| 90 | Rejected ("too long") | Not reached | Yes |

| Length | Surname result | Matches published rule? |
|---|---|---|
| 0 (empty) | Accepted everywhere | Unclear — requirement does not say surname is required |
| 10 | Rejected by JavaScript ("too short") | Yes |
| 11 | Accepted by server | Yes |
| 79 | Accepted by server | Yes |
| 80 | Rejected by JavaScript ("too long") | Yes |

What the tests showed:

1. **Surname length rules work as published** at both boundaries (10/11 and 79/80).
2. **First name has three different minimums**: the published rule has none, the page's JavaScript requires at least 3 characters, and the server requires at least 5. A user typing a real 3- or 4-character name (e.g. "Ali", "Alex") passes the on-page checks and is then rejected by the server. This is why the brief's baseline `Alex` failed.
3. The upper first-name limit (under 90) matches the requirement on the client side.
4. An empty surname is accepted. Whether that is correct depends on an unanswered requirement question.

Uncertainty: I can only see the server's behaviour for inputs that the browser lets through. For 2 characters and 90 characters I do not know what the server would do, because the JavaScript stopped the form first.

Change of direction: none. The results followed the plan; the 3/4-character results confirmed the baseline observation.

## Next Question

- What is the intended minimum first-name length? This needs an answer from the requirement owner (Tutor) before calling it a defect.
- Does the server also reject 90+ characters, or does it rely only on the JavaScript check? (Would need testing with JavaScript disabled, outside this practical's normal browser use.)
- How are spaces, accents and emoji counted (e.g. "Zoë", "Mary Ann")?
- Is surname meant to be required?
