# Extension Points

## 1. Add a new tool/skill contract

Primary files:

- `core/infra/skill_contracts.py`
- `core/infra/skill_manager.py`

Use this path when introducing new tool schemas, capability profiles, or dispatch constraints.

## 2. Add a new workflow execution feature

Primary files:

- `core/engine/dag_engine.py`
- `core/engine/runner.py`
- `core/engine/yaml_workflow.py`

Use this path for new node semantics, edge semantics, workflow loading rules, or execution behavior.

## 3. Adjust runtime routing/policy

Primary files:

- `core/runtime/constitution.py`
- `core/runtime/dispatch.py`
- `core/runtime/policies.py`
- `core/runtime/router.py`

Use this path when changing fast/slow routing, policy boundaries, or governed dispatch behavior.

## 4. Add validation/verification

Primary files:

- `tests/`
- `scripts/check_constitution_boundaries.py`
- `.github/workflows/ci.yml`

Use this path for tests, smoke validation, and CI improvements.
