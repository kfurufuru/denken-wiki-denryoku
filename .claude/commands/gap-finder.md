Read `.claude/skills/gap-finder/SKILL.md` for full instructions. Then execute the gap-finder analysis as described:

1. Read `data/atoms.csv` (all rows)
2. Read `docs/kakomon/by-field.md` (all sections)
3. Read `data/pipeline.csv`
4. List all files in `docs/themes/`
5. Compare coverage: which fields have theme pages vs. not, which past exam entries are missing from atoms.csv
6. Calculate priority scores and output the report in the format specified in the SKILL.md

Arguments (optional): $ARGUMENTS
- `--field <分野>` to filter by field
- `--top <N>` to show only top N gaps
