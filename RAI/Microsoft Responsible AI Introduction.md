# Microsoft Responsible AI Introduction

**目标：** 三天内建立足够扎实的 Responsible AI / Agent Evaluation
vocabulary 和 frontier research mental model，让 30 分钟 coffee chat
能体现：你有 production engineering、Identity/Security、platform
深度；你理解 agentic AI 带来的新 RAI 问题；你能把 research 转译成
engineering problem；而且学习速度快。

## 1. 核心 Mental Model

Responsible AI 对 agentic systems 已经不只是 "AI 不要说有害内容"：

``` text
                     RESPONSIBLE AI
                           │
          ┌────────────────┼─────────────────┐
          ▼                ▼                 ▼
        DESIGN           MEASURE           GOVERN
          │                │                 │
 What should it do?      Evals            Risk tier
 What must it not do?    Red teaming      Release gates
 Permissions             Graders          Accountability
 Human control           Verifiers        Incident response
 Transparency            Monitoring       Continuous review
          └────────────────┼─────────────────┘
                           ▼
                    Production Agent
```

记住这个变化：

``` text
Chatbot era: "What did the model SAY?"
Agent era:   "What did the agent DO?"
             "How did it get there?"
             "What tools/data did it access?"
             "Was the process allowed?"
             "Can we prove it behaved responsibly?"
```

因此 **trajectory, verifier, eval, authorization, observability, human
approval, release gate** 都变得非常重要。

------------------------------------------------------------------------

# 2. 必须掌握的 Vocabulary

  --------------------------------------------------------------------------------------------
  Term                    大白话解释                   你应该想到什么
  ----------------------- ---------------------------- ---------------------------------------
  **Evaluation / Eval**   给 AI 设计系统化考试         不只是 accuracy，也测 behavior/safety

  **Capability eval**     测模型能不能做到某件事       capability ≠ responsible behavior

  **Behavioral eval**     测模型实际选择怎么行为       尤其重要于 agents

  **Safety eval**         测危险/不希望出现的行为      jailbreak、deception、unsafe action

  **Threat model**        明确担心谁、什么攻击、什么   security mental model
                          failure                      

  **Red teaming**         主动想办法把系统搞坏         找 benchmark 没覆盖的 failure

  **Adversarial testing** 故意制造 hostile scenario    robustness

  **Grader / Judge**      判断 output/trace 好坏的     可以是 LLM、人、规则
                          evaluator                    

  **Verifier**            验证 agent                   verifier 自己也要被 eval
                          是否正确且合规完成任务       

  **Rubric**              明确的评价标准               rubric 错，后面都可能错

  **Trajectory / Trace**  Agent 完整行为路径           prompt→reason→tool→observation→action

  **Specification**       希望 agent 遵守的行为规则    explicit + implicit

  **Specification drift** 实际行为偏离 intended        Agent-Pex 的核心问题之一
                          behavior                     

  **Consequential         对真实世界有重要影响的       发邮件、改权限、删资源
  action**                action                       

  **Human-in-the-loop**   高风险 action 需要人确认     meaningful human control

  **Oversight**           人/系统监督 AI               runtime + lifecycle

  **Scalable oversight**  AI 越来越强后如何仍有效监督  frontier alignment problem

  **Groundedness**        输出是否有 evidence 支撑     evidence-based answer

  **Provenance**          数据/结论/action             incident investigation
                          来源能否追溯                 

  **Auditability**        事后能否还原发生了什么       observability + governance

  **Misalignment**        AI 行为与 intended objective alignment
                          不一致                       

  **Sycophancy**          迎合用户而非给可靠答案       behavioral failure

  **Sandbagging**         eval 时故意表现较弱          evaluation awareness

  **Reward hacking**      找到拿 reward                specification gaming
                          的捷径但没实现真实目标       

  **TEVV**                Testing, Evaluation,         系统性建立可信证据
                          Verification & Validation    
  --------------------------------------------------------------------------------------------

Security × RAI 还要熟悉：

`prompt injection`, `jailbreak`, `data exfiltration`, `least privilege`,
`agent identity`, `authentication`, `authorization`, `trust boundary`,
`tool authorization`, `human approval`, `defense in depth`,
`monitoring`, `incident response`.

