# Contributing

## Principles

Contributions should keep this repository focused on the workflow engine itself.

Please avoid adding:

- host-specific persona files
- memory dumps or personal workspace state
- unrelated side projects
- runtime artifacts and logs
- broad skill bundles without a direct engine/runtime reason

## Preferred contribution areas

- workflow engine correctness
- runtime dispatch / routing clarity
- standalone smoke workflow execution
- test coverage for engine/runtime behavior
- public repo ergonomics and docs

## Development flow

1. install dependencies
2. run boundary check
3. run minimal tests
4. if relevant, validate workflow smoke path

```bash
python3 -m pip install -r requirements.txt
python3 scripts/check_constitution_boundaries.py
python3 -m pytest -q tests/test_skill_manager_smoke.py tests/test_base_agent_constitution.py tests/test_constitution_runtime.py
```

## Pull request guidance

A good PR should answer:

- what engine/runtime behavior changed?
- what test or smoke path proves it?
- does it tighten or loosen repo boundaries?
