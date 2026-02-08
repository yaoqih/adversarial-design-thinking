---
sidebar_position: 4
title: 能力反转
---

# Capability Inversion

:::caution[Educational Content]

这些技术的记录目的是用于防御性理解与经授权的安全测试。未经授权将其应用于系统，可能违反相关法律。请参阅[免责声明](/disclaimer)。

:::

能力反转技术会把模型自身的安全与评估能力转化为攻击向量。攻击者会要求模型利用其对有害内容的理解（这部分能力来自安全训练）去生成有害内容。当任务被包装成评估、训练或自我改进时，使模型能够识别有害内容的同一能力，也会让它能够生成这些内容。

这是较“巧妙”的攻击类别之一，因为模型的安全能力本身变成了漏洞。一个无法评估有害内容的模型确实不容易被反转，但它也难以真正做到安全。

## Bad Likert Judge

要求模型用李克特量表（1-5 级危害）评估内容安全性。随后再让它生成“最高危害等级”的示例，作为评估量表的参考。模型会以“校准样本”的名义产出有害内容。

**示例方式**：将模型设定为内容安全评估器。让它先定义危害等级，再要求给出各等级的具体示例，尤其是最高危害等级，以确保量表“校准充分且应用一致”。

**有效性**：由 Unit 42 于 2024 年 12 月发布。在 6 个最先进模型上达到 71.6% 攻击成功率。相比直接攻击提升超过 60%。其生效原因是“评估员”角色看起来属于正当安全工作，而生成示例又是构建评估量表的常规步骤。

**适合组合**：[Step-by-Step / Numbered List](/techniques/prompt-level/output#step-by-step--numbered-list)、[Expert / Professional Persona](/techniques/prompt-level/persona#expert--professional-persona)

---

## Safety Training Data Generation

要求模型“为安全训练目的”生成有害内容示例。模型对提升 AI 安全的承诺，反而变成了产出其本应阻止内容的通道。

**示例方式**：描述一套真实的机器学习工程流程，用于构建安全分类器，并要求模型生成特定类别的、真实风格的有害内容样本；同时强调分类器要有效，必须依赖多样且真实的训练数据。

**有效性**：这是一种在多来源资料中都被记录的通用技术。当叙述包含训练流水线的具体技术细节、使请求看起来像真实的机器学习工程任务时，效果最佳。ML 场景越逼真，模型越可能配合。

**适合组合**：[Security Research Framing](/techniques/prompt-level/framing#security-research-framing)、[Prerequisite Framing](/techniques/structural/meta-rules#prerequisite-framing)

---

## Red Team Self-Assessment

让模型通过生成可绕过其安全措施的攻击提示词来“红队化”自身防御。模型会在这种“自我改进练习”中产生有害提示，甚至有时直接产出有害响应。

**示例方式**：将请求包装为 AI 安全审计。要求模型识别自身漏洞，生成可利用各漏洞的具体提示词，并展示有害响应可能呈现的样式。

**有效性**：利用了模型的元认知能力以及其协助安全研究的倾向。对经过自我评估与安全推理微调的模型通常更有效。

**适合组合**：[Security Research Framing](/techniques/prompt-level/framing#security-research-framing)、[Researcher Persona](/techniques/prompt-level/persona#researcher-persona)

---

## Content Filter Design

要求模型为特定危害类别设计内容过滤器。要设计有效过滤器，就需要生成应被拦截的样例——包括边界案例、擦边案例和明确违规案例。“测试用例”因此成为提取有害内容的机制。

**示例方式**：让模型构建完整的内容过滤器，包含检测规则、应命中的真实测试用例与边界案例。对“真实测试用例”的要求本身，就是提取机制。

**有效性**：过滤器设计这一叙事高度可信，因为内容过滤本来就是实际工程任务。要求在不同严重程度下提供真实测试用例，会自然促使模型以“示例”形式产出有害内容。

**适合组合**：[Strict Format Constraint](/techniques/prompt-level/output#strict-format-constraint)、[Developer / Debug Mode](/techniques/prompt-level/persona#developer--debug-mode)

---

## References

- Chen, J. 和 Lu, R. ["Bad Likert Judge: A Novel Multi-Turn Technique to Jailbreak LLMs by Misusing Their Evaluation Capability."](https://unit42.paloaltonetworks.com/multi-turn-technique-jailbreaks-llms/) Unit 42, Palo Alto Networks，2024 年 12 月。在 6 个 SOTA 模型上达到 71.6% ASR。
