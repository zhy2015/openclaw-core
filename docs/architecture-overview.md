# Architecture Overview

```mermaid
flowchart TD
    A[Workflow YAML\nworkflows/*.yaml] --> B[YAMLWorkflowLoader\ncore/engine/yaml_workflow.py]
    B --> C[WorkflowRunner\ncore/engine/runner.py]
    C --> D[DAGEngine\ncore/engine/dag_engine.py]

    D --> E[ConstitutionRuntime\ncore/runtime/constitution.py]
    E --> F[Dispatch Layer\ncore/runtime/dispatch.py]
    F --> G[Skill Manager\ncore/infra/skill_manager.py]
    G --> H[Tool / Skill Contracts\ncore/infra/skill_contracts.py]
    G --> I[Legacy Registry Adapter\ncore/infra/legacy_registry_adapter.py]

    D --> J[Workflow Context\ncore/engine/workflow_context.py]
    D --> K[Workflow Registry\ncore/engine/workflow_registry.py]
    D --> L[WAL Engine\ncore/engine/wal_engine.py]

    M[Tests\ntests/*] --> E
    M --> C
    M --> G
```

## Layer summary

### 1. Workflow definition layer
- input: YAML workflow files
- responsibility: declare nodes, edges, inputs, outputs, and execution relationships

### 2. Engine layer
- components: loader, runner, DAG engine, registry, context, WAL
- responsibility: parse workflow, execute nodes in dependency order, store run state

### 3. Runtime/governance layer
- components: constitution runtime, dispatch, routing policies
- responsibility: decide how requests are routed and constrained

### 4. Skill/contract layer
- components: skill manager, tool schemas, capability profiles, legacy adapter
- responsibility: normalize tool invocation and enforce execution policy

### 5. Verification layer
- components: tests, boundary checks, CI
- responsibility: validate that the runtime remains consistent and minimally runnable

## Intended evolution

The target architecture is:

- engine code remains independent of host workspace persona/memory files
- workflow execution forms a standalone closure
- CI verifies not only unit tests but also one real smoke workflow
- skill integration becomes cleaner and less dependent on legacy workspace state
