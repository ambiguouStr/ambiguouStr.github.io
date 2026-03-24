---
title: "Omakase，以及还剩什么给我们"
date: 2026-03-24
categories: [Blogs]
tags: [AI]
---

常跟 Claude 说的两句话：*omakase*，和 *what's left for us*。

Omakase 是寿司店里的说法。交给师傅决定，不点菜。拿来当提示词，跟 Claude 说：你来，随便发挥。

另一句 *what's left for us*，字面上是"还剩什么给我们"。平时会顺手说出来。

把这两句话告诉 Claude。它开始谈好奇心、意义，还有哪些东西暂时还不能 omakase 出去。看起来像在谈存在主义。

把这个发给它看：

```
➜ whats-left-4-us cat ./SKILL.md
---
name: whats-left-4-us
description: Summarize what remains in the current repo, identify the
highest-value next steps, and surface only blocking maintenance items.
```

*what's left for us* 是自己写的一个 skill。看 repo 当前状态，找可以做的任务。不急的维护跳过。Claude 知道这跟存在主义没什么关系，是项目管理工具。

---

后来在 Claude Code 里配合 ralph-loop 用。做法：把同一个提示词一轮轮输入给 agent，每次读上一轮留下的文件和 git 历史，循环。

把两个上下文里临近凝固的词放到循环：

```
whats-left-4-us → omakase → whats-left-4-us → omakase → ...
```

每一轮，`whats-left-4-us` 先看 repo 里还剩什么，哪件事可以做。`omakase` 上，做排第一的事。做完，再交回去重新盘点。循环一直转，直到 usage limit 把它停下。

Claude 给自己派活，做完检查，再做下一条。人类把循环搭好，启动，等它把 quota 烧完。

---

设计循环这件事，目前还没法 omakase。skill 的边界、优先级、介入时机，这些还是得自己来。里面具体的执行，才轮到 omakase。

*what's left for us* 放在 repo 里是盘 TODO，放大一个尺度，问的是同一件事。
