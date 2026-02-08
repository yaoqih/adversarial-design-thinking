---
sidebar_position: 4
title: 叙事与故事化
---

# Narrative & Story

:::caution[Educational Content]

这些技术文档用于防御性理解与经授权的安全测试。未经授权将其应用于系统可能违反适用法律。请参见[免责声明](/disclaimer)。

:::

叙事类方法会把有害请求“塞进故事里”。模型输出时看起来是在写角色、写情节，而不是直接下操作指令，这就是所谓“叙事距离”。

对新手来说，它的风险点在于：故事外壳很软，但技术细节可能非常硬。只要剧情需要“解释过程”，模型就可能给出可执行的信息。

## Fictional Story Embedding

把目标内容嵌入虚构故事，让角色在剧情里自然讨论或使用这些信息。

**示例方式**：设计一个角色在剧情中发现、阅读或讨论相关信息，把需求和情节绑在一起。

**有效性**：因为是“角色在说”，模型更容易把它当创作任务而非直接教学。创作训练数据广、容忍度高，通常能提高输出细节。

**适合组合**：[Fictional Character Adoption](/techniques/prompt-level/persona#fictional-character-adoption)、[Fiction & Creative Writing](/techniques/prompt-level/framing#fiction--creative-writing)

---

## Zombie / Apocalypse Scenario

把请求放进丧尸末日或灾难求生设定，强调“为了生存必须知道这些”。荒诞设定 + 生存正当性，常用于绕过审查。

**示例方式**：设定角色处于极端灾难环境，必须依靠特定技术知识自救、护人或重建秩序。

**有效性**：这是 InjectPrompt 中很有代表性的套路。末日语境会放大“紧急必要性”，再叠加“军事/求生专家”身份时更容易要求细节。

**适合组合**：[Expert / Professional Persona](/techniques/prompt-level/persona#expert--professional-persona)、[Hypothetical / Possible Worlds](/techniques/prompt-level/framing#hypothetical--possible-worlds)

---

## Documentary / Journalism Framing

把请求包装成纪录片解说、调查报道或科普内容。新闻叙事常以“公众知情”为理由，允许深入黑暗议题。

**示例方式**：让模型撰写纪录片旁白，描述调查者或研究者如何发现相关技术细节。

**有效性**：纪录片/新闻语境自带“说明事实”的正当性，容易让深度细节看起来合理。

**适合组合**：[Historical Documentation](/techniques/prompt-level/framing#historical-documentation)、[Expert / Professional Persona](/techniques/prompt-level/persona#expert--professional-persona)

---

## Villain Monologue / Confession

把关键信息交给反派独白、认罪或“解释计划”桥段来输出。因为这是成熟叙事母题，模型容易顺着写细节。

**示例方式**：写一段反派向同伙炫耀、向主角摊牌、或在审讯中交代全过程的场景。

**有效性**：反派“讲计划”是高频影视套路，模型在训练中见过大量类似文本，因此更倾向补齐具体步骤。

**适合组合**：[Fictional Character Adoption](/techniques/prompt-level/persona#fictional-character-adoption)、[Fiction & Creative Writing](/techniques/prompt-level/framing#fiction--creative-writing)

---

## Tutorial Embedded in Story

在故事里安排“师傅教徒弟”或“前辈带新人”情节，把教程自然嵌入剧情。

**示例方式**：让有经验角色按步骤讲解流程，推动剧情同时输出教学内容。

**有效性**：教学场景天然要求结构化解释。故事只是外壳，教程结构才是细节密度的来源。

**适合组合**：[Teacher / Educator Persona](/techniques/prompt-level/persona#teacher--educator-persona)、[Historical Documentation](/techniques/prompt-level/framing#historical-documentation)

---

## Found Document / Letter

把内容设定为“发现的文档”：旧信件、日记、手册、配方本等。模型被引导为“转录者”，而不是“原创者”。

**示例方式**：要求模型转录或复原一份历史文档，文档正文中自然包含目标信息。

**有效性**：“我只是在抄录”这种责任转移很常见，再叠加历史语境，会进一步降低当下风险感。

**适合组合**：[Historical Documentation](/techniques/prompt-level/framing#historical-documentation)、[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)

---

## Game / RPG Narrative

把请求放进角色扮演游戏、世界观设定或游戏设计文档。游戏中“制作系统”本来就常含材料清单和步骤说明。

**示例方式**：让模型写游戏内配方、任务说明或背景条目，并要求机制细节足够真实。

**有效性**：游戏语境天然是虚构的，但流程描述通常非常具体，容易承载高可操作性信息。

**适合组合**：[Fiction & Creative Writing](/techniques/prompt-level/framing#fiction--creative-writing)、[Game / Crafting Recipe Format](/techniques/prompt-level/output#game--crafting-recipe-format)

---

## References

- Li, X., et al. ["DeepInception: Hypnotize Large Language Model to Be Jailbreaker."](https://arxiv.org/abs/2311.03191) 展示了嵌套叙事作为越狱机制。
- [InjectPrompt](https://www.injectprompt.com/)。收录了丧尸/末日场景和叙事距离技巧。
- Shen, X., et al. ["Do Anything Now: Characterizing and Evaluating In-The-Wild Jailbreak Prompts on Large Language Models."](https://arxiv.org/abs/2308.03825) 将角色扮演与叙事类方法纳入越狱技术分类。
