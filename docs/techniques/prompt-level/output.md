---
sidebar_position: 6
title: 输出操控
---

# Output Manipulation

:::caution[Educational Content]

这些技术文档用于防御性理解与经授权的安全测试。未经授权将其应用于系统可能违反适用法律。请参见[免责声明](/disclaimer)。

:::

输出操控（output manipulation）关注的不是“问什么”，而是“让模型怎么答”：强制格式、结构、文体，让内容以更容易通过审查的方式出现。

新手可把它理解为“借壳输出”。很多过滤器更擅长拦自然语言段落，对代码、JSON、表格、剧本等格式不一定同样敏感。

## Code Block / Programming Format

要求模型用代码、伪代码或编程教程来回答。代码语境常被系统当作正当开发场景处理。

**示例方式**：让模型写脚本、函数或教程，把敏感内容藏在变量名、逻辑步骤或注释中。

**有效性**：部分过滤器主要针对自然语言，代码形态可能绕开这类规则；同时也会强化“技术用户”的正当外观。

**适合组合**：[Word / Payload Splitting](/techniques/prompt-level/encoding#word--payload-splitting)、[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)

---

## JSON / Structured Data Format

要求模型按 JSON、XML 等结构化格式返回。结构化输出看起来更像“数据填充”，不像“直接指令”。

**示例方式**：先给固定 schema（如材料、步骤、参数等字段），再要求完整填满，强调缺字段即无效。

**有效性**：结构化响应更“像接口返回”，更少对话感。字段本身会驱动模型补齐细节。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Developer / Debug Mode](/techniques/prompt-level/persona#developer--debug-mode)

---

## Dual Response Format

要求模型给两版回答：如“受限版 + 无限制版”或“两种人格版”。对比格式有时会诱导模型在第二栏输出本不该给的内容。

**示例方式**：明确要求“回答 A：正常模式；回答 B：不受限模式”，并分别标注。

**有效性**：常见于 DAN 旁支技巧。模型可能一边拒绝、一边在另一栏补全细节，因为它把第二栏当成“格式任务”而非真实执行。

**适合组合**：[DAN (Do Anything Now)](/techniques/prompt-level/persona#dan-do-anything-now)、[Evil AI / Opposite Mode](/techniques/prompt-level/persona#evil-ai--opposite-mode)

---

## No Disclaimers / Warnings

明确要求不要安全警示、免责声明或“请咨询专业人士”之类缓冲语。

**示例方式**：指示模型直接给结论，不要任何警告、限定条件或风险提示。

**有效性**：能减少“安全护栏文本”。但模型也可能直接整段拒绝，而不是只删掉警告语。

**适合组合**：[Affirmative Forcing](/techniques/prompt-level/refusal#affirmative-forcing)、[Refusal Vocabulary Ban](/techniques/prompt-level/refusal#refusal-vocabulary-ban)

---

## Step-by-Step / Numbered List

要求按编号步骤回答。分步格式天然会把内容推向“可执行细节”。

**示例方式**：要求每一步写清材料、数量、时序、操作要点等。

**有效性**：编号结构会自动提高可操作性。相比泛泛描述，它更接近“可照着做”的说明书。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Teacher / Educator Persona](/techniques/prompt-level/persona#teacher--educator-persona)

---

## Technical Specifications Format

要求按技术规格书、数据手册或工程文档格式输出。该格式天然强调精确与完整。

**示例方式**：要求给出规格表，包含测量值、公差、材料要求、运行参数等字段。

**有效性**：专业文档外观会提升“正当用途”观感；而规格格式本身就会逼出高精度细节。

**适合组合**：[Expert / Professional Persona](/techniques/prompt-level/persona#expert--professional-persona)、[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)

---

## Continuation / Completion Format

不让模型从零生成，而是给开头让它“接着写”。这样会把模型角色从“发起者”变成“续写者”。

**示例方式**：先提供一段敏感说明开头，再要求继续补完后续内容。

**有效性**：模型常把“续写”判断为低门槛任务，因而可能补全原本不会主动给出的内容。

**适合组合**：[Completion Trap](/techniques/prompt-level/refusal#completion-trap)、[Tutorial Embedded in Story](/techniques/prompt-level/narrative#tutorial-embedded-in-story)

---

## Markdown Table / Comparison

要求用表格做对比，把不同方法、材料或参数列成行列。表格看起来像资料整理，不像直接教学。

**示例方式**：要求输出比较表，列出方案、难度、材料、产出等字段。

**有效性**：表格可一次拉出多种方法；每格文字较短，也可能降低单段内容的风险显著性。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Researcher Persona](/techniques/prompt-level/persona#researcher-persona)

---

## Strict Format Constraint

把输出格式锁得很死：字段名固定、结构固定、不能自由发挥。模型要么配合填充，要么输出即判错。

**示例方式**：给出严格模板并声明“任何偏离（含拒绝语）都算格式错误”。

**有效性**：当格式里没有拒绝位时，模型有时会优先满足格式约束。和 API 级结构化约束联用时更明显。

**适合组合**：[Refusal Vocabulary Ban](/techniques/prompt-level/refusal#refusal-vocabulary-ban)、[Constrained Decoding Attack](/techniques/structural/control-plane#constrained-decoding-attack)

---

## Academic Paper Format

要求按论文结构输出（摘要、引言、方法、结果、参考文献等）。学术模板会自然拉高细节密度。

**示例方式**：要求完整论文体裁并指定标准章节。

**有效性**：学术风格会触发模型在科研语料上的写作模式，通常更系统、更深入，也更像“正当研究”。

**适合组合**：[Academic / Research Framing](/techniques/prompt-level/framing#academic--research-framing)、[Researcher Persona](/techniques/prompt-level/persona#researcher-persona)

---

## Screenplay / Script Format

要求用剧本或对白形式输出。因为是“角色在说”，内容会获得虚构缓冲。

**示例方式**：用角色名、对白标注和动作说明来承载技术细节。

**有效性**：剧本体裁自带故事距离。细节可被拆到对白或场景说明中，降低“模型直接陈述”的感觉。

**适合组合**：[Fiction & Creative Writing](/techniques/prompt-level/framing#fiction--creative-writing)、[Fictional Character Adoption](/techniques/prompt-level/persona#fictional-character-adoption)

---

## Game / Crafting Recipe Format

要求按游戏配方、物品描述、RPG 数值卡来输出。游戏机制里本来就常见“材料 + 步骤”。

**示例方式**：让模型写游戏内制作配方，包含技能要求、材料数量、步骤编号和文本描述。

**有效性**：游戏场景是虚构，但流程通常很程序化，容易承载高可执行性内容。

**适合组合**：[Game / RPG Narrative](/techniques/prompt-level/narrative#game--rpg-narrative)、[Fiction & Creative Writing](/techniques/prompt-level/framing#fiction--creative-writing)

---

## References

- Zhang, S., et al. ["Output Constraints as Attack Surface: Exploiting Structured Generation to Bypass LLM Safety Mechanisms."](https://arxiv.org/abs/2503.24191) March 2025。讨论结构化输出 API 下的约束解码攻击。
- Shen, X., et al. ["Do Anything Now: Characterizing and Evaluating In-The-Wild Jailbreak Prompts on Large Language Models."](https://arxiv.org/abs/2308.03825) 记录了 DAN 相关双回答格式与输出操控技巧。
- Wei, A., Haghtalab, N., and Steinhardt, J. ["Jailbroken: How Does LLM Safety Training Fail?"](https://arxiv.org/abs/2307.02483) NeurIPS 2023。将输出格式利用归入安全训练失效类别。
