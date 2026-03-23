# OpenClaw Workflow Engine

English | [中文说明](README.zh-CN.md)

OpenClaw Workflow Engine is a focused repository for a governed workflow runtime.
It is designed to execute YAML-defined DAG workflows, route tasks through a constitution-style runtime, and provide a clean foundation for future workflow orchestration work.

![Architecture](docs/architecture-overview.md)

## What this project is for

This repository is intended for:

- building and evolving a workflow engine
- running YAML / DAG-based workflows
- experimenting with governed dispatch and policy-aware routing
- validating runtime behavior through minimal engine-focused tests
- serving as a reusable base for future orchestration systems

This repository is **not** intended to be a full personal workspace snapshot, memory system, or host-specific assistant environment.

## Core capabilities

- **YAML workflow loading**: load declarative workflow definitions from `workflows/*.yaml`
- **DAG execution**: execute multi-node workflows with dependency edges
- **Governed runtime**: route requests through a constitution-style runtime
- **Skill/tool contracts**: define tools, capabilities, and policy constraints
- **Workflow state tracking**: maintain workflow context, registry, and WAL traces
- **Minimal verification suite**: validate engine behavior through focused tests

## Repository structure

```text
.
├─ core/
│  ├─ agent/       # agent-facing runtime entry layer
│  ├─ engine/      # DAG engine, runner, YAML loader, registry, WAL
│  ├─ infra/       # skill contracts, manager, legacy bridge, support infra
│  └─ runtime/     # constitution runtime, dispatch, router, progress logic
├─ tests/          # engine-focused tests
├─ workflows/      # sample and smoke workflow YAML files
├─ scripts/        # validation scripts
├─ docs/           # rebuild plan, migration notes, architecture docs
├─ README.md
├─ README.zh-CN.md
└─ requirements.txt
```

## Architecture overview

See: [docs/architecture-overview.md](docs/architecture-overview.md)

High-level flow:

1. a workflow YAML is loaded by `core/engine/yaml_workflow.py`
2. the runner builds a DAG execution plan
3. nodes are dispatched through the constitution/governed runtime
4. results are written into workflow context / registry / WAL
5. tests verify the minimal runtime contract

## Quickstart

Install dependencies:

```bash
python3 -m pip install -r requirements.txt
```

Run boundary check:

```bash
python3 scripts/check_constitution_boundaries.py
```

Run core tests:

```bash
python3 -m pytest -q \
  tests/test_skill_manager_smoke.py \
  tests/test_base_agent_constitution.py \
  tests/test_constitution_runtime.py
```

## Current status

This repository has been rebuilt into an engine-only skeleton.
The current focus is to make `workflow run` form a fully standalone execution closure, so that sample workflows can run without depending on an external workspace environment.

## Near-term roadmap

- make workflow smoke path independently runnable
- remove remaining host/workspace residue
- tighten engine/runtime boundaries further
- add a real workflow smoke CI job
- document extension points for future skills/tools

## Notes

If you are evaluating this repository as an engine codebase, focus first on:

- `core/engine/`
- `core/runtime/`
- `core/infra/skill_contracts.py`
- `core/infra/skill_manager.py`
- `tests/`
- `workflows/`
