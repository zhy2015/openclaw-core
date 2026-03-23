# OpenClaw Workflow Engine

[English](README.md) | 中文说明

OpenClaw Workflow Engine 是一个聚焦于**工作流运行时 / 编排引擎**的仓库。
它的目标是承载 YAML 定义的 DAG 工作流执行、基于 constitution 的治理式路由，以及后续复杂工作流系统的演进基础。

架构图见：`docs/architecture-overview.md`

## 这个项目是干什么的

这个仓库主要用于：

- 构建和演进工作流引擎
- 运行 YAML / DAG 风格工作流
- 试验 governed dispatch / policy-aware routing
- 用最小测试集验证 runtime 行为
- 作为后续复杂编排系统的可复用基础

这个仓库**不是**：

- 个人工作区快照
- 记忆系统主仓
- 宿主助手配置仓
- 杂糅各种 side project 的大工作区

## 核心能力

- **YAML 工作流加载**：从 `workflows/*.yaml` 读取声明式工作流
- **DAG 执行**：支持多节点、依赖边执行
- **治理式运行时**：通过 constitution runtime 做路由与约束
- **技能/工具契约**：定义 tool schema、capability 和策略限制
- **工作流状态跟踪**：维护 workflow context、registry、WAL
- **最小验证集**：通过聚焦测试验证引擎行为

## 仓库结构

```text
.
├─ core/
│  ├─ agent/       # 面向 agent 的调用入口层
│  ├─ engine/      # DAG engine、runner、YAML loader、registry、WAL
│  ├─ infra/       # skill contract、manager、legacy bridge、支撑基础设施
│  └─ runtime/     # constitution runtime、dispatch、router、progress 逻辑
├─ tests/          # 引擎聚焦测试
├─ workflows/      # 示例与 smoke workflow
├─ scripts/        # 校验脚本
├─ docs/           # 重建说明、迁移清单、架构文档
├─ README.md
├─ README.zh-CN.md
└─ requirements.txt
```

## 架构概览

见：`docs/architecture-overview.md`

高层流程：

1. `core/engine/yaml_workflow.py` 读取 workflow YAML
2. runner 构建 DAG 执行计划
3. 各节点通过 constitution / governed runtime 分发执行
4. 执行结果写入 workflow context / registry / WAL
5. 由最小测试集验证运行时契约

## 快速开始

安装依赖：

```bash
python3 -m pip install -r requirements.txt
```

运行边界检查：

```bash
python3 scripts/check_constitution_boundaries.py
```

运行核心测试：

```bash
python3 -m pytest -q \
  tests/test_skill_manager_smoke.py \
  tests/test_base_agent_constitution.py \
  tests/test_constitution_runtime.py
```

## 当前状态

这个仓库已经被重建成 **engine-only skeleton**。
当前最重要的下一步，是让 `workflow run` 真正形成**独立可运行闭环**，也就是样例 workflow 不依赖外部工作区就能跑通。

## 近期路线

- 跑通真正独立的 workflow smoke path
- 继续剔除残留的 host/workspace 痕迹
- 进一步收紧 engine/runtime 边界
- 给 CI 增加真实 workflow smoke run
- 文档化未来 skill/tool 扩展点

## 建议优先阅读

如果你是来评估这个仓库是否像一个真正的引擎仓，优先看：

- `core/engine/`
- `core/runtime/`
- `core/infra/skill_contracts.py`
- `core/infra/skill_manager.py`
- `tests/`
- `workflows/`
