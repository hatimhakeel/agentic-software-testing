---
name: excel-diff-highlighter
description: highlight updated differences between two excel workbooks when the user provides an old/baseline/source .xlsx file and a new/updated/output .xlsx file. use for requests to compare, diff, validate, audit, mark, or highlight workbook changes. the new workbook must contain exactly one worksheet; match that worksheet to the best exact, partial, normalized, or fuzzy sheet-name match in the old workbook. produce a copy of the new workbook with only changed or added cells highlighted fff2cc. deleted cells and deleted rows must not be inserted, restored, represented, copied, or highlighted in the output.
---

# Excel Diff Highlighter

Use this skill to compare an old Excel workbook against a new single-sheet Excel workbook and return a highlighted copy of the new workbook. Highlight only cells that exist in the new workbook and are changed or added. Do not insert or represent deleted content from the old workbook.

## Required inputs

- An old/baseline/source `.xlsx` workbook.
- A new/updated/output `.xlsx` workbook that contains exactly one worksheet.

Do not modify the old workbook. Always write a separate output workbook based on the new workbook.

## Workflow

1. Identify the old and new workbook paths supplied by the user.
2. Run `scripts/highlight_excel_diff.py` with:
   - `--old <old_workbook_path>`
   - `--new <new_workbook_path>`
   - `--output <highlighted_output_path>`
3. Return the generated workbook and a concise summary from the script output.

Example command:

```bash
python scripts/highlight_excel_diff.py --old /mnt/data/old.xlsx --new /mnt/data/new.xlsx --output /mnt/data/new_highlighted.xlsx
```

## Sheet matching rules

The new workbook must contain exactly one worksheet. Match that worksheet to the best old workbook worksheet using this priority:

1. Exact sheet-name match.
2. Case-insensitive exact match.
3. Normalized exact match, ignoring leading/trailing spaces and repeated internal spaces.
4. Partial match where either normalized sheet name contains the other.
5. Fuzzy similarity match as a fallback.

Normalize sheet names only for matching by lowercasing, trimming spaces, collapsing repeated spaces, and ignoring obvious separators and punctuation such as `_`, `-`, `.`, `,`, `;`, and `:`.

Fail clearly when:

- The new workbook has zero sheets or more than one sheet.
- No confident old-sheet match exists.
- More than one old sheet ties as the strongest match.

## Highlight color

- Apply only solid fill `#FFF2CC` to changed or added cells.
- Do not use any deleted-item color.
- Do not use `#DF8D77`.

## Comparison behavior

Compare formulas as formulas. Compare normal scalar values including dates, numbers, strings, booleans, blanks, and formulas.

Highlight cells with `#FFF2CC` when the cell exists in the new worksheet and:

- The old and new values differ and the new cell is not blank.
- The old and new formulas differ and the new cell is not blank.
- The old cell was blank or missing and the new cell contains content.
- The entire row exists only in the new worksheet; highlight each non-blank, non-numbering cell in that added row.

Ignore deleted content in the output:

- Do not insert deleted rows.
- Do not insert deleted cells.
- Do not copy old content that is missing from the new workbook.
- Do not restore old workbook content.
- Do not highlight blank new cells simply because the old workbook had content there.
- Do not include deleted rows or cells in the output workbook unless they already exist in the new workbook as normal new-workbook content.

## Numbering and row alignment rules

Ignore numbering of any type when aligning rows. Treat sequence numbers, serial numbers, row numbers, item numbers, index values, one-letter enumerations, Roman numerals, and similar numbering-style cells as non-semantic for alignment.

Do not treat numbering-only differences caused by deleted or missing rows as meaningful changes when the underlying non-numbering row content aligns. Numbering in the new workbook should remain exactly as provided; do not renumber rows or cells.

## Output summary

Report:

- New workbook worksheet name.
- Matched old workbook worksheet name.
- Sheet matching method and score.
- Count of changed/added cells highlighted `#FFF2CC`.
- Confirmation that deleted cells and deleted rows were not included, inserted, restored, or highlighted.
- Output filename.
- Any error or ambiguity that prevented completion.

## Implementation notes

The bundled script uses `openpyxl` and preserves workbook content, formulas, worksheet names, and existing formatting as much as possible. The only intentional formatting change is the yellow fill used to mark changed or added cells in the output copy of the new workbook.