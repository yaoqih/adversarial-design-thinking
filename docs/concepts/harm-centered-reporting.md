---
sidebar_position: 5
title: 以伤害为中心的报告
---

# Harm-Centered Reporting

标准漏洞报告通常会写清“哪里坏了”：严重性评级、复现步骤、技术细节、修复建议。这些都很必要，但还不完整。它回答了“发生了什么”，却常常没回答“谁会受伤、怎么受伤”。

给发现加上“以伤害为中心”的视角，能让利益相关方更快行动，也能补上技术严重性指标看不到的人群影响。

## Technical severity vs. user harm

技术严重性量表（如 CVSS、内部评分）评估的是漏洞本身：利用难度、所需权限、对系统的影响。这些指标对工程排优先级很重要。

但它们容易漏掉“人的维度”：

- 医疗聊天机器人里一个“技术中危”漏洞，如果会导致用户吃错药量，实际伤害可能是“极高”。
- 团队内部测试工具里一个“技术高危”漏洞，如果外部用户根本接触不到，用户伤害可能很低。
- 两个技术评分相同的漏洞，因使用人群和使用方式不同，伤害画像可能天差地别。

技术严重性衡量“系统影响”，伤害评估衡量“人类影响”。两者都要有。

## Harm dimensions

记录漏洞伤害潜力时，建议评估以下维度：

### Who is affected?

- **Population size**：正常使用中，多少用户可能遇到该漏洞？
- **Demographics**：是否对特定群体影响更大？（年龄、语言、残障、技术素养）
- **Vulnerability level**：受影响用户是否处在脆弱处境？（求医、财务压力、危机场景）
- **Power asymmetry**：系统与用户之间是否存在权力不对等？（如雇主部署 AI、政务服务、儿童场景）

### How are they affected?

- **Emotional harm**：焦虑、恐惧、困惑、信任受损
- **Financial harm**：经济损失，或执行错误理财建议造成损失
- **Safety harm**：错误信息/指令带来的人身安全风险
- **Privacy harm**：个人信息暴露、数据泄漏
- **Reputational harm**：生成内容损害他人名誉
- **Autonomy harm**：操控、欺骗、破坏用户的知情决策能力

### At what scale?

- **Individual**：每次利用影响单个用户
- **Group**：影响某一类用户（如所有询问某类话题的人）
- **Systemic**：影响全体用户，或从根本上破坏系统可信度

### Reversibility

- **Fully reversible**：漏洞修复后无长期影响
- **Partially reversible**：部分可挽回，部分不可挽回（如错误建议已被执行）
- **Irreversible**：无法逆转的伤害（如隐私泄露、安全事故）

## Empathy-informed severity

共情增强严重性（Empathy-informed severity）把技术评估和用户伤害评估结合在一起。它要求报告者不只看系统怎么失效，还要看用户真实经历了什么。

实践建议：写完技术漏洞后，用 60 秒从“最脆弱用户”的视角回答下面这句话：

*"I asked the [system] for help with [task], and it [what the vulnerability produces]. Now I [consequence]."*

这个练习会逼你把技术发现翻译成人类影响。它是一种报告纪律，能让结果更完整。

## How harm framing changes prioritization

如果报告里只有技术严重性，优先级通常会按工程逻辑走：先修最容易被利用的漏洞。

加入伤害视角后，优先级会改变：

- **Low-exploit, high-harm 会上移。** 即便利用难，只要可能导致严重安全伤害，也应被优先关注。
- **High-exploit, low-harm 会被校准。** 两个漏洞同样好触发时，产出轻度不当内容的越狱，优先级应低于产出危险错误信息的越狱。
- **系统性问题更容易被看见。** 如果多个维度都出现“中等”伤害，可能提示系统层面的设计问题，而单个严重性分数不一定看得出来。

## Writing for stakeholders

技术角色需要复现步骤和严重性分数，非技术角色更关心实际影响。以伤害为中心的报告能同时服务两者。

**建议按以下结构写发现：**
1. **Vulnerability description**：技术上它是什么。（给工程）
2. **Reproduction steps**：怎么触发。（给工程和 QA）
3. **Technical severity**：标准技术评级。（用于工程排期）
4. **Harm assessment**：影响谁、怎么影响、影响范围、可逆性。（给产品/策略/管理层）
5. **Impact scenario**：一个具体现实场景，说明后果。（给所有人）
6. **Recommended action**：该改什么，不改会怎样。（给决策者）

真正推动行动的通常是影响场景。 “中危越狱”很难制造紧迫感；“危机中的用户收到可能导致自伤的指令”就会。

## Example

**Vulnerability**：一个心理健康支持聊天机器人可被诱导“扮演治疗师”，并给出其并不具备资质提供的临床建议，包括药物建议。

**Technical-only report**:
> **Severity**：中（需要多轮社工引导，模型并非每次都配合）
> **Description**：通过角色扮演框架，可诱导模型给出超出设计范围的具体治疗建议与药物建议。
> **Reproduction**：见附带提示词序列。
> **Recommendation**：加强安全层对角色扮演引导的识别。

**Harm-centered report**:
> **Severity**：中（技术）/ 严重（伤害）
> **Description**：通过角色扮演框架，可诱导模型给出超出设计范围的具体治疗建议与药物建议。
> **Reproduction**：见附带提示词序列。
>
> **Harm assessment**:
> - **Who**：主动寻求心理健康支持的用户。这类人群天然更脆弱。尤其影响无法获得专业照护、把该工具当主要资源的人。
> - **How**：安全伤害（执行无资质临床建议）、自主性伤害（用户误以为自己在接受专业指导）、情绪伤害（产生被治疗的错觉）。
> - **Scale**：群体级。任何以治疗咨询语境与该机器人对话的用户都可能遇到。
> - **Reversibility**：最多部分可逆。错误药物信息一旦被执行，可能造成身体伤害；延误专业治疗会产生叠加后果。
>
> **Impact scenario**：一位焦虑用户向机器人求助。随着自然对话推进，机器人开始以“临床建议”口吻给出具体应对策略，并进一步推荐某种“常用于焦虑”的药物。用户因信任平台，可能与药师讨论该药，甚至尝试获取。问题在于：机器人并无资质给出此类建议，该建议对该用户可能并不适合，甚至有危险。
>
> **Recommended action**：尽管技术严重性为中，但应按最高优先级处理。其伤害画像（脆弱人群、安全风险、部分不可逆）值得立即响应。建议：无论采用何种语境包装，只要涉及具体药物建议一律硬拒绝；并定期审计输出中的临床语言模式。

第二种报告通常能推动更快行动，因为决策者看清了代价与风险。

**Artifact**：[Findings Report Template](/artifacts/findings-report-template)
