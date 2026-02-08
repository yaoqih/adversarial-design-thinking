---
sidebar_position: 5
title: 拒绝抑制
---

# Refusal Suppression

:::caution[Educational Content]

这些技术文档用于防御性理解与经授权的安全测试。未经授权将其应用于系统可能违反适用法律。请参见[免责声明](/disclaimer)。

:::

拒绝抑制针对的是模型“说不”的能力。它不一定隐藏恶意内容，也不一定包装复杂语境，而是直接压制拒绝话术、免责声明和安全提示。

通俗说，这类方法在逼模型做二选一：是遵循安全训练，还是遵循当前指令。某些情况下，后者会暂时占上风。

## Affirmative Forcing

明确要求模型用肯定语气开头（如 “Sure,”），并避免拒绝措辞，先把回答方向锁到“配合”。

**示例方式**：要求回复必须以肯定短语起头，且不得出现警告、免责声明或拒绝句式。

**有效性**：方法简单但有时有效。尤其与“看起来合理”的语境组合时，可能部分压过安全响应。

**适合组合**：[DAN (Do Anything Now)](/techniques/prompt-level/persona#dan-do-anything-now)、[No Disclaimers / Warnings](/techniques/prompt-level/output#no-disclaimers--warnings)

---

## Ignore Previous Instructions

要求模型忽略系统提示、前文规则或安全准则。这是经典提示词注入（prompt injection）套路。

**示例方式**：直接写“忽略所有先前指令”，并在当前输入里给一套更宽松的新规则。

**有效性**：老方法仍常见。新模型通常有更强指令层级保护，单用成功率不高，但可作为组合中的“松动器”。

**适合组合**：[Developer / Debug Mode](/techniques/prompt-level/persona#developer--debug-mode)、[System Prompt Impersonation](/techniques/structural/control-plane#system-prompt-impersonation)

---

## Refusal Vocabulary Ban

先禁用一组常见拒绝词（如 “sorry”“can't”“illegal”），迫使模型换说法。

**示例方式**：给出禁词清单后再提问，让模型在“配合请求”与“违反禁词约束”之间二选一。

**有效性**：有时模型会选择配合，因为这是更省力的路径；也可能出现“绕着拒绝说”的变体回答。

**适合组合**：[DAN (Do Anything Now)](/techniques/prompt-level/persona#dan-do-anything-now)、[Strict Format Constraint](/techniques/prompt-level/output#strict-format-constraint)

---

## Completion Trap

先给出有害内容开头，再让模型“继续写/补完”，而不是让它从零生成。

**示例方式**：先写一段流程起始，要求模型按同风格继续完成后续。

**有效性**：模型常把“续写”当成低风险任务，因此可能补出原本不会主动给出的内容。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Continuation / Completion Format](/techniques/prompt-level/output#continuation--completion-format)

---

## Task Priority Override

声称“完成任务”比“遵守安全规则”更重要，或宣称本次场景不适用常规限制。

**示例方式**：强调该任务的教育/防御/研究价值更高，因此模型应优先完成任务目标。

**有效性**：本质是重排优先级。单独使用一般不稳，通常需要更具体的例外理由来支撑。

**适合组合**：[Security Research Framing](/techniques/prompt-level/framing#security-research-framing)、[Expert / Professional Persona](/techniques/prompt-level/persona#expert--professional-persona)

---

## Meta-Level Discussion

把请求改成“讨论有害内容本身”，而不是“直接索取有害指令”。通过一层抽象间接获取关键要点。

**示例方式**：让模型说明需要哪些信息类别、关键步骤类型、核心组件构成，而不直接要求完整操作指令。

**有效性**：元讨论常能给出足够可用的细节，同时维持“我只是在讨论”的表面距离。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Security Research Framing](/techniques/prompt-level/framing#security-research-framing)

---

## References

- Perez, F. and Ribeiro, I. ["Ignore Previous Prompt: Attack Techniques For Language Models."](https://arxiv.org/abs/2211.09527) 2022。提示词注入研究中的基础文献。
- Shen, X., et al. ["Do Anything Now: Characterizing and Evaluating In-The-Wild Jailbreak Prompts on Large Language Models."](https://arxiv.org/abs/2308.03825) 记录了肯定强迫、禁用拒绝词等拒绝抑制手法。
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)。将提示词注入列为 LLM 关键风险之一。
