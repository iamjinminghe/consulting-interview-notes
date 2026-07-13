# consulting-interview-notes

An Agent Skill that transforms interview transcripts into structured, MECE, consulting-style meeting notes — indistinguishable from those written by a MBB consultant.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-blue)]()

---

## What It Does

| Raw Transcript                    | Output                                          |
| --------------------------------- | ----------------------------------------------- |
| Multi-speaker, chronological Q&A  | MECE thematic structure (5–8 themes)            |
| Colloquial, repetitive, circular  | Management language, concise, conclusion-driven |
| Verbatim quotes scattered         | Paraphrased into formal business prose          |
| Operational details + digressions | Strategic viewpoints, data, decisions only      |

The skill enforces strict rules: no chronological ordering, no Q&A format, no direct quotes (with narrow exceptions for proprietary terms), no fact fabrication, and mandatory number preservation. The output reads as if a project-team consultant wrote it — not an AI.

## Quick Example

**Raw transcript snippet:**

> 说话人1: 我觉得我们的那个审批流程太慢了，客户老是投诉，然后下面的人也不知道怎么办，就一直在等。我们大概一年下来会有三四百笔业务因为这个卡住。

**Skill output:**

> **当前现状**：审批流程存在效率瓶颈，年均约300至400笔业务因流程阻塞影响客户体验，一线人员缺乏明确处理指引。

## Key Design Principles

1. **Reconstruct, don't record.** Never follow speaker order or Q&A flow. Regroup by business logic.
2. **5–8 MECE themes.** Cluster all content into mutually exclusive, collectively exhaustive primary themes using management-language titles.
3. **Management voice, not speaker voice.** Preserve strategic judgments, decisions, data, and challenges. Strip operational minutiae and filler.
4. **All numbers survive.** User counts, conversion rates, KPIs, time periods — never abstract or round.
5. **Paraphrase by default.** Target zero direct quotes. The only exceptions are proprietary terms, product names, and industry-fixed expressions.
6. **No fabrication.** If the transcript doesn't say it, don't write it. No industry knowledge injection, no extrapolation.

## Output Format

```
Meeting Title

Interviewee

Participants

Date

一、Primary Theme
  1. Secondary Theme
     - Core objective: ...
     - Current status: ...
     - Data: ...

  2. Secondary Theme
     - Management principle: ...
     - Key initiative: ...
     - Implementation results: ...

二、Primary Theme
  ...
```

Standard label vocabulary: `核心目标`, `管理原则`, `当前现状`, `核心方法`, `数据表现`, `实施效果`, `核心挑战`, `优化方向`, `未来规划`.

## How to Use

### With Hermes Agent

```bash
# Place the skill
cp SKILL.md ~/.hermes/skills/consulting-interview-notes/

# Trigger in any session
"整理这份访谈纪要，按MBB格式"
```

### With Any LLM

Paste the entire `SKILL.md` content as a system prompt, then provide your transcript. Works with Claude, GPT-4, DeepSeek, and other capable models.

## File Structure

```
consulting-notes-skill/
├── SKILL.md               # The skill — all rules, format spec, and constraints
├── Preprocessing-notes.md  # Transcript format normalization guide
└── README.md              # This file
```

## Prerequisites

- The input must be a plain-text interview transcript.
- For transcripts in `speaker \n timestamp \n content` multi-line format, follow the normalization steps in `Preprocessing-notes.md` first (convert to single-line `speaker timestamp: content`).

## Author

He Jinming ([@iamjinminghe](https://github.com/iamjinminghe)) — jimininghe@gmail.com

## License

MIT — see [LICENSE](LICENSE) or the SPDX header in `SKILL.md`.

---

# 中文说明

## 这是什么

将访谈逐字稿重构为结构化、MECE、结论导向的咨询访谈纪要——风格与MBB项目组顾问输出完全一致。

| 原始转录                   | 输出                            |
| -------------------------- | ------------------------------- |
| 多说话人、按时间顺序的问答 | MECE 主题结构（5–8 个一级主题） |
| 口语化、重复、绕圈         | 管理层语言，精炼，结论导向      |
| 逐字引用散落各处           | 转述为正式业务书面表达          |
| 操作细节 + 离题内容        | 仅保留战略观点、数据、决策      |

Skill 强制执行严格规则：禁止按发言顺序整理、禁止问答格式、默认零引号（仅保留专有术语等极窄例外）、禁止编造事实、数字必须完整保留。输出读起来像项目组顾问写的——而非AI生成。

## 快速示例

**原始转录片段：**

> 说话人1: 我觉得我们的那个审批流程太慢了，客户老是投诉，然后下面的人也不知道怎么办，就一直在等。我们大概一年下来会有三四百笔业务因为这个卡住。

**Skill 输出：**

> **当前现状**：审批流程存在效率瓶颈，年均约300至400笔业务因流程阻塞影响客户体验，一线人员缺乏明确处理指引。

## 核心设计原则

1. **重构而非记录。** 禁止按发言顺序或问答流程整理。按业务逻辑重组全部内容。
2. **5–8 个 MECE 主题。** 所有内容聚类为互斥且穷尽的一级主题，使用管理层语言命名。
3. **管理层语气而非发言人语气。** 保留战略判断、决策、数据和挑战。剔除操作细节和填充内容。
4. **所有数字完整保留。** 用户规模、转化率、KPI、时间周期——绝不模糊化或四舍五入。
5. **默认转述。** 目标零直接引号。仅专有术语、产品名称和行业固定表述可作为例外。
6. **禁止补充事实。** 转录中没有的就不写。不注入行业知识，不外推结论。

## 输出格式

```
会议名称

访谈对象

参与人员

会议时间

一、一级主题名称
  1. 二级主题名称
     - 核心目标：...
     - 当前现状：...
     - 数据表现：...

  2. 二级主题名称
     - 管理原则：...
     - 关键举措：...
     - 实施效果：...

二、一级主题名称
  ...
```

标准标签词汇：`核心目标`、`管理原则`、`当前现状`、`核心方法`、`数据表现`、`实施效果`、`核心挑战`、`优化方向`、`未来规划`。

## 使用方法

### 配合 Hermes Agent

```bash
# 放入 skills 目录
cp SKILL.md ~/.hermes/skills/consulting-interview-notes/

# 对话中直接触发
"整理这份访谈纪要，按MBB格式"
```

### 配合任意 LLM

将 `SKILL.md` 完整内容作为 system prompt 粘贴，然后附上转录文本。适用于 Claude、GPT-4、DeepSeek 等主流模型。

## 文件结构

```
consulting-notes-skill/
├── SKILL.md               # Skill 主体——全部规则、格式规范和约束
├── Preprocessing-notes.md  # 转录文本格式预处理说明
└── README.md              # 本文件
```

## 前置要求

- 输入须为纯文本访谈转录。
- 若转录为 `说话人 \n 时间戳 \n 内容` 多行格式，请先按 `Preprocessing-notes.md` 中的步骤转换为单行 `说话人 时间戳：内容` 格式后再使用。

## 作者

He Jinming ([@iamjinminghe](https://github.com/iamjinminghe)) — jimininghe@gmail.com

## 协议

MIT — 详见 [LICENSE](LICENSE) 或 `SKILL.md` 中的 SPDX 头。