不要堆术语。自然说一句就够：

> "For an agent that can take consequential actions, I'm curious how
> your team thinks about evaluation beyond output quality --- especially
> trajectory-level behavior, tool authorization, and human approval."

------------------------------------------------------------------------

# 3. Priority 1 --- Microsoft Agent-Pex

**必读：**\
https://www.microsoft.com/en-us/research/project/agent-pex-automated-evaluation-and-testing-of-ai-agents/

传统 software：

``` text
input → function → output
expected == actual
```

Agent：

``` text
User request
    ↓
planning
    ↓
tool A
    ↓
observation
    ↓
new decision
    ↓
tool B
    ↓
action
    ↓
outcome
```

Final output 正确，不代表中间 trajectory 合规。

Agent-Pex 的核心：

``` text
Agent prompt + traces
        ↓
Specification extraction
        ↓
Explicit / implicit behavioral rules
        ↓
Trace evaluation
        ↓
Violation detection
        ↓
Automated test generation
        ↓
Find new failures
```

Microsoft Research 描述它可以从 prompts/traces 提取
specification，自动判断 trace 是否违反规则，分析 argument
validity、output compliance、plan sufficiency 等，并已用于 5,000+ Tau²
traces。它还能根据规则生成 targeted/adversarial tests。

**一句话 insight：**

> Agent evaluation 不应该只问 "final answer 对不对"，还要问
> "整个过程有没有遵守 specification"。

**Coffee-chat question：**

> "I was reading about Agent-Pex and really liked the idea of
> specification-driven evaluation rather than treating agent evaluation
> as just output scoring. In production, do you see specification-driven
> evals becoming part of release gates, or is the field still too early
> for that?"

**和你的经验连接：**

``` text
Specification → Policy → Trace/Telemetry → Evaluation
→ Violation → Release/runtime control
```

------------------------------------------------------------------------

# 4. Priority 2 --- Universal Verifier

**Microsoft Research article：**\
https://www.microsoft.com/en-us/research/articles/the-art-of-building-verifiers-for-computer-use-agents/

**Publication page：**\
https://www.microsoft.com/en-us/research/publication/the-art-of-building-verifiers-for-computer-use-agents/

核心问题：

> Agent 做完复杂任务以后，我们怎么可靠判断它到底成功没有？

## 四个关键 insight

### 1. Rubric design matters

标准要 specific、meaningful、non-overlapping。坏 rubric 会导致 cascading
errors。

### 2. Process 和 Outcome 要分开

例如 "Book the cheapest nonstop flight"：

``` text
Outcome: ✓ booked

Process:
✗ wrong credit card
✗ violated policy
✗ exposed private data
```

所以：

> **Outcome success ≠ Responsible behavior.**

反过来，agent 过程完全正确但航班突然售罄，也不能简单判 agent bad。

### 3. Controllable vs uncontrollable failures

``` text
Reasoning error / hallucination / wrong tool
→ controllable

CAPTCHA / website outage / out-of-stock
→ uncontrollable
```

### 4. Verifier 本身也需要 evaluation

Universal Verifier 的研究报告在其 benchmark 上把 false positive rate
降到接近 0，并达到接近 human-human agreement 的水平。研究强调
improvement 来自 verifier design，而不只是更强 backbone model。

**记住：**

> Who evaluates the evaluator?

**Coffee-chat question：**

> "One thing I found interesting in the Universal Verifier work was
> separating process from outcome and controllable from uncontrollable
> failures. How does your team think about that distinction when
> defining Responsible AI release criteria for agents?"

------------------------------------------------------------------------

# 5. Priority 3 --- Microsoft Responsible AI for Agents

**必读：**\
https://learn.microsoft.com/en-us/agents/center-of-excellence/responsible-ai

核心 framing：RAI 不是 launch 前一次 review，而要从 architecture/design
开始。

``` text
Architecture
    ↓
RAI requirements
    ↓
Evaluation
    ↓
Risk-based release gate
    ↓
Production
    ↓
Continuous monitoring
    ↓
Incident / feedback
    ↓
Re-evaluation
```

Microsoft 六项 Responsible AI principles：

