# Team Plan

## Team Identifier

manual-testing-team-fengfan

## Members

This is a solo submission. One member performs every coordination responsibility and every guided test.

### Member A
- GitHub username: FENGFANCHEN-012
- Coordination responsibility: All (team coordination, requirements and baseline, guided test coverage, evidence organisation, repository integration)

## Guided Test Allocation

All guided tests that the brief allocates to Members A–E are executed by member-a:

| Activity | Tests |
|---|---|
| Login | LOGIN-P01, LOGIN-N01, LOGIN-N02, LOGIN-N03, LOGIN-R01 |
| Equivalence partitioning | Age 10, 30, 90; blank age and `abc` observations |
| 2-point boundary | Age 17, 18, 80, 81 |
| 3-point boundary | Age 16, 19, 79, 82 (17, 18, 80, 81 reused from 2-point) |

Test IDs keep the brief's format with the `-A` suffix, e.g. `AGE-2P-18-A`.

## Agreed Baseline Data

To be confirmed on the live form before testing.

## Open-Ended Testing Allocation

To be decided after the guided activities.

## Repository Integration Arrangements

- Work on branch `testing/member-a`.
- Commit and push at every checkpoint in the brief.
- Merge into `main` through a pull request using a merge commit (keeps individual commits).
