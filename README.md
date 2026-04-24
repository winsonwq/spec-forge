# SPEC-FORGE

把模糊想法锻造成结构化、可测试、可执行的规格文档，并支持持续迭代改进。

## 核心定位

- 当你需要编写或改进 SPEC（需求规格/技术规格/开发任务文档）时触发
- 适用于个人开发者或团队
- 支持从模糊需求生成结构化规格文档
- 内置自我演进机制：通过 quality-checker 循环检查 + 用户反馈迭代改进

## Subagents（6个）

| Agent | 职责 | 触发条件 |
|-------|------|----------|
| `requirement-drafter` | 把模糊想法写成结构化 SPEC | 每次都需要 |
| `logic-verifier` | 用代码验证算法/业务逻辑 | 涉及算法/复杂逻辑时 |
| `ui-verifier` | 用组件树验证 UI/交互 | 涉及复杂 UI 时 |
| `flow-verifier` | 用流程图验证业务流程 | 涉及业务流程时 |
| `quality-checker` | 检查完整性/可测试性/逻辑一致性 | 每次都需要 |
| `task-breaker` | 把 spec 拆成 2-3 级任务 | 需要任务拆解时 |

## 目录结构

```
spec-forge/
├── SKILL.md                      # 顶层编排器
├── README.md                     # 本文件
├── agents/
│   ├── requirement-drafter.md    # 需求起草
│   ├── logic-verifier.md         # 算法验证
│   ├── ui-verifier.md            # UI 验证
│   ├── flow-verifier.md          # 流程验证
│   ├── quality-checker.md        # 质量检查
│   └── task-breaker.md           # 任务拆解
└── references/
    └── spec-template.md          # SPEC 标准模板
```

## 产出格式

文件名：`{简短说明}-v{版本}-spec.md`

示例：`user-authentication-v1.0.0-spec.md`

## 版本规范

语义化版本 X.Y.Z：
- 主版本（X）：大幅重构、新增章节
- 次版本（Y）：新增内容、修改描述
- 补丁（Z）：修复错别字、格式调整

## 使用方式

1. 触发 skill：告诉它你需要写一个 spec
2. Intake interview：回答关于需求的问题
3. 等待 draft 完成
4. Quality checker 检查并提出问题
5. 根据需要触发 logic/ui/flow verifier
6. 循环直到 quality check 通过
7. Task breaker 进行任务拆解
8. 获得最终 spec

## 设计参考

本 skill 参考了 Anthropic Skill Creator 的设计模式：
- SKILL.md 作为顶层编排器
- Subagents 作为独立技能单元
- Reactive loop 实现自我演进
- 语义化版本管理