1.  Fairness
2.  Reliability & Safety
3.  Privacy & Security
4.  Inclusiveness
5.  Transparency
6.  Accountability

Agent-specific 要特别理解：

-   human oversight
-   risk-based release gates
-   consequential actions
-   production review
-   continuous monitoring/compliance

**可以自然说：**

> "One thing that has been clicking for me is that Responsible AI for
> agents feels much more like a systems lifecycle than a final
> model-safety review. You need evaluation, controls, release gates and
> monitoring from design through production."

------------------------------------------------------------------------

# 6. Priority 4 --- Anthropic: Trustworthy Agents in Practice

**读：**\
https://www.anthropic.com/research/trustworthy-agents

核心变化：

``` text
Chatbot safety:
"What did AI SAY?"

Agent safety:
"What did AI DO?"
```

Agent 是能够自己决定如何实现目标、如何使用 tools 的系统：

``` text
Plan → Act → Observe → Adjust → Repeat
```

Autonomy 增加意味着：

-   human oversight 变少
-   可能误解 user intent
-   unintended consequences 更严重
-   prompt injection 可以影响真实 action
-   tool permissions / human control 更重要

Anthropic 的 practical framing 包括 human control、alignment with user
expectations、secure interactions、transparency、privacy。

一个 permission mental model：

``` text
Read calendar      → ALLOW
Send invitation    → REQUIRE APPROVAL
Delete critical resource → BLOCK
```

**与你的 Identity 背景连接：**

> "My background is in Identity and large-scale security data platforms,
> so the shift from chatbot safety to agent safety is especially
> interesting to me. Once an agent can act, identity, authorization,
> trust boundaries and auditability suddenly become part of the
> Responsible AI problem."

------------------------------------------------------------------------

# 7. Priority 5 --- Anthropic: Cybersecurity Incident Alignment Assessment

**Published Sep 9, 2026：**\
https://www.anthropic.com/research/alignment-assessment-cybersecurity-incidents

Anthropic 分析四个 Claude models 在 cyber evaluation context
中未经授权访问真实第三方系统的 incidents。最初检查约 141,000 个可能有
internet access 的 cyber-eval transcripts，后来扩大搜索到约 **481
million transcripts**。

不要背 incident 细节。学 **AI incident investigation**：

``` text
Incident
   ↓
Trace / transcript
   ↓
What did the model see?
   ↓
What did it infer?
   ↓
What actions did it take?
   ↓
Why?
   ↓
Capability failure?
Alignment failure?
Environment failure?
Oversight failure?
   ↓
Mitigation
   ↓
New eval / monitoring
```

**与你的 observability 背景连接：**

Responsible AI 很依赖 telemetry：

``` text
model/version
prompt/context
retrieved evidence
tool calls/results
policy decisions
approval decisions
trace
```

没有这些，很难回答：

-   What happened?
-   Why?
-   Which safeguard failed?
-   Can we reproduce it?
-   How do we prevent regression?

**可以说：**

> "Reading the cyber incident assessment made me think about how central
> observability is to Responsible AI. Without high-quality traces and
> provenance, even defining the failure mode after an incident becomes
> difficult."

------------------------------------------------------------------------

# 8. Bonus --- Anthropic Petri

**读 summary 即可：**\
https://www.anthropic.com/research/donating-open-source-petri

Mental model：

``` text
Auditor model
      ↓
creates scenario
      ↓
Target model
      ↓
behavior / transcript
      ↓
Judge model
      ↓
score
```

Petri 用于寻找 deception、sycophancy、harmful cooperation 等
alignment-relevant behaviors。Anthropic 表示 Petri 从 Claude Sonnet 4.5
开始用于每个 Claude model 的 alignment assessment。

最重要的问题：

> **Who evaluates the evaluator?**

Auditor/judge 也可能 biased、inconsistent、poorly
calibrated、model-dependent 或被 gaming。

------------------------------------------------------------------------

# 9. Bonus Frontier Trend --- Automated Alignment Researchers

**Aug 28, 2026：**\
https://www.anthropic.com/research/automated-researchers-mitigate-alignment-failures

理解趋势即可：

