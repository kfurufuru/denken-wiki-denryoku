Read `.claude/skills/kakomon-ingest/SKILL.md` for full instructions. Then add the specified past exam entry to `data/atoms.csv`.

Target: $ARGUMENTS  (format: `<年度> <問番号>`, e.g. `R07下 問1`)

Steps:
1. Read `data/atoms.csv` to get the current max id
2. Read `docs/kakomon/by-field.md` to find the target row (year × question number)
3. Determine field, subfield, title, problem type from by-field.md
4. Check for duplicates (same year × q_no already in atoms.csv)
5. Show the proposed row to the user and ask for confirmation
6. On confirmation, append the row to `data/atoms.csv`
7. Update `data/pipeline.csv` atoms_used if a related draft exists
