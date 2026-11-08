# Team Summary

I did this practical alone, so everything below is my own work (member-a).

## Guided Testing Coverage

### Login Testing

Required coverage:
- Valid credentials.
- Incorrect password.
- Missing password.
- Missing username.
- Recovery after an invalid attempt.

Results: all 5 passed. [LOGIN-P01](results/member-a.md#test-id-login-p01), [LOGIN-N01](results/member-a.md#test-id-login-n01), [LOGIN-N02](results/member-a.md#test-id-login-n02), [LOGIN-N03](results/member-a.md#test-id-login-n03), [LOGIN-R01](results/member-a.md#test-id-login-r01).

### Equivalence Partitioning

Required coverage:
- Age below the accepted range.
- Age within the accepted range.
- Age above the accepted range.

Results: [10](results/member-a.md#test-id-age-ep-10-a) was rejected, [30](results/member-a.md#test-id-age-ep-30-a) was accepted, [90](results/member-a.md#test-id-age-ep-90-a) was rejected. All 3 passed.

Note: the brief's baseline first name `Alex` was rejected by the server, so I used `Alexa` instead. See the [team plan](team-plan.md#agreed-baseline-data).

### Input-Format Observations

Required observations:
- Blank age.
- Non-numeric age input.

Results: for a [blank age](results/member-a.md#test-id-age-fmt-blank-a) the browser asked me to fill in the field. For [`abc`](results/member-a.md#test-id-age-fmt-abc-a) I could not type letters into the number box at all. I recorded both as observations.

### 2-Point Boundary Testing

Required values:
17, 18, 80, 81.

Results: all passed. [17](results/member-a.md#test-id-age-2p-17-a), [18](results/member-a.md#test-id-age-2p-18-a), [80](results/member-a.md#test-id-age-2p-80-a), [81](results/member-a.md#test-id-age-2p-81-a).

### 3-Point Boundary Testing

Required values:
16, 17, 18, 19, 79, 80, 81, 82.

Results: the new ones all passed. [16](results/member-a.md#test-id-age-3p-16-a), [19](results/member-a.md#test-id-age-3p-19-a), [79](results/member-a.md#test-id-age-3p-79-a), [82](results/member-a.md#test-id-age-3p-82-a). For 17, 18, 80 and 81 I reused my 2-point results, so I only count them once.

## Member Contributions

### Member A

- Guided results: [View results](results/member-a.md)
- Self-designed tests: [View tests](exploratory/member-a.md)
- Reflection: [View reflection](reflections/member-a.md)
- Chosen investigation: How long the first name and surname can be.
- Main observation: The minimum first name length is different in three places. The rule has none, the page's JavaScript needs 3 letters and the server needs 5. The surname limits match the rule (11 to 79).
- Pull request: https://github.com/FENGFANCHEN-012/manual-testing-team-fengfan/pull/1

## Team Conclusion

- The guided activities helped me see that whether a test is positive or negative depends on the input, and that Pass or Fail comes from comparing what I expected with what actually happened. I also learned that a few well-chosen values from each group and at each edge cover more than lots of random valid values.
- In my own testing I used boundary testing on text fields instead of numbers. I found that the browser, the JavaScript and the server do not always follow the same rules, or the published ones.
- Next I would ask what the first name minimum is supposed to be and whether surname is required, then test how spaces, accents and emoji are counted.