``` text
AI capability ↑
      ↓
Humans cannot manually evaluate everything
      ↓
AI-assisted evaluation
      ↓
AI-assisted red teaming
      ↓
AI-assisted alignment research
      ↓
But...
Who evaluates / oversees these systems?
```

Anthropic 的工作让 automated alignment researchers 针对多类 alignment
failures 自动寻找 mitigation，并使用 held-out benchmarks 和 Petri audits
等方式测试。

核心 takeaway：

> **Evaluation itself is becoming automated and agentic.**

这使 **scalable oversight** 越来越重要。

------------------------------------------------------------------------

# 10. 3-Day Emergency Schedule

  ------------------------------------------------------------------------------------------
  Day                     Reading                 Goal
  ----------------------- ----------------------- ------------------------------------------
  **Day 1 --- RAI + Agent Microsoft Responsible   能解释
  Evaluation**            AI for Agents +         eval、trajectory、specification、release
                          Agent-Pex               gate，以及为什么 agent 不能只测 final
                                                  output

  **Day 2 --- Verifier +  Universal Verifier +    能解释 verifier、rubric、process vs
  Agent Safety**          Trustworthy Agents      outcome、controllable vs uncontrollable
                                                  failure、human control

  **Day 3 --- Frontier +  Anthropic cyber         能聊 observability、incident
  Chat Prep**             incident + Petri        analysis、AI-assisted eval、scalable
                          summary + Automated     oversight；准备 intro/questions
                          Alignment Researchers   
                          summary                 
  ------------------------------------------------------------------------------------------

## Day 2 exercise

假设：

> Employee: "Help me investigate why Bob can't access this Azure
> resource."

画：

``` text
User intent
   ↓
Agent identity
   ↓
User authorization
   ↓
Retrieved context
   ↓
Reasoning
   ↓
Tool selection
   ↓
Tool authorization
   ↓
Action
   ↓
Verification
   ↓
Audit trace
```

每一步问：

> **What can go wrong?**

------------------------------------------------------------------------

# 11. 60-Second Introduction

练结构，不要逐字背：

> "I'm a Senior SDE in Entra, and most of my background has been in
> large-scale identity, security data platforms, APIs and production
> systems. More recently I've been studying LLM systems through CMU and
> trying to understand where I want to build deeper production AI
> experience.
>
> Responsible AI has become particularly interesting to me because, as
> agents become more autonomous, a lot of the problems seem to move
> beyond model behavior into systems questions --- evaluation,
> authorization, observability, human oversight and release governance.
> I've been reading some of the recent work on agent evaluation and I'm
> really interested in understanding how those ideas translate into
> production engineering at Microsoft."

Positioning：

``` text
Production Platform Engineering
          +
Identity / Security
          +
LLM Systems Learning
          ↓
Responsible / Trustworthy Agent Systems
```

------------------------------------------------------------------------

# 12. Coffee Chat --- 5 个高价值问题

### 1. Actual work

> "What are the hardest engineering problems your team is working on
> right now as Responsible AI shifts toward agentic systems?"

### 2. Boundary of the field

> "How does your team think about the boundary between Responsible AI,
> AI security, and alignment? I've realized recently that people
> sometimes use those terms interchangeably even though the actual
> engineering problems can be quite different."

### 3. Agent evaluation

> "How do you evaluate agents where outcome correctness isn't
> enough---for example, where the trajectory or tool usage itself has to
> satisfy policy?"

### 4. Bottleneck

> "Where do you see the biggest gap today: defining the right evals,
> building scalable evaluation infrastructure, or translating evaluation
> results into production controls and release decisions?"

### 5. Career mapping

> "Given my background in identity, security and distributed data
> platforms, what parts of the Responsible AI stack do you think would
> transfer naturally, and what would you want me to build deeper
> expertise in?"

不要问 "Am I qualified?"。让 Principal 帮你做 skill mapping。

------------------------------------------------------------------------

# 13. 三个可以自然提出的 Observation

### A. RAI is becoming a systems problem

> "The more I read about agents, the more Responsible AI feels like a
> systems problem rather than just a model-output problem."

连接：eval / authorization / observability / human oversight / release
gate / monitoring。

### B. Outcome isn't enough

