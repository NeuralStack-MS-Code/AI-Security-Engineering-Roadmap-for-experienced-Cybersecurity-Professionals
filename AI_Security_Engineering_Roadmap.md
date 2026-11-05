# AI Security Engineering

A 24-week learning roadmap for experienced cybersecurity professionals, with three capstone project ideas.

## Contents

1. [Purpose and Audience](#1-purpose-and-audience)
2. [Roadmap at a Glance](#2-roadmap-at-a-glance)
3. [Phase Details](#3-phase-details)
4. [Tooling Landscape](#4-tooling-landscape)
5. [Three Capstone Project Ideas](#5-three-capstone-project-ideas)
6. [Completion Criteria](#6-completion-criteria)
7. [Notes on Currency and Responsible Practice](#7-notes-on-currency-and-responsible-practice)

---

## 1. Purpose and Audience

This roadmap guides an experienced cybersecurity professional (for example in penetration testing, red teaming, application security, security architecture, incident response or detection engineering) toward working competence in AI security engineering. It assumes strong command of classical security concepts (threat modeling, injection classes, authentication and authorization, supply chain risk, cloud and network security) and working proficiency in Python. No prior machine-learning background is assumed.

**Guiding principle.** AI security is not detached from security engineering. Many failures in AI systems are familiar failure classes (injection, confused deputy, excessive privilege, supply chain compromise, data leakage) reappearing in systems whose core component is probabilistic, opaque, and unable to reliably separate instructions from data. The roadmap therefore builds machine-learning literacy first and then maps it onto the reader's existing security model.

| Parameter | Recommendation |
|---|---|
| **Duration** | 24 weeks, structured in seven phases (Phase 0 to Phase 6) |
| **Time commitment** | 6 to 10 hours per week (approximately 150 to 240 hours in total) |
| **Laboratory** | Python 3.11 or later, Jupyter, Docker; local inference (Ollama or llama.cpp) for inexpensive experimentation; API access to at least one hosted model |
| **Outcome** | A portfolio of reproducible attack write-ups, a hardened reference application, and one completed capstone project; a selected specialization track |

## 2. Roadmap at a Glance

| Phase | Weeks | Focus | Milestone |
|---|---|---|---|
| 0 | 1 | Baseline and laboratory setup | Written gap analysis; functioning lab environment |
| 1 | 2 to 6 | Machine-learning and LLM foundations | Minimal RAG assistant with tool calling, built without orchestration frameworks |
| 2 | 7 to 9 | Threat landscape and frameworks | Threat model of the Phase 1 application, mapped to OWASP and MITRE ATLAS |
| 3 | 10 to 15 | Offensive AI security | Three reproducible attack write-ups; challenge labs completed |
| 4 | 16 to 19 | Defensive engineering | Hardened application with measured reduction in attack success rate |
| 5 | 20 to 22 | Secure ML lifecycle and supply chain | Scan, verify and sign workflow for third-party models |
| 6 | 23 to 24 | Assurance, governance and specialization | Portfolio summary and selected specialization track |

Capstone projects (Section 5) are scheduled after Phases 3, 4 and 5 respectively, or may be selected individually according to the chosen specialization.

## 3. Phase Details

### Phase 0: Baseline and Laboratory Setup (Week 1)

**Objective.** Establish a skills baseline and a reproducible working environment.

**Core topics**

- Map existing expertise onto the AI attack surface: injection (prompt injection), confused deputy (agents acting with delegated credentials), supply chain (model and dataset provenance), data leakage (training data, context window, retrieval), and denial of service (token and cost exhaustion).
- Identify gaps: linear algebra and probability refreshers as needed; the Python data stack (NumPy, pandas, PyTorch basics).
- Set up the laboratory: virtual environment, Jupyter, Docker, local inference, hosted-model API access, and a notes repository for write-ups.

**Recommended resources**

- 3Blue1Brown, "Essence of Linear Algebra" (video series), if a refresher is needed
- PyTorch official tutorials ("Learn the Basics")

- [ ] **Milestone:** A one-page written gap analysis and a functioning lab.

### Phase 1: Machine-Learning and LLM Foundations (Weeks 2 to 6)

**Objective.** Acquire the minimum literacy required to reason precisely about attacks and defenses.

**Core topics**

- Supervised learning, loss functions, gradient descent, generalization, overfitting and memorization, evaluation metrics (precision, recall, ROC).
- Neural networks and the transformer architecture: tokenization, embeddings, self-attention, context windows.
- Model lifecycle: pretraining, supervised fine-tuning, preference optimization (RLHF and variants), and the relationship between alignment training and safety behavior.
- Inference: sampling parameters, system versus user messages, structured output, and why the instruction channel and the data channel are not cryptographically separated.
- Application patterns: retrieval-augmented generation (chunking, embeddings, vector stores), function calling, agent loops, memory, and the Model Context Protocol (MCP).

**Recommended resources**

- Andrej Karpathy, "Neural Networks: Zero to Hero" (video series)
- 3Blue1Brown, neural networks series
- J. Alammar and M. Grootendorst, *Hands-On Large Language Models* (O'Reilly)
- Hugging Face LLM Course; fast.ai, *Practical Deep Learning for Coders*
- Model-provider documentation on tool use; the MCP specification

- [ ] **Milestone:** Build a small RAG assistant with tool calling using direct API calls (no orchestration framework), so that every trust boundary is visible. This application is the target for all later phases.

### Phase 2: Threat Landscape and Frameworks (Weeks 7 to 9)

**Objective.** Learn the taxonomies and frameworks used to describe and govern AI risk, and apply them in a threat model.

**Core topics**

- OWASP Top 10 for LLM Applications (2025 edition) and the wider OWASP GenAI Security Project, including guidance on agentic threats.
- MITRE ATLAS: adversary tactics and techniques against ML-enabled systems and its relationship to ATT&CK.
- NIST AI 100-2 (adversarial machine learning taxonomy and terminology): evasion, poisoning, privacy and abuse attacks.
- Governance frameworks: NIST AI RMF and the Generative AI Profile (AI 600-1), Google SAIF, ISO/IEC 42001, and the EU AI Act (risk tiers and general-purpose AI obligations).
- Threat-modeling adaptation: treat the model as an untrusted component; draw trust boundaries around retrieved content, tool output and user input; enumerate assets (system prompt, credentials in context, tool privileges, training data).

**Recommended resources**

- OWASP GenAI Security Project (genai.owasp.org)
- MITRE ATLAS matrix and case studies (atlas.mitre.org)
- NIST AI 100-2 and AI 600-1 (nist.gov)
- Google, Secure AI Framework (SAIF)

- [ ] **Milestone:** A data-flow diagram and threat model for the Phase 1 application, mapping each threat to an OWASP category and, where applicable, an ATLAS technique.

### Phase 3: Offensive AI Security (Weeks 10 to 15)

**Objective.** Develop hands-on offensive proficiency across the principal attack classes.

**Core topics**

- Prompt injection: direct and indirect; jailbreak families (role-play, encoding and obfuscation, many-shot, multi-turn escalation); system-prompt extraction.
- Output and data risks: sensitive information disclosure, insecure output handling (XSS, SSRF or code execution through model output), markdown-based exfiltration channels.
- Agent and tool abuse: excessive agency, confused deputy, MCP tool poisoning, tool shadowing and definition changes after approval, and the combination of private data access, untrusted content and an exfiltration channel.
- RAG and embedding attacks: corpus poisoning, retrieval manipulation, cross-tenant leakage.
- Classical adversarial ML: evasion (FGSM, PGD), data poisoning and backdoors, model extraction, membership inference, model inversion.

**Recommended resources**

- Greshake et al. (2023), "Not what you've signed up for" (indirect prompt injection)
- Zou et al. (2023), universal and transferable adversarial attacks on aligned models; Anil et al. (2024), many-shot jailbreaking
- Goodfellow et al. (2014) and Madry et al. (2017) on adversarial examples; Shokri et al. (2017) on membership inference; Tramer et al. (2016) on model extraction
- PortSwigger Web Security Academy, LLM attack labs
- Practice platforms: Gandalf (Lakera), Prompt Airlines (Wiz), Crucible (Dreadnode), HackAPrompt, AI Village at DEF CON
- Microsoft AI Red Team material and PyRIT documentation; garak documentation

- [ ] **Milestone:** Complete at least 20 challenge levels or lab exercises across at least three platforms, and produce three reproducible attack write-ups (setup, payload, observed behavior, root cause, mitigation).

### Phase 4: Defensive Engineering (Weeks 16 to 19)

**Objective.** Design layered controls and quantify their effectiveness, recognizing the limits of probabilistic defenses.

**Core topics**

- Core principle: treat model output as untrusted input, and prefer deterministic controls (authorization, isolation, validation) over probabilistic ones (classifiers, prompt instructions).
- Input and output controls: filtering, content classifiers, structured output enforcement, spotlighting and delimiting of untrusted content; evaluation of false-positive and bypass rates.
- Architectural patterns: privilege separation, dual-model and plan-then-execute designs, taint tracking of untrusted data, human approval for high-impact actions.
- Least privilege for agents: per-tool scopes, short-lived credentials, argument validation, egress restriction, sandboxed code execution (containers, gVisor, microVMs).
- Monitoring and detection engineering: prompt and tool-call telemetry, anomaly detection, abuse and cost controls, incident response for AI systems.

**Recommended resources**

- Beurer-Kellner et al. (2025), "Design Patterns for Securing LLM Agents against Prompt Injections"
- Debenedetti et al. (2025), "Defeating Prompt Injections by Design" (CaMeL)
- Hines et al. (2024), "Defending Against Indirect Prompt Injection Attacks With Spotlighting"
- Documentation: Llama Guard and Prompt Guard (Meta), NeMo Guardrails (NVIDIA), LLM Guard (Protect AI)

- [ ] **Milestone:** Apply layered controls to the Phase 1 application, rerun the Phase 3 attack set, and report attack success rate before and after, together with the benign task completion rate.

### Phase 5: Secure ML Lifecycle and Supply Chain (Weeks 20 to 22)

**Objective.** Secure the artifacts, data and infrastructure that surround the model.

**Core topics**

- Model artifact risks: unsafe deserialization (pickle), safer formats (safetensors), model-hub trust, typosquatting and namespace reuse.
- Integrity and provenance: model signing, hashes, SLSA concepts, ML bills of materials (CycloneDX ML-BOM), dataset provenance.
- Training-time threats: data poisoning, backdoors and sleeper behavior, memorization and training-data extraction; introductory differential privacy.
- Infrastructure: notebook and GPU-cluster security, secrets handling, inference-server exposure and hardening (for example vLLM, Triton, Ollama), model-weight protection.

**Recommended resources**

- OpenSSF Model Signing project; CycloneDX ML-BOM specification
- Protect AI modelscan; Trail of Bits Fickling; Hugging Face safetensors documentation
- Carlini et al. (2021), extracting training data from language models; Carlini et al. (2023), poisoning web-scale training datasets
- Gu et al. (2017), BadNets; Hubinger et al. (2024), Sleeper Agents

- [ ] **Milestone:** A pipeline that quarantines, scans, verifies and signs a third-party model, documented with a short threat model.

### Phase 6: Assurance, Governance and Specialization (Weeks 23 to 24)

**Objective.** Convert technical skills into repeatable practice and select a long-term direction.

**Core topics**

- Designing an AI red-team engagement: scoping, rules of engagement, harm categories, safe handling of generated content, reporting.
- Rating non-deterministic findings: attack success rate over repeated trials, and impact as a function of tool privileges and data access.
- Evaluation methodology: benchmark limitations, reliability of judge models, reproducibility (pinned versions, seeds, sample sizes).
- Regulatory and assurance mapping: AI RMF, ISO/IEC 42001, EU AI Act; evidence collection.
- Specialization tracks: (A) AI red teaming and adversarial evaluation; (B) AI security architecture and agent security engineering; (C) MLSecOps and model supply chain; (D) AI governance, risk and assurance.

**Recommended resources**

- UK AI Security Institute, Inspect evaluation framework documentation
- Microsoft (2025), "Lessons From Red Teaming 100 Generative AI Products"
- MITRE ATLAS case studies

- [ ] **Milestone:** A portfolio (write-ups, harness, gateway or pipeline) and a selected specialization track with a six-month follow-up plan.

## 4. Tooling Landscape

The following tools recur throughout the roadmap. Maintenance status and features change quickly; confirm the current state of each project before adoption.

| Category | Representative tools | Typical use |
|---|---|---|
| **LLM vulnerability scanning and red teaming** | garak (NVIDIA), PyRIT (Microsoft), promptfoo, Giskard | Automated probe suites, custom attack orchestration, regression testing |
| **Evaluation frameworks** | Inspect (UK AISI), promptfoo | Reproducible evaluations, scoring, judge-model workflows |
| **Guardrails and filters** | Llama Guard and Prompt Guard (Meta), NeMo Guardrails (NVIDIA), LLM Guard (Protect AI) | Input and output classification, policy enforcement layers |
| **Adversarial ML libraries** | Adversarial Robustness Toolbox (ART), Foolbox, CleverHans, TextAttack | Evasion, poisoning, extraction and inference attacks on classical models |
| **Model supply chain** | modelscan, fickling, safetensors, OpenSSF model-signing, CycloneDX | Artifact scanning, safe formats, signing, bills of materials |
| **Local inference and serving** | Ollama, llama.cpp, vLLM | Lab targets, offline experimentation, serving-layer security review |
| **Agent and MCP testing** | MCP Inspector, custom MCP servers | Examining tool definitions and building controlled test servers |
| **Observability** | OpenTelemetry, Langfuse | Tracing prompts, retrievals and tool calls for detection and forensics |

## 5. Three Capstone Project Ideas

Each project consumes the outputs of earlier phases and produces an artifact suitable for a public repository or professional portfolio. Estimated effort assumes 6 to 10 hours per week.

### Project 1: Continuous LLM Red-Team Harness

*Schedule: after Phase 3 | Effort: 3 to 4 weeks*

**Goal.** Build a repeatable, CI-integrated adversarial test suite for a RAG assistant, with results mapped to recognized taxonomies.

**Components**

- Target application: the Phase 1 RAG assistant, extended with a document corpus, a planted canary secret in the system prompt, and at least one tool with a side effect.
- Attack library: probe suites from garak and PyRIT or promptfoo, plus custom indirect-injection documents placed in the retrieval corpus.
- Scoring: deterministic checks (canary leakage, unauthorized tool invocation) combined with a rubric-based judge model for policy violations.
- Mapping: every test case tagged with an OWASP LLM Top 10 category and, where applicable, an ATLAS technique.
- CI integration: a workflow that fails when attack success rate exceeds a defined threshold.

**Deliverables**

- Test suite with at least 100 cases across at least six categories
- Machine-readable and HTML reports showing attack success rate by category and over time
- Short methodology note covering model versions, seeds, trial counts and limitations

**Success criteria**

- Results are reproducible with pinned model versions and recorded seeds
- Judge reliability is verified by manually labeling at least 50 samples and reporting the agreement rate
- A deliberately introduced regression is detected by the CI workflow

**Extensions**

- Automated multi-turn escalation attacks
- Comparison across two or three models or system-prompt variants

### Project 2: Policy-Enforcing Tool Gateway for Agents

*Schedule: after Phase 4 | Effort: 4 to 5 weeks*

**Goal.** Implement a deterministic authorization layer between an agent and its tools (including MCP servers) that contains the impact of a successful prompt injection.

**Components**

- Interception proxy that mediates every tool call and records a structured audit log.
- Declarative policy (for example YAML, Open Policy Agent or Cedar): tool allowlists, argument schemas and value constraints, rate limits, and per-session scopes.
- Data-flow labeling: once untrusted content has entered the session, outbound or state-changing calls are blocked or escalated to human approval.
- Tool-definition pinning: hash tool descriptions at approval time and alert on changes.
- Scenario suite: indirect injection through email or web content leading to exfiltration, MCP tool poisoning, and confused-deputy misuse of delegated credentials.

**Deliverables**

- Gateway implementation with documented policy language and example policies
- Scenario suite with scripted attacks and a set of benign tasks
- Report on blocked attacks, benign task completion, latency overhead and explainability of decisions

**Success criteria**

- All scripted attack scenarios are blocked or escalated
- At least 90 percent of benign tasks complete without human intervention
- Every policy decision is traceable to a specific rule in the audit log

**Extensions**

- Plan-then-execute (CaMeL-inspired) agent design with a quarantined model for untrusted content
- Policy tests expressed as property-based tests

### Project 3: Secure Model Supply Chain Pipeline

*Schedule: after Phase 5 | Effort: 3 to 4 weeks*

**Goal.** Create an ingestion gate that admits third-party models and datasets only after scanning, verification and signing.

**Components**

- Quarantine stage: model pulled from a public hub into an isolated environment.
- Static checks: serialization scanning (modelscan, fickling), preference for safetensors, hash and signature verification, license and provenance extraction.
- Behavioral smoke tests: canary prompts and trigger-phrase probing for anomalous behavior.
- Attestation: CycloneDX ML-BOM generation, signing with OpenSSF model-signing, publication to an internal registry with an admission policy that rejects unsigned artifacts.
- Test artifacts: a deliberately flagged serialized model with a benign payload (for example writing a marker file), handled only inside an isolated sandbox.

**Deliverables**

- Pipeline definition (for example GitHub Actions) with documentation
- Threat model for the model ingestion path
- Detection results for the test artifacts, and a generated ML-BOM for an admitted model

**Success criteria**

- All test artifacts are detected and rejected
- No unsigned model is admitted by the registry policy
- The generated ML-BOM validates against the CycloneDX schema

**Extensions**

- BadNets-style poisoning experiment on a small classifier, with a detection method such as activation clustering
- Dataset integrity checks and provenance tracking

## 6. Completion Criteria

Upon completing the roadmap, the reader should be able to:

- Produce a threat model for an LLM-based application or agent, identifying trust boundaries, assets and attack paths.
- Execute and document attacks from each principal class (prompt injection, tool abuse, retrieval poisoning, evasion, extraction, supply chain) in a reproducible manner.
- Select, implement and evaluate layered defenses, and state clearly which risks remain after mitigation.
- Design and report on an AI red-team engagement, including severity assessment for non-deterministic findings.
- Map technical findings to OWASP, MITRE ATLAS, NIST and regulatory requirements.

## 7. Notes on Currency and Responsible Practice

- The field evolves rapidly. Confirm current editions of OWASP, MITRE ATLAS and NIST publications, and the maintenance status of tools, before relying on them.
- Conduct offensive exercises only against systems the reader owns or is explicitly authorized to test, and observe the usage policies of hosted model providers and challenge platforms.
- Handle generated harmful content, credentials and any real data used in experiments according to the same standards as in conventional security engagements.
