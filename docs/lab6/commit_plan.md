# Commit plan (one commit per TDD cycle) – run inside the lab6 folder

```powershell
git switch -c lab6-tdd
```
Write each test FIRST, run `python -m pytest -q` and see it FAIL (Red), then write the code (Green), tidy (Refactor).

| # | Do | Commit message |
|---|---|---|
| 0 | add `pyproject.toml`, `.gitignore` | `chore: lab6 setup` |
| 1 | Red: add `test_register_adds_hours` (+ empty `Student` / `RegistrationError`) → fails. Green: `register` adds hours | `test: rule 1 register adds hours` |
| 2 | add 18-hour test → fails → add the limit check | `test: rule 2 18-hour limit` |
| 3 | add duplicate test → fails → add duplicate check | `test: rule 3 no duplicate course` |
| 4 | add drop test → fails → add `drop` | `test: rule 4 drop course` |
| 5 | Task A1: add not-registered test (coverage 100%) | `test: cover drop of unknown course` |
| 6 | `features/` (feature, environment, steps) | `feat: BDD registration feature` |
| 7 | drop scenario + `@when` drop step | `feat: BDD drop scenario` |
| 8 | copy `legacy_invoice.py` → `invoice.py` + characterization tests (3 pass) | `test: characterize make_invoice` |
| 9–11 | refactor steps 2, 3+4, 5 (one commit each, tests green) | `refactor: name constants` etc. |
| 12 | add `("sibling", 5400)` test → fails → add `SiblingPolicy` | `feat: SiblingPolicy` |
| 13 | `docs/lab6/*` | `docs: lab6 answers` |

Then: `git log --oneline` → take a screenshot for the submission.