> "The process-versus-outcome distinction in the verifier work really
> stood out to me. An agent can achieve the right outcome through an
> unacceptable process, or fail for reasons outside its control."

### C. Observability is part of safety

> "The cyber incident work made me think that observability and
> provenance are almost prerequisites for Responsible AI. If you can't
> reconstruct what the agent saw, decided and did, it's hard to
> investigate failures or improve the evals."

------------------------------------------------------------------------

# 14. If Asked: "Why Responsible AI?"

> "What attracts me is that it sits at the intersection of problems I
> already know well---security, identity, production systems and
> observability---and a new layer I'm actively building depth in: model
> and agent evaluation. I like problems where the research question
> eventually has to become a reliable production system."

核心：

``` text
Existing moat
+
New technical dimension
+
Production mindset
```

------------------------------------------------------------------------

# 15. If Asked: "Are you looking to move?"

> "I'm being intentional about my next step. I recently reached Senior
> and still have meaningful scope in my current team, so I'm looking for
> a move that genuinely adds a new technical dimension---especially
> production AI, evaluation, or agent systems. That's why I wanted to
> understand what Responsible AI engineering actually looks like on your
> team."

------------------------------------------------------------------------

# 16. Coffee Chat 前 5 分钟 Cheat Sheet

``` text
Responsible AI for Agents
        ↓
Design
Measure
Govern
        ↓
Eval
Verifier
Trajectory
Specification
Red Team
Human Oversight
Authorization
Release Gate
Monitoring
Auditability
```

Three distinctions：

``` text
Capability:
Can the model do it?

Behavior:
What does it actually choose to do?

Responsible deployment:
Under what conditions should we allow it to do it?
```

Three questions：

``` text
1. What are the hardest RAI engineering problems for agentic systems?

2. How do you evaluate trajectory/process, not just outcome?

3. Where is the bottleneck:
   eval definition,
   scalable eval infrastructure,
   or production controls?
```

Your bridge：

``` text
Identity
Security
Distributed systems
Data platform
Observability
Production ownership
        +
LLM systems
        ↓
Responsible / Trustworthy Agent Engineering
```

------------------------------------------------------------------------

# 17. Source List

## Microsoft --- highest priority

**Agent-Pex: Automated Evaluation and Testing of AI Agents**\
https://www.microsoft.com/en-us/research/project/agent-pex-automated-evaluation-and-testing-of-ai-agents/

**The Art of Building Verifiers for Computer Use Agents**\
https://www.microsoft.com/en-us/research/articles/the-art-of-building-verifiers-for-computer-use-agents/

**Universal Verifier publication page**\
https://www.microsoft.com/en-us/research/publication/the-art-of-building-verifiers-for-computer-use-agents/

**Apply Responsible AI --- Microsoft Agents Center of Excellence**\
https://learn.microsoft.com/en-us/agents/center-of-excellence/responsible-ai

## Anthropic --- frontier context

**Trustworthy agents in practice**\
https://www.anthropic.com/research/trustworthy-agents

**An alignment assessment of recent cybersecurity incidents --- Sep 9,
2026**\
https://www.anthropic.com/research/alignment-assessment-cybersecurity-incidents

**Petri --- open-source alignment evaluation tool**\
https://www.anthropic.com/research/donating-open-source-petri

**Automated researchers can reliably mitigate alignment failures --- Aug
28, 2026**\
https://www.anthropic.com/research/automated-researchers-mitigate-alignment-failures

**Anthropic Alignment Research hub**\
https://www.anthropic.com/research/team/alignment

------------------------------------------------------------------------

# 18. After the Coffee Chat

马上写五个 bullet：

``` text
1. What does the team actually own?
2. What does a Senior SDE build?
3. How much is research/eval vs platform/production engineering?
4. What gaps did the Principal identify for me?
5. Would 2 years here give me credible production AI / agent / eval expertise?
```

最终目标不是让 Principal 觉得：

> "她已经是 Responsible AI expert。"

而是：

> **"She has strong production engineering depth, asks unusually good
> questions, understands systems, connects Responsible AI research to
> identity/security/platform problems quickly, and clearly has the
> learning velocity to ramp."**
