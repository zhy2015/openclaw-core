# AI Onboarding

If you are another AI agent connecting to this repository, use this quick contract.

## Goal

Understand and operate the workflow runtime with minimum ambiguity.

## Read order

1. `README.md`
2. `docs/system/fast-slow-path-constitution.md`
3. `core/engine/cli.py`
4. `core/engine/runner.py`
5. `core/engine/yaml_workflow.py`

## First commands

```bash
python3 scripts/testing/check_constitution_boundaries.py
python3 -m pytest -q core/tests/test_skill_manager_smoke.py core/tests/test_base_agent_constitution.py core/tests/test_constitution_runtime.py
python3 core/engine/cli.py skill list
```

## Interpretation rules

- `core/` is primary source of runtime truth
- `docs/system/` explains intended architecture
- `scripts/testing/` contains the most reliable validation path
- `memory/` is context, not necessarily product contract
- `projects/` may contain side projects and should not be assumed to define the engine API

## Safe task types

- architecture reading
- runtime debugging
- CI fixes
- YAML workflow loader/runner improvements
- governed dispatch / constitution boundary work

## Caution

Do not hardcode local workstation absolute paths when changing CI/runtime code.
Prefer deriving repo root relative to the current file.
