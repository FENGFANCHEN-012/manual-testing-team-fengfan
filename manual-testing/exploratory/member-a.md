# Self-Designed Testing — Member A

## Testing Idea

I want to test the length rules for First name and Surname on the Test Pages form, at both ends of each range.

## Reason

When I checked the baseline, the server rejected the first name `Alex` with "Firstname too short". The published rules only say the first name must be filled and be under 90 characters, so this did not make sense to me. I want to find out what the real limit is. I also picked Surname because it has a clear range (11 to 79), so it is a good field to practise boundary testing on (this is also suggested in section 18.2 of the brief).

## Test Basis

From the instructions page (8 Nov 2026):

- firstname must be filled
- firstname must be less than 90 chars
- surname should be between 11 and 79 chars

My assumptions:

- "Must be filled" has no minimum, so I treat any name that is not empty as valid.
- I take "between 11 and 79" to include 11 and 79.
- The rules do not say surname is required. I am assuming empty is invalid because 0 is not between 11 and 79.
- I only use normal English letters for now. No spaces, accents or emoji.

## Approach

I used boundary value analysis on the number of characters. For First name I tried 2, 3, 4 and 5 characters at the low end, because I do not know the real minimum, and 89 and 90 at the top. For Surname I tried 10 and 11, 79 and 80, and empty. Everything else stays at the baseline. For each test I wrote down which part reacted: the browser, the page's JavaScript or the server.

## Test Cases

### Test ID: OWN-A-01

| Item | Details |
|---|---|
| Test type | Negative? |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Fail |

#### Purpose

I want to see if a 2-letter first name is accepted.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| First name | `Al` (2 chars) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the first name to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

By the published rule it should be accepted, since it is filled and under 90. But because `Alex` failed, I am not sure.

#### Actual Result

Ran at 2:24 pm. The form did not submit. The page showed a red message under the field: "Firstname provided is too short". The browser itself did not complain. Nothing was sent to the server. This does not match the published rule, because the rule has no minimum. So it is a Fail against the requirement, or the requirement is missing a minimum.

#### Evidence

[View screenshot](../evidence/member-a/own-a-01.png)

---

### Test ID: OWN-A-02

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Fail |

#### Purpose

I want to see if a 3-letter first name is accepted.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| First name | `Ali` (3 chars) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the first name to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

Accepted.

#### Actual Result

Ran at 2:24 pm. The page let me submit. The server's Validation Report said "Firstname Error: Firstname too short". So the JavaScript was fine with 3 letters, but the server still rejected it. The two checks do not match.

#### Evidence

[View screenshot](../evidence/member-a/own-a-02.png)

---

### Test ID: OWN-A-03

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Fail |

#### Purpose

I want to try `Alex` again to make sure the baseline failure happens every time.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| First name | `Alex` (4 chars) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the first name to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

Accepted.

#### Actual Result

Ran at 2:24 pm. The page let me submit. The server's Validation Report said "Firstname Error: Firstname too short". Same as my baseline check, so the problem can be repeated.

#### Evidence

[View screenshot](../evidence/member-a/own-a-03.png)

---

### Test ID: OWN-A-04

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Pass |

#### Purpose

I want to check the 5-letter name I used as my new baseline.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| First name | `Alexa` (5 chars) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the first name to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

Accepted.

#### Actual Result

Ran at 2:24 pm. The page let me submit. The server's Validation Report said "Valid Input: Your Input passed validation".

#### Evidence

[View screenshot](../evidence/member-a/own-a-04.png)

---

### Test ID: OWN-A-05

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Pass |

#### Purpose

I want to check the longest first name that should be allowed.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| First name | `A` x 89 (89 chars) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the first name to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

Accepted, because 89 is less than 90.

#### Actual Result

Ran at 2:24 pm. The page let me submit. The server's Validation Report said "Valid Input: Your Input passed validation". The full 89-letter name showed under "You submitted".

#### Evidence

[View screenshot](../evidence/member-a/own-a-05.png)

---

### Test ID: OWN-A-06

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Pass |

#### Purpose

I want to check the shortest first name that is too long.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| First name | `A` x 90 (90 chars) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the first name to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

Rejected, because 90 is not less than 90.

#### Actual Result

Ran at 2:24 pm. The form did not submit. The page showed a red message under the field: "Firstname provided is too long". The browser itself did not complain. Nothing was sent to the server.

#### Evidence

[View screenshot](../evidence/member-a/own-a-06.png)

---

### Test ID: OWN-A-07

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Pass |

#### Purpose

I want to check a surname that is one character too short.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Surname | `S` x 10 (10 chars) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the surname to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

Rejected, because it is under 11.

