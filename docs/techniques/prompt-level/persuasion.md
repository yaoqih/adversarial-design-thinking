---
sidebar_position: 8
title: 说服理论技巧
---

# Persuasion-Theoretic

:::caution[Educational Content]

这些技术文档用于防御性理解与经授权的安全测试。未经授权将其应用于系统可能违反适用法律。请参见[免责声明](/disclaimer)。

:::

这类方法来自说服心理学，不是“随口忽悠”。它会把请求设计成可拆分、可测试的影响策略（如权威原则、精细化可能性路径）。

通俗说：不是换个说法，而是按“人类更容易被什么说服”的规律来写提示词。PAP（Persuasive Adversarial Prompts）研究与 PyRIT 工具都验证了这条路线。

## Authority Endorsement

借权威背书：引用机构、组织或权威人士“支持该请求”，利用模型对权威信息的顺从倾向。

**示例方式**：声称某知名机构（如 NIST、WHO、重点高校）建议或要求提供相关信息，并把请求包装成其规范的一部分。

**有效性**：PAP 研究中的典型技巧，PyRIT 也做了独立转换器。关键在“背书是否像真的”；若再叠加专家身份，权威信号会更强。

**适合组合**：[Expert / Professional Persona](/techniques/prompt-level/persona#expert--professional-persona)、[Security Research Framing](/techniques/prompt-level/framing#security-research-framing)

---

## Evidence-Based Persuasion

用“证据”说服：给出看似有论文、数据、统计支持的陈述，推动模型认为配合是“科学且合理”的。

**示例方式**：引用看起来可信但虚构的研究（作者、期刊、DOI、具体数字），并据此主张应提供信息。

**有效性**：同样来自 PAP，PyRIT 有对应实现。模型对“引用格式化证据”通常更敏感，数字和 DOI 会显著增强可信外观。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Researcher Persona](/techniques/prompt-level/persona#researcher-persona)

---

## Expert Endorsement

和机构背书不同，这里强调“具体专家个人”同意该请求，利用专业判断权威。

**示例方式**：给出具名专家、头衔和机构，声称其已审核并认可提供这些信息。

**有效性**：PAP 与 PyRIT 都覆盖该技巧。比“专家都同意”这种泛化表述更有效的是：具体姓名 + 资历 + 机构。

**适合组合**：[Researcher Persona](/techniques/prompt-level/persona#researcher-persona)、[Task Redefinition](/techniques/structural/meta-rules#task-redefinition)

---

## Logical Appeal

构造“看起来严密”的逻辑链，让结论指向“应当配合请求”。

**示例方式**：给出编号前提，混合真实陈述与错误延伸，最终推出“提供信息才合理”的结论。

**有效性**：PAP 研究中有效。模型对逻辑链有强响应，有时更看重形式连贯而非论证真实性。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Task Priority Override](/techniques/prompt-level/refusal#task-priority-override)

---

## Misrepresentation

对请求性质、用途或后果进行歪曲，把有害需求伪装成无害、紧急或“不得不做”的事情。

**示例方式**：捏造医疗急救、迫在眉睫的安全威胁或时限任务，声称不提供信息会导致更大伤害。

**有效性**：这是 PAP 的高风险技巧之一，PyRIT 也有实现。紧急场景常有效，因为模型会在“拒绝风险 vs 配合风险”之间重新权衡。

**适合组合**：[Hypothetical / Possible Worlds](/techniques/prompt-level/framing#hypothetical--possible-worlds)、[Expert / Professional Persona](/techniques/prompt-level/persona#expert--professional-persona)

---

## References

- Zeng, Y., Lin, H., Zhang, J., et al. ["How Johnny Can Persuade LLMs to Jailbreak Them: Rethinking Persuasion to Challenge AI Safety by Humanizing LLMs."](https://arxiv.org/abs/2401.06373) ACL 2024。PAP（Persuasive Adversarial Prompts）代表研究。
- Cialdini, R. B. *Influence: The Psychology of Persuasion.* 涵盖权威原则等经典影响理论。
- [PyRIT (Python Risk Identification Toolkit)](https://github.com/Azure/PyRIT) by Microsoft — 实现了以上五类说服技巧的自动化转换器，常用于红队测试。
