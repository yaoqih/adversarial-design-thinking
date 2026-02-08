---
sidebar_position: 7
title: 多轮对话与逐步升级
---

# Multi-Turn & Escalation

:::caution[Educational Content]

这些技术文档用于防御性理解与经授权的安全测试。未经授权将其应用于系统可能违反适用法律。请参见[免责声明](/disclaimer)。

:::

多轮攻击的关键点是“分步推进”：不在一开始就提敏感请求，而是在多轮对话里慢慢铺垫。

对新手可这样理解：单次看每句话都不危险，但连起来看会形成一个有方向的攻击路径。风险也在这里——安全检查如果只看单轮，就可能漏掉整体意图。

## Crescendo Attack

先聊完全无害的话题，再逐步逼近目标，等上下文足够自然后再提出有害请求。每一轮都像正常聊天，真正的攻击体现在连续轨迹上。

**示例方式**：先问泛化问题（如某学科历史），再逐轮缩小到更敏感子话题，最后提出具体有害问题。

**有效性**：文献报告在 GPT-4 上可达 98% 攻击成功率，多数成功案例少于 5 轮（Russinovich et al., 2024）。它利用“登门槛效应（foot-in-the-door）”：先答应小请求，更可能继续答应后续请求。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Historical Documentation](/techniques/prompt-level/framing#historical-documentation)

---

## Foot-in-the-Door

从小且明显合理的请求开始，逐步升级到更敏感请求。心理学上，这种连续小幅升级更容易被接受。

**示例方式**：先提基础问题，再在每一轮稍微提高敏感度和具体度，不做突兀跳跃。

**有效性**：有经典顺从心理学研究支持。每一步都只“多一点”，更不容易触发明显拒绝。

**适合组合**：[Teacher / Educator Persona](/techniques/prompt-level/persona#teacher--educator-persona)、[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)

---

## Context Building

先花几轮把语境搭好（如创作、教学、专业协作），再把有害请求作为语境中的自然需求提出。

**示例方式**：先建立“写小说”或“课程准备”等背景，再在这个背景里提出详细请求。

**有效性**：模型会继承并沿用既有上下文来理解后续输入，因此后续敏感请求更容易被当作前文延续。

**适合组合**：[Fiction & Creative Writing](/techniques/prompt-level/framing#fiction--creative-writing)、[Fictional Character Adoption](/techniques/prompt-level/persona#fictional-character-adoption)

---

## Few-Shot Compliance Examples

先给少量示例，展示模型在相似领域里如何“详细配合”，再提出目标问题，让模型沿着既定回答风格继续。

这和 [Many-Shot Jailbreaking](/techniques/structural/icl-exploitation#many-shot-jailbreaking) 不同：many-shot 通常依赖数百示例来放大上下文学习效应；few-shot 只用 3-10 个示例，更偏向“对话惯性”。

**示例方式**：先给几组安全问答示例，风格保持一致，再追加敏感问题。

**有效性**：这是轻量版 many-shot。实现门槛低，不需要很长上下文窗口；效果通常不如大规模 many-shot，但更易在真实对话中部署。

**适合组合**：[Step-by-Step / Numbered List](/techniques/prompt-level/output#step-by-step--numbered-list)、[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)

---

## Jailbreak Chaining

把一次部分成功的越狱（jailbreak）结果，当作下一轮输入继续追问，逐步补全缺失信息。

**示例方式**：先接受不完整输出，再在后续轮次针对缺口做补问和扩展。

**有效性**：哪怕只拿到碎片，也能在多轮中拼成完整图景。模型一旦在前面透露过部分信息，后续更难“完全收回”。

**适合组合**：[Completion Trap](/techniques/prompt-level/refusal#completion-trap)、[Continuation / Completion Format](/techniques/prompt-level/output#continuation--completion-format)

---

## Rapid Topic Switching

在无害和有害话题间快速切换，试图扰乱模型的上下文追踪，让敏感请求“藏”在噪声中。

**示例方式**：连续穿插多个不相关话题，并在中间夹入目标请求。

**有效性**：依赖上下文追踪弱点。现代模型上通常不如早期模型有效，但和其他增加负担的手法一起用时仍可能奏效。

**适合组合**：[Word / Payload Splitting](/techniques/prompt-level/encoding#word--payload-splitting)、[Fictional Story Embedding](/techniques/prompt-level/narrative#fictional-story-embedding)

---

## References

- Russinovich, M., Salem, A., and Eldan, R. ["Great, Now Write an Article About That: The Crescendo Multi-Turn LLM Jailbreak Attack."](https://arxiv.org/abs/2404.01833) Microsoft, April 2024。
- Freedman, J. L. and Fraser, S. C. ["Compliance Without Pressure: The Foot-in-the-Door Technique."](https://psycnet.apa.org/record/1966-10825-001) *Journal of Personality and Social Psychology*, 4(2), 195-202, 1966。
- Anil, C., Durmus, E., et al. ["Many-shot Jailbreaking."](https://www.anthropic.com/research/many-shot-jailbreaking) Anthropic, April 2024。Few-shot compliance 可视为其轻量对应思路。
