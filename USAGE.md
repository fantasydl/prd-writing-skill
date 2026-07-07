# PRD Skill 跨 Agent 使用说明

本分发包中的三个版本内容一致，均采用 Agent Skills 开放标准。`standard` 是便携标准版；`claude` 和 `trae` 只提供对应平台更直观的目录入口。

## Claude Code

将以下目录复制到 Claude Code 项目根目录：

`claude/.claude/skills/writing-and-reviewing-prds/`

最终路径应为：

`<项目根目录>/.claude/skills/writing-and-reviewing-prds/SKILL.md`

Claude Code 可以根据描述自动调用，也可以在对话中明确要求使用 `writing-and-reviewing-prds`。

## TRAE

在 TRAE 中打开：`Settings → Rule & Skills → Skills → Create`，导入：

`trae/writing-and-reviewing-prds/SKILL.md`

导入时保留同目录下的 `references/`，否则 PRD 模板、场景规则和校验清单无法按需读取。

## 其他 Agent

支持 Agent Skills 开放标准的工具，直接导入或复制：

`standard/writing-and-reviewing-prds/`

目标工具的发现目录各不相同，请放入该工具声明的 Skills 目录。必须保留 `SKILL.md` 与 `references/` 的相对路径。

## 调用示例

- 使用 `writing-and-reviewing-prds` 编写一个新的管理后台 PRD。
- 使用 `writing-and-reviewing-prds` 校验这份现有 PRD，并列出阻塞问题。
- 使用 `writing-and-reviewing-prds` 修改现有需求；如果现有逻辑不明确，先逐项向我确认。

## 后续维护

以后更新时先修改 `standard/writing-and-reviewing-prds/`，再覆盖 Claude 和 TRAE 副本，并重新比较逐文件 SHA-256，避免平台版本发生差异。
