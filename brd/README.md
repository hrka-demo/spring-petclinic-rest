# brd/

One folder per client BRD, owned by agent A1 (`.claude/agents/a1-requirements.md`).

- `source/`: the BRD exactly as received, plus the Docling Markdown extract
- `brd.md`: cleaned BRD with inline requirement IDs
- `index.json`: requirement index (IDs are permanent)
- `open-questions.md`: ambiguities and conflicts for the PO

A BRD is usable by A2 only when `index.json` has `"status": "signed-off"` (PO gate).
