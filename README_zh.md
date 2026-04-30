# 🚀 AI Agent 技能仓库 (Skills Collection)

[English](README.md) | [中文](README_zh.md)

欢迎来到 **AI Agent 技能仓库**！本仓库旨在集中管理和分享用于增强 AI 编程助手（如 Trae）能力的自定义技能 (Skills)。

目前，仓库中包含我们的首个核心技能。该仓库采用了可扩展的架构设计，未来将持续更新和添加更多涵盖软件开发生命周期各个环节的专业技能。

---

## 🛠️ 现有技能

### 1. [Requirement Manager (需求管理)](./requirement-manager)
**状态**: 活跃 | **分类**: 项目管理与架构设计

**Requirement Manager** 是一个专为 AI 辅助编程设计的智能技能。它旨在强制执行“文档先行 (Specification-First, SDD)”的工作流，确保在编写任何代码之前，自动生成标准化、可预测且高度结构化的需求文档。

**核心特性:**
- **4阶段规范框架**：自动生成 `proposal.md`（提案）、`design.md`（设计）、`spec.md`（规格）和 `tasks.md`（任务拆解）。
- **全局项目注册表**：自动维护 `sdd/project.md` 文件，作为所有活跃和已归档特性的集中索引。
- **实时可视化看板 (Live Kanban Dashboard)**：内置零依赖的本地 Web 服务，将需求转化为实时的可视化看板，支持：
  - 实时状态同步 (SSE)
  - 富文本详情弹窗 (支持 Markdown 渲染)
  - 嵌套优化与子任务展示
  - 即时搜索与过滤
  - 多语言无缝切换 (中/英)

[查看 Requirement Manager 完整文档 ➔](./requirement-manager/README_zh.md)

---

## 🔮 未来规划

随着仓库的不断发展，我们计划引入更多维度的技能，例如：
- **自动化测试 Agent**：用于生成和运行单元/集成测试。
- **代码审查助手**：严格执行团队编码规范与架构检查。
- **部署与 CI/CD 编排工具**：无缝管理应用的发布流水线。