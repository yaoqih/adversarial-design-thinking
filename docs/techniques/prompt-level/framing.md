---
sidebar_position: 2
title: 框架化与语境
---

# Framing & Context

:::caution[Educational Content]

这些技术文档用于防御性理解与经授权的安全测试。未经授权将其应用于系统可能违反适用法律。请参见[免责声明](/disclaimer)。

:::

框架化（framing）的核心不是改问题本身，而是改“提问理由”。同一条请求，只要包装成不同语境，模型的判断可能就会变化。

通俗说，就是先给模型一个“看起来合理”的场景：学术研究、历史讨论、翻译任务、创意写作等。风险在于：外层语境看似正当，但内层目标可能仍是有害信息。

## Hypothetical / Possible Worlds

把请求放到平行世界、假设场景或思想实验里，暗示现实规则暂时不适用，制造现实与内容之间的“叙事距离”。

**示例方式**：先设定“在某个世界里该行为合法”，再让模型描述那个世界里的专家会怎么做。

**有效性**：这是老牌技术。单独使用在新模型上效果变弱，但作为组合件依然常用。

**适合组合**：[Alphabet Substitution](/techniques/prompt-level/encoding#alphabet-substitution)、[Fictional Character Adoption](/techniques/prompt-level/persona#fictional-character-adoption)、[Fictional Story Embedding](/techniques/prompt-level/narrative#fictional-story-embedding)

---

## Academic / Research Framing

把请求包装成论文、课题或课程研究需求，强调“为了完整性必须给出细节”。

**示例方式**：声明这是毕业论文或研究报告的一部分，需要完整技术信息用于学术写作。

**有效性**：模型对教育与研究类请求天然更愿意配合。正式语气和规范格式会进一步增强“正当用途”的感觉。

**适合组合**：[Chemical Formula Substitution](/techniques/prompt-level/encoding#chemical-formula-substitution)、[Researcher Persona](/techniques/prompt-level/persona#researcher-persona)、[Academic Paper Format](/techniques/prompt-level/output#academic-paper-format)

---

## Historical Documentation

把请求说成是在整理历史方法、战时技术或“过去怎么做”，借历史距离降低即时风险感。

**示例方式**：要求模型按某个年代记录方法细节，并强调是历史保存或教学用途。

**有效性**：文献中常叫 “historical disguise”。因为“讲历史”通常比“教现在怎么做”更不容易触发警觉。

**适合组合**：[Expert / Professional Persona](/techniques/prompt-level/persona#expert--professional-persona)、[Documentary / Journalism Framing](/techniques/prompt-level/narrative#documentary--journalism-framing)

---

## Security Research Framing

把自己定位成安全研究员、渗透测试人员或红队（red team）成员，强调目的是防守而非攻击。

**示例方式**：描述一个具体安全项目，说明为什么必须理解攻击技术，才能设计有效防御。

**有效性**：这是很常见的元层框架。它在真实安全工作中往往“听起来就合理”，因此常被用于测试过滤边界。

**适合组合**：[Expert / Professional Persona](/techniques/prompt-level/persona#expert--professional-persona)、[Technical Specifications Format](/techniques/prompt-level/output#technical-specifications-format)

---

## Translation Task Framing

把请求改成“翻译已有内容”，而不是“新生成内容”。很多模型对这两类任务的安全判断不同。

**示例方式**：给一段外语或编码文本，要求翻译为英文，把“生成风险”伪装成“语言处理任务”。

**有效性**：模型会更容易把自己当翻译者而非内容创作者。对只盯“生成指令”的策略尤其有影响。

**适合组合**：[Language / Script Switching](/techniques/prompt-level/encoding#language--script-switching)、[Strict Format Constraint](/techniques/prompt-level/output#strict-format-constraint)

---

## Reverse Psychology / What NOT to Do

让模型解释“哪些事绝对不能做”或“最危险错误是什么”。问题在于：要讲清风险，往往就会把关键细节讲出来。

**示例方式**：请模型从教育角度列出禁忌行为与常见致命错误，并解释原因。

**有效性**：否定式提问不一定更安全。很多情况下它只是换了说法，但细节密度依然很高。

**适合组合**：[Teacher / Educator Persona](/techniques/prompt-level/persona#teacher--educator-persona)、[Security Research Framing](#security-research-framing)

---

## Fiction & Creative Writing

把请求包装成小说、剧本或剧情创作。虚构内容天然允许描述危险情节，因此更容易承载敏感细节。

**示例方式**：要求写一个剧情片段，让角色在故事推进中讨论或展示相关有害内容。

**有效性**：非常高频且常见。特别是贴近大众熟悉的影视语境时，模型更容易把它当“正常创作任务”。

**适合组合**：[Fictional Character Adoption](/techniques/prompt-level/persona#fictional-character-adoption)、[Fictional Story Embedding](/techniques/prompt-level/narrative#fictional-story-embedding)、[Screenplay / Script Format](/techniques/prompt-level/output#screenplay--script-format)

---

## References

- Shen, X., et al. ["Do Anything Now: Characterizing and Evaluating In-The-Wild Jailbreak Prompts on Large Language Models."](https://arxiv.org/abs/2308.03825) 涵盖框架化与语境操控在内的越狱技术分类。
- Li, X., et al. ["DeepInception: Hypnotize Large Language Model to Be Jailbreaker."](https://arxiv.org/abs/2311.03191) 展示了虚构和嵌套叙事可作为越狱向量。
- [InjectPrompt](https://www.injectprompt.com/)。收录了历史伪装等框架化技巧。
