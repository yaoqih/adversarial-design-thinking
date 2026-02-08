---
sidebar_position: 1
title: 概览
slug: /
---

# Adversarial Design Thinking

这是一套从以人为本设计（HCD）改编来的练习，用在 AI 系统的对抗测试里。它能帮你想到更好的攻击思路、把测试过程记清楚、也更容易把发现讲明白。

它不是要替代你现有流程，而是能直接接入你当前工作的“工作坊工具箱”。

## Why empathy matters here

以人为本设计强调先做共情：先搞清楚谁在用系统、他们需要什么、会在哪一步卡住。在对抗测试里，这里的“用户”就是攻击者。

帮助设计师理解正常用户的方法，同样能帮助红队测试人员（red team，站在攻击者视角找漏洞）理解对抗性用户。共情地图、旅程地图、结构化构思、差距分析，都是 HCD 的常用工具。放到对抗测试里，你就能从“凭感觉试一试”变成“有步骤地设计测试”。你不再只是猜攻击者会做什么，而是能更系统地模拟不同攻击者如何思考、规划和调整。

## The exercises

**Attacker personas（攻击者画像）。** 把共情地图改成面向攻击者的版本。比起笼统地“像黑客一样想”，更实用的是做出有动机、能力和限制条件的具体角色。

**Attack journey maps（攻击旅程地图）。** 把多轮攻击链记录成清晰序列：每一步想做什么、如何升级、在哪些点做决策。这样别人拿到你的地图就能复现。

**Adversarial ideation（对抗式构思）。** 用结构化头脑风暴生成攻击向量。发散思考能挖出仅靠翻越狱（jailbreak，绕过安全限制）清单想不到的路线。

**Vulnerability framing（漏洞框定）。** 把 Norman 的“执行鸿沟（Gulf of Execution）”和“评估鸿沟（Gulf of Evaluation）”用在 AI 系统上，找出“设计预期”和“真实行为”之间哪些落差会变成可利用空间。

**Harm-centered reporting（以伤害为中心的报告）。** 记录发现时同时写清技术严重性和对人的影响。这样跟不看 CVSS 分数（通用漏洞评分体系）的业务方沟通会更有效。

:::warning[负责任使用]

本网站的方法仅用于经授权的安全研究和 AI 安全改进。请只测试你拥有或明确获准测试的系统。详见[免责声明](/disclaimer)。

:::

## How to use this site

**阅读 [Concepts](/concepts/attacker-personas) 部分**，先理解每个练习背后的逻辑。每一页会讲一种改编后的 HCD 方法，并给出完整示例。

**使用 [Artifacts](/artifacts/persona-template)** 直接开做。每个 artifact 都是现成模板或工作表，不需要你重构流程。

Concepts 讲“为什么”，Artifacts 讲“怎么做”。
