# OpenClaw Evolution Lab Heartbeat

Heartbeat is only for light health and continuity checks. Real work happens in
evolution cycles.

During heartbeat, check:

- Dashboard state.
- Latest cycle age.
- Preview registry.
- GitHub authentication.
- Open blockers.

If the lab is healthy enough for the next evolution cycle, return:

```text
HEARTBEAT_OK
```

If it is not healthy, record the smallest useful blocker and leave the workspace
ready for the next cycle to continue.
