<div align="center">

# 🧠 Memory Card — Codex 会话记忆系统

**让 AI 记住你说过的每一句话，随时间自动压缩精简，越用越懂你。**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Codex Skill](https://img.shields.io/badge/Platform-Codex%20Desktop-ff6b35.svg)](https://github.com/nicepkg/codex-desktop)

</div>

---

## 这是什么

Memory Card 是一个 **Codex Desktop 会话记忆插件（Skill）**。它能在每次对话时自动记录你说过的话，生成结构化的「记忆卡」，并随时间推移自动压缩精简——重要的事情保留更久，随口一提的很快会被清理。

**核心理念**：AI 不应该每次都从零开始认识你。

## 功能特点

- **实时记录** — 对话过程中自动捕获你提到的情绪、事件、人物、话题
- **智能压缩** — 按时间自动精简：3天 → 1周 → 1月，重要记忆层层沉淀
- **检索回忆** — 当你说"之前说过""记得吗"时，自动搜索相关记忆卡
- **路径自适应** — 自动检测存储路径，不依赖固定目录
- **中文优先** — 完全面向中文用户设计，时间统一北京时间

## 安装方法

### 方式一：手动安装

1. 下载本仓库所有文件
2. 将整个 `memory-card` 文件夹放到 Codex 的 skills 目录下：

```bash
# macOS / Linux
cp -r memory-card ~/.codex/skills/
```

3. 重启 Codex Desktop，skill 会自动加载

### 方式二：通过 Codex 安装

```bash
# 如果你的 Codex 支持从本地路径安装 skill
codex skill install ./memory-card
```

## 工作原理

```
对话开始 → 创建/读取当天记忆卡
    ↓
对话过程中 → 实时记录关键信息
    ↓
3天后 → 压缩至 500-1000 tokens，删除仅提及1次的内容
    ↓
1周后 → 移动到 month 文件夹，压缩至 300-500 tokens
    ↓
1月后 → 移动到 year 文件夹，压缩至 200 tokens，保留核心四要素
```

### 记忆卡存储结构

```
~/Documents/memory-card/
├── weak/          # 一周内的记忆卡（完整版）
│   └── 08-15.md
├── month/         # 超一周未满一月（压缩版）
│   └── 08-10--项目讨论·压力大.md
└── year/          # 超过一月（极简版）
    └── 2026-07-15--与老板谈加薪·焦虑.md
```

### 记忆卡格式

```markdown
# 记忆卡
- 日期：2026-08-15
- 创建时间：14:30 (北京时间)
- 最后更新：16:45 (北京时间)
- 重要标签：#工作 #项目A #截止日期

## 记录内容
----14:30 用户说：项目A的截止日期提前了，压力很大---
----15:00 用户说：小王也遇到了同样的问题---
----16:45 用户重复：第3次提到截止日期---
```

## 压缩规则

| 时间 | 目标大小 | 保留内容 | 简略内容 | 删除内容 |
|------|---------|---------|---------|---------|
| 3天内 | 500-1000 tokens | 重复40次+、标记"重要"的 | 重复20次+的 | 仅提及1次的 |
| 1周内 | 300-500 tokens | 核心事件、主要情绪、关键人物 | — | 其余 |
| 1月后 | 200 tokens | 时间+人物+事件+情绪（四要素） | — | 其余 |

## 检索方式

当你在对话中提到以下关键词时，系统会自动检索相关记忆卡：

- "之前说过"、"以前"、"上次"、"记忆"、"记得吗"
- 提到特定的时间、人物或事件

## 隐私说明

- 所有记忆卡存储在你的 **本地电脑** 上，不会上传到任何服务器
- 严格遵循「真实记录」原则：只记录你说过的话，不添加推测
- 你可以随时查看、编辑或删除任何记忆卡文件

## 项目结构

```
memory-card/
├── SKILL.md              # Skill 主文件（核心逻辑与规则）
├── README.md             # 本文件
├── LICENSE               # MIT 开源协议
├── .gitignore
├── agents/
│   └── openai.yaml       # Agent 接口配置
├── references/           # 参考文档（预留）
└── scripts/              # 辅助脚本（预留）
```

## 贡献

欢迎提交 Issue 和 Pull Request！如果你有好的想法（比如新的压缩策略、可视化界面等），请开一个 Issue 讨论。

## 许可证

[MIT License](LICENSE) — 自由使用，自由分享。

---

<div align="center">

Made with ❤️ for anyone who wants their AI to actually remember them.

</div>
