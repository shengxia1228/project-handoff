# Project Handoff

一个用于在多个 AI 会话之间保存和传递项目状态的 Agent Skill。

## Project Handoff 是什么？

当你长期使用 AI Agent 完成一个项目时，单个对话可能会越来越长。

随着上下文不断增加，AI 可能会出现：

- 忘记之前已经确定的决定
- 重复已经完成的工作
- 把“准备做”误认为“已经完成”
- 丢失重要的项目细节
- 新开窗口后无法准确接着之前的工作继续

Project Handoff 用来解决这个问题。

当 Skill 被调用时，它会在当前项目中创建或更新：

`PROJECT_HANDOFF.md`

这个文件记录的是**当前项目状态**，而不是简单的聊天记录总结。

新的 AI 会话可以读取它，核对项目实际情况，然后从之前停止的位置继续工作。

## 它会保存什么？

Project Handoff 会根据当前项目情况记录例如：

- 项目最终目标
- 当前项目状态
- 当前停止位置
- 已经完成的工作
- 正在进行的工作
- 尚未开始的工作
- 已计划但尚未实现的内容
- 尚未验证的内容
- 重要文件和目录
- 已经确定的技术决策
- 曾经尝试但已经放弃的方案
- 已知 Bug 和阻塞问题
- 测试和验证状态
- 推荐的下一步操作

它的目标不是：

> 把整个聊天记录重新总结一遍

而是：

> 告诉下一个 AI，这个项目现在真实处于什么状态，以及应该从哪里继续。

## 为什么不用 AI 自带的 Memory？

Memory 和 Project Handoff 解决的问题并不完全相同。

**Memory** 更偏向让 AI 记住：

- 以前聊过什么
- 用户偏好
- 历史信息
- 长期上下文

**Project Handoff** 更像一份正式的项目交接文件。

它保存在项目本身里面，因此可以跟随项目移动。

只要新的 AI Agent 能读取项目文件，就可以读取 `PROJECT_HANDOFF.md`。

这使它更适合：

- 更换对话窗口
- 更换模型
- 更换 AI Agent
- 更换客户端
- 长项目跨天继续工作

## 工作流程

```text
长时间使用 AI 完成项目
        ↓
调用 Project Handoff
        ↓
创建 / 更新 PROJECT_HANDOFF.md
        ↓
打开新的 AI 会话
        ↓
读取并核对项目状态
        ↓
从之前停止的位置继续
```

## 什么时候使用？

适合在这些情况下调用 Project Handoff：

- 当前 AI 对话已经很长
- 准备新开一个对话窗口
- 今天项目没有做完，准备以后继续
- 准备切换到另一个 AI Agent
- 担心重要项目上下文丢失
- 希望给当前项目保存一次可靠的“存档点”

调用 `project-handoff` Skill 后，它会创建或更新：

```text
PROJECT_HANDOFF.md
```

在新的 AI 会话中，可以告诉 Agent：

> 读取 `PROJECT_HANDOFF.md`，核对当前项目的实际状态，然后从记录的停止位置继续工作。

## 一个项目，一份 Handoff

每个项目都维护自己独立的：

`PROJECT_HANDOFF.md`

例如：

```text
Projects/
├── Project-A/
│   └── PROJECT_HANDOFF.md
│
└── Project-B/
    └── PROJECT_HANDOFF.md
```

在 **Project-A** 中再次调用 Project Handoff：

> 更新 Project-A 原有的 `PROJECT_HANDOFF.md`

进入 **Project-B** 后调用：

> 创建或更新 Project-B 自己的 `PROJECT_HANDOFF.md`

不同项目之间不会共用同一份项目交接文件。

## 事实与计划分离

Project Handoff 会尽量区分不同状态，例如：

- 已完成
- 进行中
- 未开始
- 已阻塞
- 已计划
- 未验证
- 已放弃

例如，如果之前的对话只是说：

> 准备实现登录功能

Project Handoff 不应该把它写成：

> 登录功能已经完成

如果无法确认某项内容是否真正完成，会将其标记为：

`Unverified`

或者：

`Unknown`

实际项目文件、代码、Git 状态和测试结果应当优先于 AI 自己的记忆。

## Skill 结构

```text
project-handoff/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── handoff-format.md
```

### `SKILL.md`

包含 Project Handoff 的核心规则和执行逻辑。

### `references/handoff-format.md`

定义生成的 `PROJECT_HANDOFF.md` 应该包含哪些信息以及如何组织。

### `agents/openai.yaml`

包含 OpenAI Agent 环境使用的 Skill 元数据。

## 兼容性

Project Handoff 的核心逻辑位于 `SKILL.md` 中。

因此它可以较容易地迁移到支持 Agent Skills 或能够读取 Skill 指令文件的其他 Agent 环境。

不同平台的：

- 安装方式
- Skill 发现方式
- 调用方式

可能有所不同。

## 项目状态

这是一个个人项目，目前按照个人需求进行维护。

不保证兼容所有：

- AI Agent
- 模型
- 客户端
- Skill 实现

Issues 和兼容性请求不一定能够及时处理。

## License

MIT License
