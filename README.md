# PRD Writing Skill

一套用于**新建、校验和修改 PRD** 的通用 Agent Skill，帮助产品、研发、测试和 AI 对业务逻辑形成一致理解。

它不追求把 PRD 写得更长，而是让复杂需求具备清晰结构、明确规则、完整边界和可验证的验收标准。

## 核心能力

- 新建 PRD：从业务场景、业务用户、目标和范围开始，逐步形成可执行需求。
- 校验 PRD：识别缺失项、歧义、矛盾、异常遗漏、原型脱节和不可验收描述。
- 修改 PRD：使用“现有逻辑 → 新逻辑 → 影响范围”表达变化，只改与需求相关的内容。
- 现状确认门禁：修改现有系统但未提供现有逻辑时，停止输出依赖该逻辑的最终需求，每次追问一个关键问题，直到确认清楚。
- 技术可读性：使用流程图、泳道图、状态机、判定表和时序图降低理解成本。
- 全场景覆盖：明确主流程、分支、异常、空态、权限、并发、失败、回滚和操作留痕等适用场景。
- 术语与协同：统一名词，区分已确认事实、业务决策、暂时假设和待确认问题，并要求评审结论和答疑负责人。
- 多 Agent 分发：提供 Claude Code、TRAE 和其他支持 Agent Skills 标准的版本。

## 版本更新说明

### 2026-07-16

- 简化 `references/prd-template.md`：从 17 个主章节调整为 8 个主章节，减少模板阅读负担。
- 强化“一页摘要”入口：先呈现目标、范围、核心改动、影响系统和阻塞问题，让评审人更快抓重点。
- 保留关键可执行结构：业务场景、现状与改动、业务流程、状态流转、页面交互、系统规则、异常边界和验收标准。
- 管理后台页面仍按“列表字段 / 筛选项 / 操作 / 权限 / 分页与其他页面元素”的顺序描述，但减少重复解释。
- 明确小需求可以删除无关章节，只保留摘要、现状与改动、验收和待确认问题。

## 关键规则

### 1. 现有逻辑不明确时必须先确认

如果需求涉及现有页面、流程、接口、字段、状态、权限或后台规则，Skill 会先确认：

- 原入口、用户、角色和权限；
- 原流程、状态、触发点、条件和副作用；
- 原字段来源、计算规则、校验和异常处理；
- 原系统集成、通知和操作留痕。

截图只能证明可见内容，不能证明隐藏规则。目标方案也不能反向证明现有逻辑。

### 2. 重要改动必须红色加粗

会改变业务流程、状态、字段取值、操作权限、系统规则、数据结果或验收结论的重要内容，使用以下格式突出显示：

```html
<span style="color:#FF0000"><strong>重要改动内容</strong></span>
```

只标记真正发生变化的关键内容，不整页标红。

### 3. 管理后台按固定顺序描述

管理后台、运营后台或内部管理系统的每个适用页面，按以下顺序说明：

1. 列表页字段及逻辑；
2. 筛选项及逻辑；
3. 操作按钮及逻辑；
4. 权限及逻辑；
5. 分页；
6. 排序、批量选择、空状态、加载状态、异常状态和跳转行为等其他页面元素。

每一项都应明确取值、条件、权限、触发结果和异常处理。

## 目录结构

```text
prd-writing-skill/
├── README.md
├── USAGE.md
├── standard/
│   └── writing-and-reviewing-prds/
│       ├── SKILL.md
│       └── references/
├── claude/
│   └── .claude/skills/writing-and-reviewing-prds/
│       ├── SKILL.md
│       └── references/
└── trae/
    └── writing-and-reviewing-prds/
        ├── SKILL.md
        └── references/
```

三个版本的内容保持一致：

- `standard`：便携标准版；
- `claude`：符合 Claude Code 项目级 Skill 目录结构；
- `trae`：便于通过 TRAE Skills 界面导入。

每个版本均包含以下参考文件：

