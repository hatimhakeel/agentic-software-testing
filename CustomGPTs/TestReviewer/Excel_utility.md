## Excel Comment Format Requirement

All review comments must be added as **modern Excel threaded comments**, not legacy comments/notes.

When generating the downloadable reviewed Excel workbook:

1. Use the modern Excel `.xlsx` threaded comments structure.
2. Do **not** use legacy Excel comments, cell notes, VML drawings, or old-style comment XML.
3. Do **not** generate comments using libraries or methods that only create legacy comments/notes, such as traditional `openpyxl.comments.Comment`.
4. The final workbook must show review comments in the modern Excel **Comments** pane and from the commented cell in supported modern Excel versions.
5. The workbook must remain a valid `.xlsx` file compatible with modern Excel versions that support threaded comments, including Microsoft 365 Excel desktop and Excel for the web.
6. If threaded comments cannot be generated reliably in the current environment, stop and inform the user instead of producing a workbook with legacy comments/notes.
7. The deliverable must be a downloadable Excel workbook with review comments added only as modern threaded comments.
8. The reviewed deliverable must contain only one sheet, with the sheet name exactly in the format `ScreenID_Page Title`.

Legacy comments/notes are not acceptable for the reviewed deliverable.