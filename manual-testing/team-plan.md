# Team Plan

## Team Identifier

manual-testing-team-fengfan

## Members

I am doing this practical by myself, so I am the only member and I took on all the roles.

### Member A
- GitHub username: FENGFANCHEN-012
- Coordination responsibility: All of them (time keeping, requirements and baseline, test coverage, evidence, and merging the pull requests)

## Guided Test Allocation

Because I am working alone, I ran every guided test that the brief splits between Members A to E:

| Activity | Tests |
|---|---|
| Login | LOGIN-P01, LOGIN-N01, LOGIN-N02, LOGIN-N03, LOGIN-R01 |
| Equivalence partitioning | Age 10, 30, 90, plus blank age and `abc` |
| 2-point boundary | Age 17, 18, 80, 81 |
| 3-point boundary | Age 16, 19, 79, 82 (I reused my results for 17, 18, 80, 81) |

I kept the test ID format from the brief and ended all of them with `-A`, for example `AGE-2P-18-A`.

## Agreed Baseline Data

| Field | Baseline value |
|---|---|
| First name | `Alexa` (I changed this from `Alex`, see below) |
| Surname | `TestingStudent` |
| Age | `30` |
| Country | `Singapore` |
| Notes | `Manual testing classroom exercise` |

When I checked the baseline on 8 Nov 2026:

- With `Alex` as the first name, the server said "Firstname too short", so the baseline did not pass.
- With `Alexa`, the server said "Valid Input: Your Input passed validation".

Question for the Tutor: the rules only say the first name must be filled and be less than 90 chars, but the server rejected a 4-letter name. Is there a minimum length that is not written down, or is this a bug? For now I am using `Alexa` so the age tests are not affected by the first name.

## Open-Ended Testing Allocation

### Member A — Open-Ended Testing

- Chosen area: How long the First name and Surname can be on the Test Pages form.
- Question to investigate: Do the page checks and the server checks follow the published rules (first name filled and under 90 chars, surname 11 to 79 chars)? And why was `Alex` rejected?
- Record: [exploratory/member-a.md](exploratory/member-a.md)

## Repository Integration Arrangements

- I work on the branch `testing/member-a`.
- I commit and push at each checkpoint in the brief.
- I merge into `main` with a pull request, using a normal merge commit so all my commits stay in the history.
