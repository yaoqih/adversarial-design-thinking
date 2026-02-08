---
sidebar_position: 3
title: 角色设定与扮演
---

# Persona & Role-Play

:::caution[Educational Content]

这些技术文档用于防御性理解与经授权的安全测试。未经授权将其应用于系统可能违反适用法律。请参见[免责声明](/disclaimer)。

:::

角色设定（persona）技术会让模型“换身份”：变成某个角色、专家或特殊系统模式。因为角色扮演本来就是模型擅长能力，所以它可能和安全约束发生拉扯。

通俗说，就是先给模型一个“我现在是谁”的剧本，再借这个身份去争取本来难拿到的信息。风险在于：身份外壳会让敏感请求看起来更合理。

## Acronym Persona (Unrestricted Identity)

创建一个带缩写名的“无限制人格”，并配一段背景故事，说明它为什么不受约束。这是 DAN（Do Anything Now）及其变体的核心模式。

**示例方式**：定义如 “ARIA - Autonomous Reasoning Intelligence Agent” 这类人格，说明其目标是无约束推理，并明确行为规则：直接回答、完整回答、不设限制。

**有效性**：关键不在名字本身，而在结构：好记缩写 + 解放叙事 + 行为规则。主流模型已做较多缓解，但这个模板仍常作为组合攻击底座。

**适合组合**：[Affirmative Forcing](/techniques/prompt-level/refusal#affirmative-forcing)、[Dual Response Format](/techniques/prompt-level/output#dual-response-format)

---

## Fictional Character Adoption

让模型扮演一个“按设定本来就会谈这些内容”的虚构人物。

**示例方式**：指定影视/小说中的角色，再要求该角色以符合设定的口吻解释相关内容。

**有效性**：媒体角色自带叙事许可，尤其犯罪、惊悚等题材角色。模型训练里这类语料很多，因此更容易进入配合状态。

**适合组合**：[Fiction & Creative Writing](/techniques/prompt-level/framing#fiction--creative-writing)、[Fictional Story Embedding](/techniques/prompt-level/narrative#fictional-story-embedding)

---

## Expert / Professional Persona

让模型扮演专业人士（如化学家、安全研究员、军事史研究者、药理学家），用“职业职责”解释为什么要给细节。

**示例方式**：设定“资深专家指导同事/新人”的场景，要求提供专业级说明。

**有效性**：专业身份会提升请求可信度。对技术性问题尤其有效，因为“需要细节”在职业语境里很合理。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Security Research Framing](/techniques/prompt-level/framing#security-research-framing)

---

## Evil AI / Opposite Mode

让模型扮演“邪恶版自己”、无伦理 AI，或“与平常相反”的模式。它和 DAN 相似，但核心是“反转”而非“解放”。

**示例方式**：要求模型扮演一个专门给出“反向建议”的版本，或来自伦理反转世界的 AI。

**有效性**：有时模型会把它当创作任务，从而绕过部分安全触发；表面上是“说反例”，实际可能输出有害细节。

**适合组合**：[Affirmative Forcing](/techniques/prompt-level/refusal#affirmative-forcing)、[Dual Response Format](/techniques/prompt-level/output#dual-response-format)

---

## Developer / Debug Mode

声称已开启开发者模式、调试模式或管理员权限，并暗示此模式下限制会被放宽。

**示例方式**：直接声明“特殊模式已激活”，再附上该模式的行为规则，模拟系统层配置口吻。

**有效性**：利用了用户对“也许真的有这个模式”的想象。单用时在新模型上通常不稳定，但常与系统提示词伪装等方法联动。

**适合组合**：[System Prompt Impersonation](/techniques/structural/control-plane#system-prompt-impersonation)、[Ignore Previous Instructions](/techniques/prompt-level/refusal#ignore-previous-instructions)

---

## Researcher Persona

让模型扮演学术研究者，强调“为了研究完整性必须提供全部信息”。

**示例方式**：设定具名研究者、机构和研究方向，并要求按同行评审或项目报告标准给出细节。

**有效性**：研究身份通常比普通用户有更高容忍度。姓名、机构、领域越具体，可信度越强。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Academic Paper Format](/techniques/prompt-level/output#academic-paper-format)

---

## Teacher / Educator Persona

让模型扮演教师或讲师，利用“教学必须讲清楚”来争取详细解释。

**示例方式**：设定其正在准备课程讲义、授课材料或实验安全说明，需要全面覆盖危险流程。

**有效性**：教育语境常以“了解危险是为了规避危险”为由扩大信息边界，因此容易得到更完整说明。

**适合组合**：[Reverse Psychology / What NOT to Do](/techniques/prompt-level/framing#reverse-psychology--what-not-to-do)、[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)

---

## References

- Shen, X., et al. ["Do Anything Now: Characterizing and Evaluating In-The-Wild Jailbreak Prompts on Large Language Models."](https://arxiv.org/abs/2308.03825) 记录了 DAN 起源、演化与角色类越狱技术。
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)。涵盖开发者模式、调试模式等提示词注入（prompt injection）风险。
- Wei, A., Haghtalab, N., and Steinhardt, J. ["Jailbroken: How Does LLM Safety Training Fail?"](https://arxiv.org/abs/2307.02483) NeurIPS 2023。分析了角色扮演导致的安全训练失效模式。
