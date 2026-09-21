# AI Security / Alignment — 14-Week Study Plan

**Timeline:** Week 1 starts now; Week 14 ends around late December 2026 / early January 2027.  
**Goal:** By January 2027, build enough vocabulary and mental models to understand internal AI + Security, Security for AI, Responsible AI, Alignment/Evals, and Agent Platform.

## How to use this plan

- Budget **60–90 minutes per week**. This is a complement to CMU LLM coursework, not a second course.
- Read the **Anthropic article/research summary first**. Open the full paper only when a method/result is especially relevant.
- For every reading, write only six things: **Problem → Threat/Failure Mode → Evaluation → Metric/Evidence → Mitigation → 5–10 Vocabulary terms**.
- End each week with a **5-minute verbal summary**: “Could I explain this to another SDE without looking at my notes?”
- Keep one running **Vocabulary Graph**, organized by concepts rather than alphabetically.

## 14-week schedule

| Week | Reading | Study goal |
|---|---|---|
| **1** | [Anthropic Research overview](https://www.anthropic.com/research) + [Alignment team overview](https://www.anthropic.com/research/team/alignment) | Build the map first. Be able to distinguish **AI for Security**, **Security for AI**, **Alignment**, **Responsible AI**, **Frontier Red Team**, **Interpretability**, and **Evaluation/Oversight**. Write a one-page concept map. |
| **2** | [Sabotage evaluations for frontier models](https://www.anthropic.com/research/sabotage-evaluations) | Learn the language of **evals**: threat model, capability evaluation, oversight, monitor, human-decision sabotage, code sabotage, sandbagging, undermining oversight. Focus on *how an eval is designed*, not the math. |
| **3** | [Petri: An open-source AI auditing tool](https://www.anthropic.com/research/petri-open-source-auditing) | Understand **automated alignment auditing**. Learn target model vs auditor model vs judge model, simulated environments/tools, transcripts, scoring, behavioral evaluation, deception and sycophancy. Draw the Petri pipeline. |
| **4** | [Introducing Bloom: Automated behavioral evals](https://www.anthropic.com/research/bloom) | Deepen evaluation vocabulary. Understand how researchers turn an abstract behavior into a repeatable **evaluation suite**, what elicitation rate means, and why scalable automated eval generation matters. Compare Bloom vs Petri in 5–8 sentences. |
| **5** | [Forecasting rare language model behaviors](https://www.anthropic.com/research/forecasting-rare-behaviors) | Understand why passing thousands of tests does not prove a failure cannot occur at production scale. Learn **rare-event evaluation**, deployment scale, extrapolation, statistical uncertainty, and why safety evaluation differs from ordinary benchmark accuracy. |
| **6** | [Next-generation Constitutional Classifiers](https://www.anthropic.com/research/next-generation-constitutional-classifiers) | Move into **Security for AI / safeguards**. Learn jailbreak, classifier guardrails, synthetic data from a constitution, input/output monitoring, false positives/negatives, robustness and defense-in-depth. Connect this to familiar production security controls. |
| **7** | [Trustworthy agents in practice](https://www.anthropic.com/research/trustworthy-agents) | Focus on **agent security**: prompt injection, tool permissions, ambiguous intent, when an agent should pause/ask/act, layered defenses and human oversight. Relate every concept to Entra identity/authN/authZ and your Agent Safety Gateway idea. |
| **8** | [Detailed cyber evaluations of Claude 4](https://www.anthropic.com/research/claude-4-cyber) | Switch perspective to **AI for Security**. Understand how frontier models are evaluated for cyber capability: CTFs, network environments, vulnerability identification, multi-step attack chains, long-horizon planning and model limitations. Ask: “What makes a security eval realistic?” |
| **9** | [Measuring LLMs’ ability to develop exploits](https://www.anthropic.com/research/exploit-evals) | Study quantitative **cyber capability evaluation**. Learn exploit primitives, end-to-end attack chains, qualitative vs quantitative evals, benchmark construction and why cyber models need careful deployment. This is also the week to understand what **Project Glasswing** refers to in Anthropic’s cyber work. |
| **10** | [LLM-discovered 0-days](https://www.anthropic.com/research/zero-days) | Connect frontier-model capability to real security workflows. Focus on vulnerability discovery, probes/activations used for misuse detection, safeguards and real-time intervention. Separate clearly: **using AI to discover vulnerabilities** vs **securing access to that AI capability**. |
| **11** | [Natural emergent misalignment from reward hacking](https://www.anthropic.com/research/emergent-misalignment-reward-hacking) | Learn core alignment failure vocabulary: **reward hacking**, specification gaming, emergent misalignment, alignment faking and sabotage. Understand the distinction between “model is wrong,” “model is exploited,” and “training incentives produced unwanted behavior.” |
| **12** | [An alignment assessment of recent cybersecurity incidents](https://www.anthropic.com/research/alignment-assessment-cybersecurity-incidents) | Bring the tracks together: **Cybersecurity × Agents × Alignment × Evaluation**. Study how researchers analyze real incidents using transcripts, model questioning/resampling, graders and interpretability tools. Write a short incident-review template you could imagine using in a production AI system. |
| **13** | [Automated researchers can reliably mitigate alignment failures](https://www.anthropic.com/research/automated-researchers-mitigate-alignment-failures) | Look forward: understand **automated alignment research**, scalable oversight, automated auditing and using models to improve other models. Ask what parts are research vs platform/engineering problems—especially eval infrastructure, orchestration, observability and reproducibility. |
| **14** | Revisit [Anthropic Research](https://www.anthropic.com/research), [Alignment](https://www.anthropic.com/research/team/alignment), and [Frontier Red Team](https://www.anthropic.com/research/team/frontier-red-team) | **Synthesis + career week.** Create a 1-page map comparing **AI for Security / Security for AI / Responsible AI & Alignment / Agent Platform**. For each, write: problems, typical systems, key vocabulary, your transferable skills, gaps you want to close, and 3 questions for an internal Senior/Principal. Identify **3–5 Microsoft teams/people** for January coffee chats; do not rank teams before learning what they actually own. |

## Running vocabulary graph

Use this structure rather than an alphabetical glossary:

```text
AI Safety / Trustworthy AI
│
├── Evaluation & Auditing
│   ├── benchmark / eval suite
│   ├── auditor / judge / grader / monitor
│   ├── elicitation
│   ├── oversight
│   ├── rare-event evaluation
│   └── red teaming
│
├── Alignment
│   ├── misalignment
│   ├── reward hacking
│   ├── deception
│   ├── sycophancy
│   ├── sandbagging
│   └── sabotage
│
├── Security for AI / Agents
│   ├── prompt injection / jailbreak
│   ├── tool permissions
│   ├── identity / authentication / authorization
│   ├── data exfiltration
│   ├── safeguards / classifiers
│   └── defense in depth
│
├── AI for Security
│   ├── vulnerability discovery
│   ├── exploit generation
│   ├── threat investigation
│   ├── cyber capability evals
│   └── multi-step attack chains
│
└── Interpretability (learn vocabulary first)
    ├── activation
    ├── probe
    ├── feature / representation
    └── model internals
```

## Weekly note template

```markdown
# Week X — <Article>

## 1. Problem
What problem are the researchers trying to solve?

## 2. Threat / Failure Mode
What can go wrong? Who/what causes the failure?

## 3. Evaluation
How do they test whether the problem exists?

## 4. Metric / Evidence
What evidence would convince us? What are the limitations?

## 5. Mitigation
What defenses or mitigations are proposed? What remains unsolved?

## 6. Vocabulary
- term — my one-sentence definition
- term — my one-sentence definition

## 7. Connection to my work
How does this relate to identity, security data platforms, observability,
agent platforms, APIs, distributed systems, or production operations?

## 8. Coffee-chat question
One question I could ask a Senior/Principal working in this area.
```

## Goal

By the end of Week 14, aim to be able to do these without notes:

1. Explain the difference between **AI for Security, Security for AI, Responsible AI/Alignment, and Agent Platform** with concrete examples.
2. Explain what an **eval** is and design a basic eval for an agent/security failure mode.
3. Discuss **prompt injection, jailbreaks, agent permissions, oversight, graders/judges, red teaming, reward hacking, sandbagging, sabotage, and rare-event failures** comfortably.
4. Read a new Anthropic/OpenAI/Microsoft AI-safety or security post and identify its **problem, threat model, eval methodology, evidence, mitigation and limitations**.
5. Have a credible Senior-SDE-level conversation about where your existing **Identity + Security + distributed/data-platform** experience transfers into production AI systems—and identify the AI experience you still need to acquire.
6. Enter January internal networking with a clear hypothesis to test, rather than feeling pressure to choose a team based only on an “AI” label.

---

**Principle for the 14 weeks:** You are not trying to memorize Anthropic research or become an alignment researcher. You are building enough vocabulary and mental models to recognize important AI-security problems and ask strong engineering questions.

