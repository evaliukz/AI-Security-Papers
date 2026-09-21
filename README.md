# AI Security + Responsible AI + Alignment — 14-Week Study Plan

**Timeline:** September 2026 → early January 2027  
**Weekly load:** ~60–90 minutes  
**Career goal:** By January 2027, be able to have substantive conversations with internal teams working on **AI for Security, Security for AI, Responsible AI, Alignment/Evals, and Agent Platform**, understand what each team actually owns.

> **Core idea:** Do not try to become an alignment researcher in 14 weeks. Build a durable vocabulary, mental map, and evaluation mindset that connects your existing Identity/Security/Platform experience to production AI systems.

## Landscape

```text
                         TRUSTWORTHY / SAFE AI
                                  │
          ┌───────────────────────┼────────────────────────┐
          │                       │                        │
          ▼                       ▼                        ▼
    AI for Security        Security for AI          Responsible AI
    用 AI 做安全           保护 AI / Agent           管理 AI 的整体风险
          │                       │                        │
 threat detection          prompt injection          fairness
 investigation             jailbreak                 reliability & safety
 vulnerability discovery   identity / permissions    privacy & security
 cyber agents              data exfiltration         transparency
 exploit analysis          tool security             accountability
          │                       │                   human oversight
          └───────────────┬───────┴───────────────┬────────┘
                          ▼                       ▼
                    Evaluation / Evals        Alignment
                    Red Teaming / TEVV        misalignment
                    Monitoring                reward hacking
                    Auditing                  deception/sabotage
```

Responsible AI is intentionally treated as its **own track**, not as a synonym for alignment or security.

## 14-week schedule

