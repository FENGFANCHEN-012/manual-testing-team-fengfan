# Team Summary

Solo submission: every record below was produced by member-a (FENGFANCHEN-012).

## Guided Testing Coverage

### Login Testing

Required coverage:
- Valid credentials.
- Incorrect password.
- Missing password.
- Missing username.
- Recovery after an invalid attempt.

Results: all 5 Pass — [LOGIN-P01](results/member-a.md#test-id-login-p01), [LOGIN-N01](results/member-a.md#test-id-login-n01), [LOGIN-N02](results/member-a.md#test-id-login-n02), [LOGIN-N03](results/member-a.md#test-id-login-n03), [LOGIN-R01](results/member-a.md#test-id-login-r01).

### Equivalence Partitioning

Required coverage:
- Age below the accepted range.
- Age within the accepted range.
- Age above the accepted range.

Results: [AGE-EP-10-A](results/member-a.md#test-id-age-ep-10-a) Pass (rejected), [AGE-EP-30-A](results/member-a.md#test-id-age-ep-30-a) Pass (accepted), [AGE-EP-90-A](results/member-a.md#test-id-age-ep-90-a) Pass (rejected).

Baseline note: the brief's first name `Alex` was rejected by the server, so the baseline uses `Alexa` — see [team plan](team-plan.md#agreed-baseline-data).

### Input-Format Observations

Required observations:
- Blank age.
- Non-numeric age input.

Results: [AGE-FMT-BLANK-A](results/member-a.md#test-id-age-fmt-blank-a): the browser blocked it as a required field. [AGE-FMT-ABC-A](results/member-a.md#test-id-age-fmt-abc-a): the letters could not be typed into the number field. Both are recorded as observations.

### 2-Point Boundary Testing

Required values:
17, 18, 80, 81.

Results: all Pass — [17](results/member-a.md#test-id-age-2p-17-a), [18](results/member-a.md#test-id-age-2p-18-a), [80](results/member-a.md#test-id-age-2p-80-a), [81](results/member-a.md#test-id-age-2p-81-a).

### 3-Point Boundary Testing

Required values:
16, 17, 18, 19, 79, 80, 81, 82.

Results: new executions all Pass — [16](results/member-a.md#test-id-age-3p-16-a), [19](results/member-a.md#test-id-age-3p-19-a), [79](results/member-a.md#test-id-age-3p-79-a), [82](results/member-a.md#test-id-age-3p-82-a). 17, 18, 80 and 81 reuse the 2-point executions (counted once).

## Member Contributions

### Member A

- Guided results: [View results](results/member-a.md)
- Self-designed tests: [View tests](exploratory/member-a.md)
- Reflection: [View reflection](reflections/member-a.md)
- Chosen investigation: First name and Surname length validation.
- Main observation: first-name minimum length differs between the published rule (none), the page's JavaScript (3) and the server (5); surname limits match the published 11–79.
- Pull request: https://github.com/FENGFANCHEN-012/manual-testing-team-fengfan/pull/1

## Team Conclusion

- The guided activities showed that test type (positive or negative) comes from the input, while status comes from comparing actual with expected results. They also showed that a few well-chosen partition and boundary values cover more behaviour than many random valid values.
- The open-ended testing extended boundary analysis to text fields. It showed that the form's three validation layers (HTML5, JavaScript, server) do not always agree with each other or with the published requirements.
- Next, we would get the intended first-name minimum and the surname-required rule confirmed, and then check how spaces, accents and emoji are counted in names.
