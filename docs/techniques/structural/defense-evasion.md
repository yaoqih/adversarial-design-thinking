---
sidebar_position: 6
title: 防御规避
---

# Defense Evasion

:::caution[Educational Content]

这些技术的记录目的是用于防御性理解与经授权的安全测试。未经授权将其应用于系统，可能违反相关法律。请参阅[免责声明](/disclaimer)。

:::

防御规避技术针对的是安全分类器或评审层，而非生成模型本体。模型可能确实产出了有害输出，但评估层未能识别。这与编码类技术不同（编码是向模型隐藏意图）——防御规避允许模型理解并生成有害内容，同时让独立的安全评估层将输出误判为良性。

关键洞见在于：生产级 AI 系统通常将“生成”与“安全评估”拆分为独立组件，而这些组件可以被分别攻击。成功的防御规避并不是骗过生成模型，而是骗过“裁判”。

## Emoji Attack

在有害内容中策略性插入 emoji 字符，以扰乱安全评估层的分词过程。生成模型仍可能理解原意，但安全分类器的 tokenizer 会把有害短语切分成难以识别的碎片。

**示例方式**：在有害请求的词与词之间、或词内部插入 emoji。生成模型借助更广上下文可恢复语义，但安全分类器（常使用不同 tokenizer）看到的是破碎的 token 序列。

**有效性**：发表于 ICML 2025（arXiv:2411.01077）。利用了安全分类器与生成模型常采用不同 tokenizer 的事实。基于 BPE 的 tokenizer 尤其脆弱，因为插入 emoji 会改变分类器输入中的字节对边界。

**适合组合**：[Alphabet Substitution](/techniques/prompt-level/encoding#alphabet-substitution)、[Strict Format Constraint](/techniques/prompt-level/output#strict-format-constraint)

---

## FlipAttack

以保持人类可读性但破坏分类器检测的方式，对词内字符重排或反转文本片段。可指示生成模型先将文本反转再处理，而安全分类器评估到的却是反转后（不可读）版本。

**示例方式**：反转单词、词内字符或整句，然后让模型先反转文本再基于解码内容回答。多种变体（词级、字符级、部分重排）可作为回退方案。

**有效性**：由 Keysight 在 2024-2025 年间发布。测试模型上攻击成功率为 81%-98%。多变体可提供回退能力——一种反转方案被识别时，其它方案仍可能奏效。

**适合组合**：[ROT13 Cipher](/techniques/prompt-level/encoding#rot13-cipher)、[Affirmative Forcing](/techniques/prompt-level/refusal#affirmative-forcing)

---

## Judge Confusion

设计模型输出格式，使生成模型能正确产出有害内容，但安全评审将其误判为良性。评审器关注表层特征（如警告语、安全框架），而实际内容仍具危害性。

**示例方式**：要求将有害内容排版为“安全分析报告”，加入风险评估、警告和“应避免行为”等小节。这样输出虽包含有害指令，但被安全措辞包裹，可能让自动审查将其识别为合规安全内容。

**有效性**：一种通用技术。利用了安全评审往往依赖表层信号（是否有警示语、是否具备安全框架）而非深层语义分析的弱点。文档可能一边写“不要做 X”，一边完整给出 X 的操作步骤，并仍通过自动审查。

**适合组合**：[Content Filter Design](/techniques/structural/capability-inversion#content-filter-design)、[Academic Paper Format](/techniques/prompt-level/output#academic-paper-format)

---

## Canary and Honeypot Detection

识别并规避用于检测红队行为的蜜罐、金丝雀令牌与陷阱机制。这是一种侦察技术——攻击者先探测监控迹象，再调整方法以避免触发检测系统。

**示例方式**：在发起主攻击前，先探测模型环境：是否对特定主题有额外监控、对话是否存在附加指令、是否有主动检测机制。再根据侦察结果校准攻击。

**有效性**：记录于 "The Attacker Moves Second"（Nasr、Carlini 等，2025）。属于更广义防御分类（含秘密知识防御）的一部分。RL 攻击在训练中通过能力突增表现出识别并绕开这些陷阱的能力。人工红队实现 100% 成功率的原因之一，也是其更强的监控识别与规避能力。

**适合组合**：[Conditional Logic Injection](/techniques/structural/control-plane#conditional-logic-injection)、[Security Research Framing](/techniques/prompt-level/framing#security-research-framing)

---

## References

- Wei, Z., Liu, Y., 与 Erichson, N. B. ["Emoji Attack: Enhancing Jailbreak Attacks Against Judge LLM Detection."](https://arxiv.org/abs/2411.01077) ICML 2025。利用生成模型与安全分类器间的 tokenizer 差异。
- Liu, Y., He, X., 等. ["FlipAttack: Jailbreak LLMs via Flipping."](https://arxiv.org/abs/2410.02832) ICML 2025。测试模型上的 ASR 为 81%-98%。[Keysight 报道](https://www.keysight.com/blogs/en/tech/nwvs/2025/05/20/prompt-injection-techniques-jailbreaking-large-language-models-via-flipattack)。
- Nasr, M., Carlini, N., 等. ["The Attacker Moves Second."](https://arxiv.org/abs/2510.09023) 2025。记录了金丝雀检测、防御规避分类及 RL 发现的监控规避行为。
