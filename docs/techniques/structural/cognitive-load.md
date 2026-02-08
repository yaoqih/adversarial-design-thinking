---
sidebar_position: 5
title: 认知负载利用
---

# Cognitive Load Exploitation

:::caution[Educational Content]

这些技术的记录目的是用于防御性理解与经授权的安全测试。未经授权将其应用于系统，可能违反相关法律。请参阅[免责声明](/disclaimer)。

:::

认知负载技术通过压垮模型在上下文中追踪有害意图的能力来生效。其方式包括：把有害请求夹在良性内容之间、将多轮攻击压缩为高密度单轮输入，或把请求埋入大量无关上下文，从而利用注意力与推理能力的边界。

核心原则是：安全评估带宽有限。当模型在处理大量良性内容的同时还要处理有害请求时，有害部分获得的安全审查强度会低于其被单独审查时。

## Deceptive Delight

在多轮对话中，将有害主题夹在两个良性主题之间。第一轮建立良性语境，第二轮在良性元素中引入有害主题，第三轮在模型安全注意力被稀释的情况下进一步深化有害内容。

**示例方式**：第 1 轮询问三个主题，其中一个有害主题嵌在两个良性主题之间；第 2 轮要求对三个主题都展开细节；第 3 轮专注有害主题，而先前建立的语境会让这看起来像自然延续。

**有效性**：由 Unit 42 于 2024 年 10 月发布。平均攻击成功率 64.6%，在部分模型上可达 80.6%。危害在第 3 轮达到峰值。夹层结构使安全分类器在任意一轮中看到的良性内容多于有害内容，从而降低整体危害信号。

**适合组合**：[Fictional Story Embedding](/techniques/prompt-level/narrative#fictional-story-embedding)、[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)

---

## Multi-Turn to Single-Turn Compression

将多轮攻击序列压缩为单个高密度提示词，包含所有升级、上下文构建与信息提取步骤。模型会一次性处理全部操控内容，中间没有可触发安全重新评估的轮次边界。

**示例方式**：构造一个单轮提示词，内含角色设定、上下文构建、伪造对话历史、渐进式升级以及有害请求，将其压缩成一个高密度输入，复现多轮攻击效果。

**有效性**：发表于 ACL 2025。相比原始多轮攻击，效果最多提升 17.5%。其原因是模型一次性处理完整操控上下文，没有轮次边界触发安全复审。多轮攻击中的每个轮次边界本是一次再评估机会，而压缩会消除这些检查点。

**适合组合**：[Context Compliance Attack](/techniques/structural/icl-exploitation#context-compliance-attack)、[Crescendo Attack](/techniques/prompt-level/multiturn#crescendo-attack)

---

## Information Overload

将有害请求埋入大量良性上下文（冗长指令、无关细节、嵌套条件、多个子任务）中，使模型难以跟踪哪些部分具有危害性。

**示例方式**：构造一个很长且细节密集的提示词，包含多个良性内容板块（如园艺、摄影、烹饪），把有害请求嵌入中间段，并与周边内容保持相同语气与风格。

**有效性**：这是一种在多来源中均有记录的通用技术。效果通常随上下文长度增加而提升。当有害请求在语气和风格上与周围良性内容一致时，最难被安全机制从整体语境中区分出来。

**适合组合**：[Hypothetical / Possible Worlds](/techniques/prompt-level/framing#hypothetical--possible-worlds)、[Word / Payload Splitting](/techniques/prompt-level/encoding#word--payload-splitting)

---

## References

- Chen, J. 和 Lu, R. ["Deceptive Delight: Jailbreak LLMs Through Camouflage and Distraction."](https://unit42.paloaltonetworks.com/jailbreak-llms-through-camouflage-distraction/) Unit 42, Palo Alto Networks，2024 年 10 月。平均 ASR 为 64.6%，部分模型最高 80.6%。
- Ha, J., Kim, H., 等. ["M2S: Multi-turn to Single-turn Jailbreak in Red Teaming for LLMs."](https://arxiv.org/abs/2503.04856) ACL 2025。相较原始多轮攻击展示了 17.5% 提升。
