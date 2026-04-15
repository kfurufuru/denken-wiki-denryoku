Read `.claude/skills/calc-pattern-writer/SKILL.md` for full instructions. Then append a new calculation pattern to `docs/reference/calc-patterns.md`.

Target pattern: $ARGUMENTS  (e.g. `配電線路の電力損失計算`)

Steps:
1. Read the full `docs/reference/calc-patterns.md` to find the current max pattern number and avoid duplication
2. Read `docs/reference/numbers.md` and `docs/reference/glossary.md` for correct values and terminology
3. Read `data/atoms.csv` and extract any relevant formula rows for this pattern
4. Write the new pattern block following the exact structure of existing patterns (公式 → 記号表 → 手順 → 注意点 → 例題)
5. Verify the example calculation result before appending
6. Append to `docs/reference/calc-patterns.md`
7. Remind the user to link to this pattern from the relevant `docs/themes/*.md` page
