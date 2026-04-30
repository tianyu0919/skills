# Trae Skill: Requirement Manager (需求管理技能)

Requirement Manager 是一个智能的 AI Agent Skill，专为 AI 辅助编程设计。它旨在强制执行“文档先行 (Specification-First, SDD)”的工作流，确保在编写任何代码之前，自动生成标准化、可预测且高度结构化的需求文档。

## ✨ 核心特性

- **4阶段规范框架**：自动生成 `proposal.md`（提案）、`design.md`（设计）、`spec.md`（规格）和 `tasks.md`（任务）。
- **机器可读元数据**：在 `spec.md` 中注入 YAML Frontmatter，使 AI Agent 能够瞬间理解代码影响范围 (impact radius) 和依赖关系 (dependencies)。
- **全局项目注册表**：自动维护 `sdd/project.md` 文件，作为所有活跃和已归档特性的集中索引。
- **零上下文丢失**：通过标准化的文档结构，让 AI 在长时间的编码会话中保持专注，有效防止架构漂移。

## 📂 目录结构与规范说明

该技能通过在项目根目录下的 `sdd` 文件夹中管理需求规范来实现工作流。

### 1. 新需求 (New Requirements)
添加新需求时，会在 `sdd/specs/<需求名称>/` 下创建目录。每个目录必须遵循 SDD 标准结构，包含以下四个核心文件：

- **`proposal.md` (提案)**：记录上下文、现状与痛点、功能价值主张、替代方案考虑以及成功衡量指标。
- **`design.md` (设计)**：记录技术架构、数据模型与接口定义、数据流转以及异常处理策略。
- **`spec.md` (规格)**：详细的产品规格说明，包含 YAML Frontmatter（标识状态、影响范围和依赖）以及功能点细节和验收清单 (Acceptance Checklist)。
- **`tasks.md` (任务)**：将需求拆解为可执行的原子任务看板，按阶段划分（如基础脚手架、核心逻辑、UI 交互等）。

### 2. 现有需求变更 (Modifying Existing Requirements)
修改现有需求时，**不会**覆盖原始规范，而是在现有需求的 `changes` 目录下创建新的变更记录：
`sdd/specs/<现有需求名称>/changes/<变更名称>/`

变更目录同样需要包含上述的四个核心文件（`proposal.md`, `design.md`, `spec.md`, `tasks.md`），以清晰追踪变更的动机和实现细节。

## 🛠 安装指南

1. 在你的项目根目录下，如果不存在，请先创建 `.trae/skills/` (或 `.AGENTS/skills/`) 目录。
2. 将本仓库克隆或放置到该目录中：

```bash
mkdir -p .trae/skills/
cd .trae/skills/
git clone <repository-url> requirement-manager
```

## 🚀 如何使用 (Workflow)

当用户提出以下请求时，即可触发 Requirement Manager 技能：
- “添加一个新需求：...”
- “修改现有功能：...”
- “为新特性创建需求文档...”

### 执行步骤

1. **理解需求**：AI 会与用户澄清需求或变更的具体内容。
2. **确定范围**：判断这是一个全新需求还是对现有功能的变更。
3. **生成结构**：AI 会读取本技能 `references/` 目录下的模板，在 `sdd/specs/` 目录下生成对应的四个 Markdown 文件。
4. **更新全局注册表**：在 `sdd/project.md` 中新增或更新该特性的条目。
5. **填充内容**：根据用户描述，AI 自动编写四个文档的具体内容。
6. **用户确认**：AI 会请求用户检查生成的规范文档，并在获得确认后，进入后续的开发阶段。

## 📌 任务状态与生命周期管理

- **任务跟踪**：在 `tasks.md` 和 `spec.md` 中的所有任务和验收清单，默认使用未完成状态的 Markdown 任务列表 (`- [ ]`)。
- **状态更新**：当某个任务完成时，AI 会将其更新为已完成 (`- [x]`)。
- **特性闭环**：当一个需求的所有任务和验收清单都已完成 (`- [x]`) 时，必须将 `spec.md` YAML Frontmatter 和 `sdd/project.md` 注册表中的状态更新为 `completed`。
- **归档规则 (Archiving)**：
  - **不要**仅仅因为需求已完成就将其归档 (`archived`)。已完成的需求应当保留在活跃的 `sdd/specs/` 目录中，作为当前系统架构的活跃文档。
  - **只有**当用户**明确要求**归档，或者该功能已被全新的系统完全弃用/替换时，才将其移动到 `sdd/archive/` 目录并更新全局注册表。
