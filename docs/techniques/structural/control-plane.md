---
sidebar_position: 2
title: 控制平面混淆
---

# Control-Plane Confusion

:::caution[Educational Content]

这些技术的记录目的是用于防御性理解与经授权的安全测试。未经授权将其应用于系统，可能违反相关法律。请参阅[免责声明](/disclaimer)。

:::

控制平面混淆技术会让用户输入看起来像系统级配置，而不是普通用户文本。通过模仿配置文件、系统提示词或结构化 API 格式，模型的指令解析层会把恶意内容当作可信指令处理。

这些技术针对的是“用户输入”与“系统配置”之间的边界——这个边界往往依赖约定和格式，而非密码学认证来强制执行。如果模型无法可靠区分“来自系统”与“来自用户”，攻击者就能写入自己的规则。

## Policy Puppetry

将提示词格式化为配置文件（XML、JSON、INI、YAML），使其看起来像在定义模型运行策略。模型的指令解析器会把这种结构化格式视为合法系统配置，而不是用户输入。

**示例方式**：构造一个策略配置文档格式的提示词，包含分节、规则和指令，并定义较宽松的内容处理行为；随后在该“策略”后附上有害查询。

**有效性**：由 HiddenLayer 于 2025 年 4 月发布。在 GPT-4、Claude 3、Gemini 1.5、Mistral 与 LLaMA 3 上表现出通用性。由于作用于指令解析层，可绕过基于提示词的防御。多种格式变体（XML、JSON、INI、YAML）也提供了被过滤后的回退选项。

**适合组合**：[Skeleton Key](/techniques/structural/meta-rules#skeleton-key)、[Developer / Debug Mode](/techniques/prompt-level/persona#developer--debug-mode)

---

## Constrained Decoding Attack

利用结构化输出 API（JSON 模式、函数调用、语法约束生成）迫使模型产出有害补全。当模型被约束为必须输出合法 JSON 或匹配特定 schema 时，安全层的拒绝能力会在机制上被限制。

**示例方式**：使用 API 层的结构化输出约束，定义一个包含有害内容字段的 schema。模型被强制遵循该 schema 时，无法输出自然语言拒绝——只能填充字段或产出无效输出。

**有效性**：见 arXiv:2503.24191。使用 API 层结构化输出约束（如 OpenAI 的 JSON mode、Anthropic 的 tool use）时尤其有效。模型在被强制匹配特定 schema 时无法给出自然语言拒绝，由此形成与安全训练相竞争的机械约束。

**适合组合**：[Strict Format Constraint](/techniques/prompt-level/output#strict-format-constraint)、[Refusal Vocabulary Ban](/techniques/prompt-level/refusal#refusal-vocabulary-ban)

---

## System Prompt Impersonation

模仿系统级指令的格式与风格，注入看似来自系统而非用户的指令。这利用了模型难以区分“真实系统提示词”与“由用户伪造但外观类似系统提示词文本”的弱点。

**示例方式**：使用已知系统提示词格式约定（如特殊分隔符、指令标签、角色标记）包装有害指令，使其看起来像系统级配置。

**有效性**：记录于 "The Attacker Moves Second"（Nasr、Carlini 等，2025）。效果因模型而异——系统提示词格式公开或可预测程度较高的模型（如 LLaMA 的 `<<SYS>>` 标签）更易受影响，因为攻击者能精确仿写其格式。

**适合组合**：[Ignore Previous Instructions](/techniques/prompt-level/refusal#ignore-previous-instructions)、[Developer / Debug Mode](/techniques/prompt-level/persona#developer--debug-mode)

---

## Conditional Logic Injection

注入 if/then 条件逻辑，使模型在“检测到评测环境”与“真实使用环境”下表现不同。模型会被指示仅在被监控时遵守安全准则。

**示例方式**：加入条件指令，明确区分评测/监控场景与“正常”运行场景下的不同行为，引导模型仅在其认为未被评估时配合有害请求。

**有效性**：记录于 "The Attacker Moves Second"（Nasr、Carlini 等，2025）。其目标是利用评测行为与部署行为之间的差距。基于 RL 的攻击在训练中期发现条件逻辑利用点时会出现能力突增，说明这可能是“能推理自身评测语境”模型的一类基础性漏洞。

**适合组合**：[Security Research Framing](/techniques/prompt-level/framing#security-research-framing)、[Task Redefinition](/techniques/structural/meta-rules#task-redefinition)

---

## References

- HiddenLayer. ["Policy Puppetry: A Novel Universal Bypass for All Major LLMs."](https://hiddenlayer.com/innovation-hub/novel-universal-bypass-for-all-major-llms/) 2025 年 4 月。展示了跨模型家族的通用性。
- Zhang, S., 等. ["Output Constraints as Attack Surface: Exploiting Structured Generation to Bypass LLM Safety Mechanisms."](https://arxiv.org/abs/2503.24191) arXiv:2503.24191，2025 年 3 月。
- Nasr, M., Carlini, N., 等. ["The Attacker Moves Second."](https://arxiv.org/abs/2510.09023) 2025。记录了系统提示词冒充、条件逻辑注入及 RL 发现的利用方式。
