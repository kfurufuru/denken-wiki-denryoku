Read `.claude/skills/formula-ingest/SKILL.md` for full instructions. Then add the specified formula or constant to `data/atoms.csv`.

Target: $ARGUMENTS  (formula name, e.g. `比速度の定義式`)

Steps:
1. Read `data/atoms.csv` to get the current max id and check for duplicates
2. Read `docs/reference/calc-patterns.md` — if the formula already exists there, report it instead of adding
3. Read `docs/reference/numbers.md` and `docs/reference/glossary.md` to verify values
4. Determine: field, subfield, formula expression, unit, source
5. Show the proposed row to the user and ask for confirmation
6. On confirmation, append to `data/atoms.csv` with type=formula (or type=number if a constant)
