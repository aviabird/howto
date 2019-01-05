## How to review a PR?

Please keep all these points in mind while reviewing a PR.

1. Check for function placement in correct modules/classes **(SRP)**
2. Check for repetition of code **(DRY)**
3. Check for variable/function naming **(Code readability)**
4. Functions should have consistent return types **(Code consistency)**
5. Documentation at places where we have assumed something **(Code maintainability)**
6. Documentation for logic where complex logic is there. **(Code maintainability)**
7. Give preference to readable code(more LOC) than complex(less LOC) **(Code readability)**

### Special instructions
Respect code boundaries and domain structure (DDD).
Make sure to discuss the code design. This can also be done on a whiteboard before starting the PR review.

Check this [PR](https://github.com/aviacommerce/avia/pull/364/) for example PR review.
