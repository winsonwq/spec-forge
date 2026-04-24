# SPEC-FORGE

把模糊想法锻造成结构化、可测试、可执行的规格文档，并支持持续迭代改进。

## 核心定位

- 当你需要编写或改进 SPEC（需求规格/技术方案文档）时触发
- 适用于个人开发者或团队
- 支持从模糊需求生成结构化规格文档
- 内置自我演进机制：通过循环检查 + 批判性思考持续改进

## 核心循环机制

每轮迭代：
1. 产出新内容
2. 版本号 +1（补丁版本）
3. quality-checker 评估
4. 决定下一步（继续循环或结束）

**版本更新时机**：
- 每轮循环结束：Z+1（补丁版本）
- 重大改进：Y+1（次版本）
- 里程碑完成：X+1（主版本）

## Subagents（6个）

| Agent | 职责 | 触发条件 |
|-------|------|----------|
| `requirement-drafter` | 把模糊想法写成结构化 SPEC | 每次都需要 |
| `logic-verifier` | 用代码验证算法/业务逻辑 | 涉及算法/复杂逻辑时 |
| `ui-verifier` | 用组件树验证 UI/交互 | 涉及复杂 UI 时 |
| `flow-verifier` | 用流程图验证业务流程 | 涉及业务流程时 |
| `quality-checker` | 检查质量 + 批判性挖掘潜在问题 | 每次都需要 |
| `task-breaker` | 拆成 2-3 级任务（Markdown checkbox） | 需要任务拆解时 |

## Subagent 调用约定

调用 subagent 时传递上下文：

```json
{
  "agent": "logic-verifier",
  "spec_content": "当前 SPEC 完整内容",
  "focus_area": "需要该 agent 处理的具体部分",
  "output_path": "产出保存路径",
  "version": "当前版本号"
}
```

## 目录结构

```
spec-forge/
├── SKILL.md                      # 顶层编排器（含 intake + reactive loop）
├── README.md                     # 本文件
├── agents/
│   ├── requirement-drafter.md    # 需求起草
│   ├── logic-verifier.md         # 算法验证（代码草图）
│   ├── ui-verifier.md            # UI 验证（组件树）
│   ├── flow-verifier.md          # 流程验证（Mermaid 图）
│   ├── quality-checker.md        # 质量检查 + 批判性思考
│   └── task-breaker.md           # 任务拆解（Markdown checkbox）
└── references/
    └── spec-template.md          # SPEC 标准模板
```

## 产出格式

文件名：`{简短说明}-v{版本}-spec.md`

示例：`user-authentication-v1.0.0-spec.md`

## 版本规范

语义化版本 X.Y.Z：
- 主版本（X）：里程碑级重构
- 次版本（Y）：新增内容、重大改进
- 补丁（Z）：每轮循环结束自动 +1

## Intake Interview

**是循环的第一步**，收集需求信息，决定后续调度哪些 subagent。

## QA 批判性思考

quality-checker 会主动挖掘需求中未明确说明的问题：
- 边界条件（空输入、极限情况）
- 异常流程（错误处理、回滚）
- 安全考量（权限、数据隔离）
- 性能假设（并发量、响应时间）
- 依赖风险（外部系统、第三方库）
- 向后兼容（数据迁移、API 版本）

## 设计参考

参考 Anthropic Skill Creator 的设计模式：
- SKILL.md 作为顶层编排器
- Subagents 作为独立技能单元
- Reactive loop 实现自我演进
- 语义化版本管理