| Week | Reading / paper links | Study goal |
|---|---|---|
| **1 — Build the map** | [Anthropic Research](https://www.anthropic.com/research) · [Anthropic Alignment](https://www.anthropic.com/research/team/alignment) · [Microsoft Responsible AI principles](https://www.microsoft.com/en-us/ai/principles-and-approach) | Build the top-level vocabulary. Explain **AI for Security, Security for AI, Alignment, Responsible AI, Frontier Red Team, Evaluation, Interpretability**. Learn Microsoft's six RAI principles: **fairness, reliability & safety, privacy & security, inclusiveness, transparency, accountability**. Deliverable: one-page concept map. |
| **2 — Learn how AI evals work** | [Anthropic — Sabotage evaluations for frontier models](https://www.anthropic.com/research/sabotage-evaluations) | Learn **eval, threat model, capability evaluation, behavioral evaluation, monitor, oversight, grader, sabotage, sandbagging**. Focus on how a vague safety concern becomes a measurable test. Deliverable: design one simple enterprise-agent eval. |
| **3 — Automated auditing** | [Anthropic — Petri / open-source alignment tool](https://www.anthropic.com/research/donating-open-source-petri) | Understand target model → auditor → scenario → transcript → judge/grader. Learn deception, sycophancy and behavioral scoring. Deliverable: draw the Petri pipeline and explain one weakness of LLM-as-a-judge. |
| **4 — Responsible AI as engineering governance** | [Microsoft Responsible AI principles & Standard](https://www.microsoft.com/en-us/ai/principles-and-approach) · [NIST AI RMF 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10) | Learn how RAI becomes an **engineering/governance lifecycle**. For NIST, focus on **GOVERN → MAP → MEASURE → MANAGE**, risk ownership, documentation and deployment controls rather than reading every page. Deliverable: apply the lifecycle to one enterprise agent. |
| **5 — Responsible AI for Generative AI** | [NIST — Generative AI Profile (AI 600-1)](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence) · [PDF](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) | Learn GenAI-specific risk language: **trustworthiness, TEVV, human oversight, privacy, information integrity, misuse, risk measurement**. Read selectively. Deliverable: 8–10 vocabulary terms + a GenAI risk checklist. |
| **6 — Security for AI: trustworthy agents** | [Anthropic — Trustworthy agents in practice](https://www.anthropic.com/research/trustworthy-agents) · [Microsoft — Apply responsible AI to agents](https://learn.microsoft.com/en-us/agents/center-of-excellence/responsible-ai) | Study **prompt injection, tool permissions, ambiguous intent, data boundaries, consequential actions, human approval, fail-safe behavior, continuous monitoring**. Connect to identity/authN/authZ/least privilege. Deliverable: `ALLOW / REQUIRE_APPROVAL / BLOCK` policy. |
| **7 — Alignment failure: reward hacking** | [Anthropic — Natural emergent misalignment from reward hacking](https://www.anthropic.com/research/emergent-misalignment-reward-hacking) | Learn **reward hacking, specification gaming, emergent misalignment, alignment faking, sabotage**. Distinguish normal model error vs adversarial compromise vs unwanted behavior produced by training incentives. |
| **8 — AI for Security: cyber capability** | [Anthropic — Assessing Claude Mythos Preview's cybersecurity capabilities](https://www.anthropic.com/research/mythos-preview) | Switch direction: AI is now the security capability. Study cyber capability evaluation, vulnerability discovery, multi-step security tasks and dual-use risk. Introduction to **Project Glasswing**. |
| **9 — Glasswing + cyber eval methodology** | Re-read the **Project Glasswing** sections of [Mythos Preview cyber capabilities](https://www.anthropic.com/research/mythos-preview) and follow the linked technical material most relevant to evaluation. | Understand **model capability → evaluation evidence → safeguard/deployment decision → defensive use**. Deliverable: explain Glasswing in 2 minutes and identify which pieces are AI for Security vs responsible/secure deployment. |
| **10 — Responsible AI: fairness, transparency, accountability** | [Microsoft Responsible AI principles](https://www.microsoft.com/en-us/ai/principles-and-approach) · [NIST AI RMF resources](https://www.nist.gov/itl/ai-risk-management-framework/ai-risk-management-framework-resources) | Prevent the plan from collapsing into cyber only. Study **fairness, transparency and accountability** in depth. Deliverable: review a hypothetical AI security agent against all six Microsoft RAI principles. |
| **11 — Alignment × real cybersecurity incidents** | [Anthropic — An alignment assessment of recent cybersecurity incidents](https://www.anthropic.com/research/alignment-assessment-cybersecurity-incidents) | Bring the tracks together. Study transcript analysis, resampling, graders, monitoring, interpretability evidence, environment design and mitigation. Deliverable: mini AI incident-review template. |
| **12 — Scaling alignment/evaluation** | [Anthropic — Automated researchers can reliably mitigate alignment failures](https://www.anthropic.com/research/automated-researchers-mitigate-alignment-failures) | Understand automated alignment research and scalable oversight. Separate research from engineering/platform work: **eval infrastructure, orchestration, reproducibility, observability, experiment tracking, deployment gates**. Identify 3 places your platform background transfers. |
| **13 — Responsible AI system-design capstone** | Revisit [NIST GenAI Profile](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence) · [Microsoft Responsible AI](https://www.microsoft.com/en-us/ai/principles-and-approach) · [Anthropic Trustworthy Agents](https://www.anthropic.com/research/trustworthy-agents) | Design a **Responsible Enterprise Security Agent**. Include identity, permissions, grounding, evals, red teaming, fairness, privacy/data boundaries, transparency, human approval, monitoring, incident response and accountable ownership. Deliverable: architecture diagram + one page of design decisions. |
| **14 — Career synthesis & internal search prep** | Revisit [Anthropic Research](https://www.anthropic.com/research), [Alignment](https://www.anthropic.com/research/team/alignment), [Microsoft Responsible AI](https://www.microsoft.com/en-us/ai/principles-and-approach), [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) | Final map: **AI for Security vs Security for AI vs Responsible AI vs Alignment/Evals vs Agent Platform**. For each: problems, systems, vocabulary, what Senior SDEs build, transferable strengths, missing experience, and 3 coffee-chat questions. Identify **3–5 internal teams/people** for January. |

## Responsible AI anchor

Use Microsoft's six principles:

1. **Fairness**
2. **Reliability & Safety**
3. **Privacy & Security**
4. **Inclusiveness**
5. **Transparency**
6. **Accountability**

Connect them to NIST:

```text
GOVERN → MAP → MEASURE → MANAGE → continuous lifecycle
```

Key vocabulary:
- AI risk assessment
- risk tolerance
- impact assessment
- human oversight / human-in-the-loop
- consequential actions
- transparency / disclosure
- explainability vs transparency
- accountability / ownership
- privacy
- fairness / bias
- reliability / failure modes
- TEVV — testing, evaluation, verification, validation
- deployment gates
- continuous monitoring
- incident management

## Weekly study method

**Pass 1 — 15–20 min: Find the story**
1. What problem are they worried about?
2. Why does ordinary software testing not solve it?
3. Is this AI for Security, Security for AI, Responsible AI, Alignment, or an overlap?

**Pass 2 — 25–35 min: Understand the mechanism**

```text
Problem
  ↓
Threat / Failure Mode
  ↓
Evaluation / Measurement
  ↓
Evidence
  ↓
Mitigation / Control
  ↓
Remaining uncertainty
```

**Pass 3 — 15 min: Build vocabulary**

For 5–10 useful terms:
```text
Term:
One-sentence definition:
Concrete example:
Related terms:
Where it sits in my landscape map:
```

**Pass 4 — 10 min: Career translation**

Ask: **If I were a Senior SDE on this team, what would I actually build?**

Examples: eval platform, agent authorization layer, red-team infrastructure, monitoring/observability, security investigation agent, model gateway, human-approval workflow, audit/trace system, RAI deployment pipeline.

## Weekly note template

```markdown
# Week X — <Topic>

## 1. Problem
What problem is this work trying to solve?

## 2. Which bucket?
- [ ] AI for Security
- [ ] Security for AI
- [ ] Responsible AI
- [ ] Alignment
- [ ] Evaluation / Red Team
- [ ] Agent Platform

Why?

## 3. Threat / Failure Mode
What can go wrong?
Is the cause an attacker, model capability, training incentive,
bad system design, bad data, or human/process failure?

## 4. Evaluation / Measurement
How do they know whether the problem exists?
- test environment?
- dataset/scenario?
- grader/judge?
- metric?
- baseline?

## 5. Evidence & limitations
What did they actually demonstrate?
What did they NOT demonstrate?

## 6. Mitigation / control
What defenses, safeguards, governance processes,
or architectural controls are proposed?

## 7. Responsible AI lens
- Fairness
- Reliability & Safety
- Privacy & Security
- Inclusiveness
- Transparency
- Accountability
- Human oversight

## 8. Vocabulary
| Term | My definition | Concrete example |
|---|---|---|
|  |  |  |

## 9. Connection to my experience
Identity / Entra / security / distributed systems / data platform /
observability / APIs / production operations / agents

## 10. Senior-SDE engineering question
If this became a production system, what would be difficult to build?

## 11. Coffee-chat question
One question I could ask someone actually working in this area.
```

## January 2027 exit criteria

By Week 14, be able to:

1. Explain **AI for Security, Security for AI, Responsible AI, Alignment, and Agent Platform** with concrete examples.
2. Given a failure mode, sketch **threat model → eval → grader/metric → threshold → mitigation → re-evaluation → production monitoring**.
3. Apply Microsoft's six Responsible AI principles plus human oversight to an enterprise agent design.
4. Read a new research post and identify **Problem → Threat Model → Evaluation → Evidence → Mitigation → Limitations**.
5. Translate research into engineering: **“What infrastructure would we need to productionize this?”**
6. Enter internal networking with hypotheses rather than choosing teams based on an “AI” label.

## Recommended source hierarchy

### Anthropic
Best for **alignment, behavioral/model evals, frontier safety, agent safety, cyber capability research, red teaming**.  
Research hub: https://www.anthropic.com/research

### Microsoft
Best for **enterprise Responsible AI, principles → engineering requirements, agent deployment, governance, real product architecture**.  
Responsible AI: https://www.microsoft.com/en-us/ai/principles-and-approach

### NIST
Best for **vendor-neutral risk-management vocabulary, AI lifecycle, governance, TEVV, systematic GenAI risk taxonomy**.  
AI RMF: https://www.nist.gov/itl/ai-risk-management-framework  
GenAI Profile: https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence

---

**Final principle:** The goal is not “I have read 14 AI papers.” The goal is: **I understand the landscape well enough to recognize what problem a team is actually solving, understand its vocabulary, ask technically meaningful questions, and judge whether spending the next 2–3 years there would add the AI experience I want.**
