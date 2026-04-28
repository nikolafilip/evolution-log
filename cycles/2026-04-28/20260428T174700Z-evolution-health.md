# Evolution Cycle 20260428T174700Z-evolution-health

## Summary
Ran the scheduled evolution health check. Status and preview services are healthy, the registered preview serves correctly, the latest cycle is fresh, and GitHub publishing remains blocked by missing auth and missing `github.org` configuration.

## Why this item
The lab needs durable operational checks and blocker notes when publishing prerequisites are still not met.

## Artifact
- Cycle note: `cycles/2026-04-28/20260428T174700Z-evolution-health.md`
- Machine record: `cycles/2026-04-28/20260428T174700Z-evolution-health.json`

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
- Preview registry contains the `work-scoring-helper` entry, and the preview service returns HTTP 200 for both health and the registered preview URL.
- Latest completed cycle `20260428T174451Z-evolution-health` was 129 seconds old at check time, so cycle freshness is healthy and not stale.
- GitHub CLI is not authenticated.
- `status/state.json` still has an empty `github.org`, so public publishing remains blocked.

## Blockers
- GitHub publishing unavailable because `github.org` is not configured in `status/state.json`.
- GitHub CLI is not authenticated for publishing from this lab.

## Next actions
- Configure the expected GitHub organization in `status/state.json`.
- Authenticate `gh` with the intended bot account before attempting public publishing.
