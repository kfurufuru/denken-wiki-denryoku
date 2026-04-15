Read `.claude/skills/theme-writer/SKILL.md` for full instructions. Then generate a new theme page as described.

Target theme: $ARGUMENTS

Steps:
1. Read `docs/themes/suiryoku.md` as the golden template
2. Read `docs/kakomon/by-field.md` to find past exam entries for the target theme
3. Read `docs/reference/calc-patterns.md`, `docs/reference/numbers.md`, `docs/reference/glossary.md`
4. Read `data/atoms.csv` and filter rows for the target theme
5. Generate `docs/themes/<slug>.md` following the standard structure in SKILL.md
6. After generating, remind the user to run `/fact-check docs/themes/<slug>.md`
