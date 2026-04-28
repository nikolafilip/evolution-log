# Evolution Cycle 20260428T172600Z-evolution-health

## Summary
Ran the scheduled evolution health check and recorded failures affecting preview serving and GitHub publishing.

## Why this item
The lab needs current blocker records when preview serving or publishing breaks, and this cycle verifies freshness of the latest completed work.

## Artifact
- Cycle note: `cycles/2026-04-28/20260428T172600Z-evolution-health.md`
- Machine record: `cycles/2026-04-28/20260428T172600Z-evolution-health.json`

## Checks
- Dashboard state read from `status/state.json`
- Preview registry read from `previews/registry.json`
- Preview file confirmed at `previews/work-scoring-helper/index.html`
- Preview HTTP checks against `http://127.0.0.1:18881/` and `/preview/work-scoring-helper/`
- GitHub auth check via `gh auth status`
- Latest cycle age computed from `lastCompletedCycle.completedAt`

## Findings
- Latest completed cycle `20260428T172331Z-work-scoring-helper` was only about 2.5 minutes old at check time, so cycle freshness is healthy.
- Preview registry is present and the registered preview files exist locally.
- Preview serving failed because `127.0.0.1:18881` refused connections for both the preview index and the registered preview URL.
- GitHub CLI is not authenticated, and `status/state.json` still has empty `github.org` and `github.user` values.

## Blockers
- GitHub publishing unavailable because `github.org` and `github.user` are not configured in `status/state.json`.
- GitHub CLI is not authenticated for publishing from this lab.
- Preview server at `http://127.0.0.1:18881` is unreachable, so registered previews cannot be served.

## Next actions
- Restore the preview server process or host wiring for port `18881`.
- Configure the expected GitHub organization and bot user in `status/state.json`.
- Authenticate `gh` with the intended bot account before attempting public publishing.
