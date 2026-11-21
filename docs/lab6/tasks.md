# Lab 6 – Answers

## Task A1 – Coverage
Fifth test added: `test_cannot_drop_a_course_that_is_not_registered` (covers line 26).
Coverage report: 100% (see `coverage.txt`; add your own screenshot as `coverage.png`).

**Does 100% coverage prove the code is correct?**
No – it only shows that every line was executed by some test, not that the tests check the right behaviour or cover all inputs and combinations.

## Task B1 – Drop scenario
Added `Scenario: Drop a registered course` to `features/registration.feature` and a new
`@when('the student drops "{code}"')` step. `python -m behave` → 7 scenarios, 28 steps, all passed (see `behave_output.txt`).

## Task C1 – Smells in `legacy_invoice.py`

| Smell | Where | Principle it breaks |
|---|---|---|
| Long if/elif chain on `kind` | loop body + after the loop | OCP: a new student type means editing this function |
| Magic numbers (1200, 0.5, 2000, 5000) | fee calculations | Readability / no single place to change a rate |
| One function calculates, formats, writes a file and prints | whole `make_invoice` | SRP: several reasons to change |
| File opened without `with` (manual `close()`) | file writing | Resource safety (file stays open if `write` fails) |
| Disk access hard-wired inside the function | `open(...)` | DIP: depends on the concrete disk, cannot be tested with a fake |
| Fee worked out per course, though only total hours matter | the `for` loop | Needless complexity; the rule is a function of total hours |
| `kind` checked twice (loop and after loop) | `if kind == "international"` | Duplicated logic, rules for one type are scattered |

## Task C2 – SiblingPolicy
`SiblingPolicy` (25% off the regular fee) was added test-first: first the failing test
`("sibling", 5400)`, then the class + one `POLICIES` entry. `make_invoice` was **not** changed.

| Measure | Before | After |
|---|---|---|
| Cyclomatic complexity of `make_invoice` (Ruff C901) | 6 | 1 |
| Tests passing (`python -m pytest -q`) | 8 (5 registration + 3 characterization) | 11 |
| Add "sibling discount" | Edit two if/elif chains | One class + one dict entry |
| Test without writing files | Not possible | Yes, with `FakeWriter` |
