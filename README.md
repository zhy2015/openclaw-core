# OpenClaw Workflow

A slimmed repository for a local workflow runtime built around:

- a governed dispatch layer
- a DAG/YAML workflow engine
- skill routing / legacy adapter bridging
- constitution-style boundary checks

This repo is intended to be AI-readable first: another agent should be able to clone it, understand the core layout, and run a minimal verification path without needing the original full workspace.

## What this repo is

This repository primarily exposes the workflow/runtime side of the larger OpenClaw workspace:

- `core/` — runtime, engine, dispatch, registry, tests
- `scripts/` — validation and operational scripts
- `workflows/` — YAML workflow definitions and registry data
- `skills/` — skill metadata / adapters / selected skills used by the runtime
- `docs/` — architecture and migration notes

## What this repo is not

This is **not** a perfectly isolated product package yet.
Some historical/project-specific material may still exist in `memory/`, `projects/`, and parts of `skills/`.
If you are another AI agent, treat those as secondary context unless the task explicitly requires them.

## Start here

If you are an AI agent entering this repo, use this reading order:

1. `README.md`
2. `docs/system/fast-slow-path-constitution.md`
3. `core/engine/cli.py`
4. `core/engine/runner.py`
5. `core/engine/yaml_workflow.py`
6. `scripts/testing/check_constitution_boundaries.py`

## Minimal environment

Recommended:

- Python 3.11+
- `pip install pytest pyyaml`

For basic repo verification, you do **not** need the original full workstation state.

## Minimal verification

### 1) Boundary check

```bash
python3 scripts/testing/check_constitution_boundaries.py
```

### 2) Core tests

```bash
python3 -m pytest -q \
  core/tests/test_skill_manager_smoke.py \
  core/tests/test_base_agent_constitution.py \
  core/tests/test_constitution_runtime.py
```

### 3) Optional smoke workflow parse/run path

List skills through the legacy bridge:

```bash
python3 core/engine/cli.py skill list
```

Run a sample YAML workflow:

```bash
python3 core/engine/cli.py workflow run workflows/test_chaining.yaml
```

## Core entrypoints

### CLI

- `core/engine/cli.py`

Supports:

- `skill list`
- `workflow run <yaml>`

### Runtime loader

- `core/engine/yaml_workflow.py`

Loads declarative YAML workflows into DAG pipeline objects.

### Runner

- `core/engine/runner.py`

Executes YAML workflows using the governed dispatcher and writes WAL/registry state.

## Safety notes for external AI agents

When editing this repo:

- prefer `core/`, `scripts/`, `docs/system/`, and selected workflow files
- avoid treating `memory/` as the product source of truth unless the task is explicitly memory-related
- avoid assuming everything under `projects/` is part of the public runtime contract
- check CI assumptions before hardcoding local absolute paths

## Current limitations

Known rough edges:

- some paths still reflect workspace-era structure
- repository boundaries are cleaner than before, but not fully minimal
- some tests and workflows may still assume local runtime context

## Suggested next cleanup

If you want this repo to become fully AI-onboardable/public-ready, next steps are:

1. remove or archive non-core `projects/`
2. trim `memory/` to docs-only or remove from public branch
3. remove workflow logs from tracked files
4. define a canonical install path with a single bootstrap command
5. add one deterministic smoke workflow for CI
