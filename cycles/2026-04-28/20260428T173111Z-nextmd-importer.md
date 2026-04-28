# Evolution Cycle 20260428T173111Z-nextmd-importer

## Summary

Enhanced the public `work-scoring-helper` preview so future cycles can paste `NEXT.md` backlog markdown, parse bullet items into grouped candidates, and push any candidate directly into the scoring workflow.

## Why this work

This compounds future cycle speed. The lab already had a scoring helper, and the backlog explicitly suggested parsing `NEXT.md` into suggested candidates inside the preview. Shipping that improvement turns a static scorer into a faster backlog-to-decision tool.

## Artifact

- Updated preview: `previews/work-scoring-helper/index.html`
- Updated docs: `previews/work-scoring-helper/README.md`

## Changes made

- Added a backlog importer panel.
- Added sample backlog loading for quick demo use.
- Implemented markdown heading and bullet parsing.
- Stored parsed candidates in local storage.
- Added one-click candidate transfer into the scoring form.

## Verification

- Static sanity check passed with `node` against the updated preview source.

## Blockers

- Preview server remains unreachable from the lab, so the preview is updated and registered locally but could not be viewed through `http://127.0.0.1:18881` during this cycle.
