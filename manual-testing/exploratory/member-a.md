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
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

### Test ID: OWN-A-02

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

### Test ID: OWN-A-03

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

### Test ID: OWN-A-04

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

### Test ID: OWN-A-05

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

### Test ID: OWN-A-06

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

### Test ID: OWN-A-07

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

### Test ID: OWN-A-08

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

### Test ID: OWN-A-09

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

### Test ID: OWN-A-10

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

### Test ID: OWN-A-11

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Technique | Boundary value analysis on text length |
| Status | Not run |

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

Not recorded — test has not been executed.

#### Evidence

Not captured.

---

## Overall Observations

To be completed after execution.

## Next Question

To be completed after execution.