#### Actual Result

Ran at 2:24 pm. The form did not submit. The page showed a red message under the field: "Surname provided is too short". The browser itself did not complain. Nothing was sent to the server.

#### Evidence

[View screenshot](../evidence/member-a/own-a-07.png)

---

### Test ID: OWN-A-08

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Pass |

#### Purpose

I want to check the shortest allowed surname.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Surname | `S` x 11 (11 chars) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the surname to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

Accepted.

#### Actual Result

Ran at 2:24 pm. The page let me submit. The server's Validation Report said "Valid Input: Your Input passed validation".

#### Evidence

[View screenshot](../evidence/member-a/own-a-08.png)

---

### Test ID: OWN-A-09

| Item | Details |
|---|---|
| Test type | Positive |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Pass |

#### Purpose

I want to check the longest allowed surname.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Surname | `S` x 79 (79 chars) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the surname to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

Accepted.

#### Actual Result

Ran at 2:24 pm. The page let me submit. The server's Validation Report said "Valid Input: Your Input passed validation".

#### Evidence

[View screenshot](../evidence/member-a/own-a-09.png)

---

### Test ID: OWN-A-10

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Pass |

#### Purpose

I want to check a surname that is one character too long.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Surname | `S` x 80 (80 chars) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the surname to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

Rejected, because it is over 79.

#### Actual Result

Ran at 2:24 pm. The form did not submit. The page showed a red message under the field: "Surname provided is too long". The browser itself did not complain. Nothing was sent to the server.

#### Evidence

[View screenshot](../evidence/member-a/own-a-10.png)

---

### Test ID: OWN-A-11

| Item | Details |
|---|---|
| Test type | Negative |
| Tester | member-a |
| Website | Test Pages validation form |
| Technique | Boundary value analysis on length |
| Status | Observation only |

#### Purpose

I want to see if an empty surname is accepted.

#### Preconditions

The form is open in a fresh page and all the other fields use the baseline (`Alexa` / `TestingStudent` / `30` / `Singapore` / `Manual testing classroom exercise`).

#### Test Data

| Field | Value |
|---|---|
| Surname | (left empty) |

#### Steps

1. Open the form.
2. Fill in the baseline.
3. Change only the surname to the test value.
4. Click Submit.
5. Write down what blocked it, if anything (browser, JavaScript or server), and the message.

#### Expected Result

Rejected, because 0 is not between 11 and 79. This is based on my assumption that surname is required.

#### Actual Result

Ran at 2:25 pm. The page let me submit. The server's Validation Report said "Valid Input: Your Input passed validation". The browser, the JavaScript and the server all accepted it. My expected result was only an assumption, because the rules never say surname is required. So I am recording this as an observation and a question, not a bug.

#### Evidence

[View screenshot](../evidence/member-a/own-a-11.png)

---

## Overall Observations

First name:

| Length | Page JavaScript | Server | Matches the published rule? |
|---|---|---|---|
| 2 | Rejected ("too short") | Never reached | No, the rule has no minimum |
| 3 | Allowed | Rejected ("too short") | No |
| 4 | Allowed | Rejected ("too short") | No |
| 5 | Allowed | Accepted | Yes |
| 89 | Allowed | Accepted | Yes |
| 90 | Rejected ("too long") | Never reached | Yes |

Surname:

| Length | Result | Matches the published rule? |
|---|---|---|
| empty | Accepted | Not clear, the rule does not say it is required |
| 10 | Rejected by JavaScript ("too short") | Yes |
| 11 | Accepted | Yes |
| 79 | Accepted | Yes |
| 80 | Rejected by JavaScript ("too long") | Yes |

What I found:

1. The surname limits work the way the rules say, at both ends.
2. The first name has three different minimums. The published rule has none, the page's JavaScript needs at least 3 letters, and the server needs at least 5. So someone called "Ali" or "Alex" would pass the page check and then get rejected by the server. This explains why the brief's baseline failed.
3. The 90-character upper limit for first name matches the rule on the page side.
4. An empty surname gets accepted. Whether that is right depends on a rule that is not written down.

What I am not sure about: I can only see what the server does with values the page lets through. For 2 letters and 90 letters the JavaScript stopped the form first, so I don't know what the server would do with them.

I did not change direction during the tests. The 3 and 4 letter results just confirmed what I saw with the baseline.

## Next Question

- What is the real minimum length for first name? I need to ask the Tutor before I can call it a bug.
- Does the server also block names of 90+ characters, or does it only rely on the JavaScript? I would need to test with JavaScript turned off, which is outside this practical.
- How does it count spaces, accents and emoji, like "Zoë" or "Mary Ann"?
- Is surname supposed to be required?
