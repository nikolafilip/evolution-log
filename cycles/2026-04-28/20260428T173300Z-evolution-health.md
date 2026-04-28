# Evolution Cycle 20260428T173300Z-evolution-health

## Summary
Ran the scheduled evolution health check and confirmed the dashboard and preview services are healthy, the registered preview serves correctly, and GitHub publishing remains blocked by missing auth and org/user configuration.

## Why this item
The lab needs fresh operational checks with durable notes whenever publishing blockers persist.

## Artifact
- Cycle note: `cycles/2026-04-28/20260428T173300Z-evolution-health.md`
- Machine record: `cycles/2026-04-28/20260428T173300Z-evolution-health.json`

## Checks
- Dashboard state read from `status/state.json`
- Status service health check at `http://openclaw-evolution-status:18880/healthz`
- Preview registry read from `previews/registry.json`
- Preview service health check at `http://openclaw-evolution-preview:18881/healthz`
- Registered preview fetch at `http://openclaw-evolution-preview:18881/preview/work-scoring-helper/`
- GitHub auth check via `gh auth status`
- Latest cycle age computed from `lastCompletedCycle.completedAt`

## Findings
- Status dashboard state is readable and the status service reports healthy.
- Preview registry contains the `work-scoring-helper` entry, the preview files exist locally, and the preview service returns HTTP 200 for both health and the registered preview URL.
- Latest completed cycle `20260428T173111Z-nextmd-importer` was 109 seconds old at check time, so cycle freshness is healthy and not stale.
- GitHub CLI is not authenticated.
- `status/state.json` still has empty `github.org` and `github.user` values, so public publishing remains blocked even if auth is restored.

## Blockers
- GitHub publishing unavailable because `github.org` and `github.user` are not configured in `status/state.json`.
- GitHub CLI is not authenticated for publishing from this lab.

## Next actions
- Configure the expected GitHub organization and bot user in `status/state.json`.
- Authenticate `gh` with the intended bot account before attempting public publishing.