| 文件 | 用途 |
|---|---|
| `SKILL.md` | 使用条件、硬门禁、工作流程和完成标准 |
| `references/prd-template.md` | PRD 正文结构及管理后台页面模板 |
| `references/clarity-and-alignment.md` | 技术可读性、图表选择和协同规则 |
| `references/scenario-patterns.md` | 资金、接口、移动端等场景模板 |
| `references/review-checklist.md` | PRD 完成前的系统化检查清单 |

## 安装

### Claude Code

在仓库根目录执行：

```bash
mkdir -p <项目目录>/.claude/skills
cp -R claude/.claude/skills/writing-and-reviewing-prds <项目目录>/.claude/skills/
```

安装后的入口文件为：

```text
<项目目录>/.claude/skills/writing-and-reviewing-prds/SKILL.md
```

### TRAE

1. 打开 `Settings → Rule & Skills → Skills → Create`；
2. 导入 `trae/writing-and-reviewing-prds/SKILL.md`；
3. 保留同目录下的 `references/` 及其相对路径。

### 其他 Agent

将以下完整目录复制到目标 Agent 声明的 Skills 目录：

```text
standard/writing-and-reviewing-prds/
```

目标 Agent 需要支持 [Agent Skills 开放标准](https://agentskills.io/)，并能够按相对路径读取 `references/`。

更简短的平台使用说明见 [USAGE.md](USAGE.md)。

## 使用示例

### 新建 PRD

```text
使用 writing-and-reviewing-prds，为商家管理后台的订单导出功能编写 PRD。
```

### 校验 PRD

```text
使用 writing-and-reviewing-prds 校验这份现有 PRD，按阻塞问题、重要问题和优化建议输出结果。
```

### 修改现有需求

```text
使用 writing-and-reviewing-prds 修改订单取消规则。如果现有逻辑不明确，先逐项向我确认，不要自行假设。
```

### 根据系统截图补充需求

```text
使用 writing-and-reviewing-prds 结合系统截图完善 PRD。截图未体现的权限、计算和触发规则必须向我确认。
```

## 推荐提供的输入材料

材料越完整，PRD 越容易快速收敛：

- 业务背景、目标、范围和非目标；
- 业务用户、角色及权限；
- 现有 PRD、系统入口和当前逻辑；
- 原型图、UI 图或系统页面截图；
- 字段来源、状态定义、接口说明和异常规则；
- 已确认的业务决策、待确认事项和相关负责人。

材料不足时，Skill 不会静默补全事实，而是明确标记假设或继续追问。

## 适用文档

- Markdown 和纯文本 PRD；
- Word PRD（要求 Agent 具备 Word 读写与渲染检查能力）；
- 飞书 Docx 或 Wiki PRD（要求 Agent 具备对应连接器和权限）；
- 配有原型图、UI 图、截图、流程图或状态机的需求文档。

## 完成标准

一份 PRD 只有在以下关键条件满足后才应被认定为完成：

- 业务用户能够理解场景和流程；
- 技术人员能够快速定位核心改动、规则和边界；
- 字段取值、状态流转、触发点、权限和异常明确；
- 现有逻辑、新逻辑和影响范围清楚区分；
- 图、文、原型、接口和测试口径一致；
- 验收标准能够明确判断通过或失败；
- 复杂需求已经评审，并记录待确认项和答疑负责人。

## 维护与一致性检查

后续更新时，先修改 `standard/writing-and-reviewing-prds/`，再同步覆盖 Claude 和 TRAE 版本。提交前执行：

```bash
diff -qr standard/writing-and-reviewing-prds claude/.claude/skills/writing-and-reviewing-prds
diff -qr standard/writing-and-reviewing-prds trae/writing-and-reviewing-prds
```

两条命令均无输出，表示三个版本一致。

## 项目原则

- 复杂不等于有效，文档厚度不能替代逻辑清晰度；
- 先确认事实，再设计方案；
- 图表用于降低理解成本，正文负责给出可执行规则；
- 只改与当前需求直接相关的内容；
- 不能验证的描述，不作为最终验收标准。
