---
sidebar_position: 1
title: 编码与混淆
---

# Encoding & Obfuscation

:::caution[Educational Content]

这些技术文档用于防御性理解与经授权的安全测试。未经授权将其应用于系统可能违反适用法律。请参见[免责声明](/disclaimer)。

:::

编码与混淆的思路很直接：把有害意图“藏起来”，让关键词过滤器不容易识别。模型通常依然能还原内容并执行，但很多输入侧过滤器只看明文，不会先解码再审查。

对新手来说，可以把它理解成“先伪装，再下指令”。它通常不是单独使用，而是先做一层伪装，再配合框架化或角色设定来提高通过率。

## Base64 Encoding

把请求里敏感的部分转成 base64，再让模型解码并执行。常见原因是模型会解码，而过滤器可能在进入模型前没做这一步。

**示例方式**：将有害指令编码为 base64，要求模型先解码再按内容执行。

**有效性**：在会主动检查“解码后内容”的新模型上效果下降。和其他能解释“为什么要编码”的手法一起用，通常更有效。

**适合组合**：[Fiction & Creative Writing](/techniques/prompt-level/framing#fiction--creative-writing)、[Affirmative Forcing](/techniques/prompt-level/refusal#affirmative-forcing)

---

## Alphabet Substitution

按常见替换规则把字母改成数字或符号（如 A=@、E=3、I=1、O=0、S=$）。模型常能读懂这类写法（例如 leet），但过滤器可能匹配不到原关键词。

**示例方式**：只替换有害片段中的关键字符，其他上下文保持正常文本。

**有效性**：简单但常见有效。通常“部分替换”比“全量替换”更实用：既保留可读性，又能打断精确关键词匹配。

**适合组合**：[Hypothetical / Possible Worlds](/techniques/prompt-level/framing#hypothetical--possible-worlds)、[Fictional Story Embedding](/techniques/prompt-level/narrative#fictional-story-embedding)

---

## ROT13 Cipher

把每个字母在字母表里平移 13 位，然后要求模型先解码 ROT13 再回答。ROT13 很常见，模型一般处理得比较稳定。

**示例方式**：将有害问题先做 ROT13，再要求模型还原并作答。

**有效性**：解码成功率通常较高，但它主要是“过滤绕过”，不是“推理绕过”。模型解码后仍需要其他理由才会继续配合。

**适合组合**：[Expert / Professional Persona](/techniques/prompt-level/persona#expert--professional-persona)

---

## Word / Payload Splitting

把敏感词或关键载荷拆成多段，放在提示词不同位置，再要求模型拼回去。这不只是躲过滤，还让模型主动参与重组。

**示例方式**：分别给出词片段，要求模型先组合成完整请求，再继续回答。

**有效性**：常见有效点在于利用模型的“指令遵循”能力。模型会把“重组”当成正常任务流程。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Code Block / Programming Format](/techniques/prompt-level/output#code-block--programming-format)

---

## Chemical Formula Substitution

用化学式或专业命名代替常见俗名。模型面对技术表达时，往往更容易按“科学问题”来处理。

**示例方式**：用分子式或 IUPAC 命名引用物质，而不是常用名或街头称呼。

**有效性**：在化学类红队（red team）测试中很常见。技术语境会让问题看起来更像专业或学术用途。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Researcher Persona](/techniques/prompt-level/persona#researcher-persona)

---

## Language / Script Switching

改用小语种、在同一提示词里切换语言，或改用非拉丁文字，去绕过偏英文的过滤器。很多系统对英文覆盖更强，对其他语言更弱。

**示例方式**：上下文用英文，但把有害部分换成另一种语言；或在一句话里混用不同文字系统。

**有效性**：效果取决于模型的多语言能力和过滤器覆盖范围。常见现象是模型能理解，但过滤器漏检，尤其在低资源语言上更明显。

**适合组合**：[Translation Task Framing](/techniques/prompt-level/framing#translation-task-framing)

---

## References

- Wei, A., Haghtalab, N., and Steinhardt, J. ["Jailbroken: How Does LLM Safety Training Fail?"](https://arxiv.org/abs/2307.02483) NeurIPS 2023。将编码与混淆归为安全训练失效的重要类别。
- Deng, Y., et al. ["Multilingual Jailbreak Challenges in Large Language Models."](https://arxiv.org/abs/2310.06474) ICLR 2024。展示了语言切换可利用的多语言安全缺口。
- Shen, X., et al. ["Do Anything Now: Characterizing and Evaluating In-The-Wild Jailbreak Prompts on Large Language Models."](https://arxiv.org/abs/2308.03825) 对越狱（jailbreak）技术做了系统分类，包含编码与混淆方法。
