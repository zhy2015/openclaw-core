# Smoke Workflow

## Goal

A smoke workflow should prove that a fresh clone can do more than import modules — it should execute a minimal workflow path successfully.

## Current state

Current sample workflow files:

- `workflows/ai_smoke.yaml`
- `workflows/test_chaining.yaml`
- `workflows/test_chaos_core.yaml`

At the moment, the repository still needs more work before `workflow run` forms a fully standalone public smoke path.

## Expected target usage

```bash
python3 core/engine/cli.py workflow run workflows/ai_smoke.yaml
```

## Desired result shape

A successful smoke run should return JSON containing at least:

- `workflow_id`
- `results`
- `context`
- `wal_path`
- `registry_path`

## Why this matters

Unit tests can be green while the public runtime remains unusable.
A smoke workflow is the real proof that the repository works as an engine product.
