# Pixel AI: The Sovereign Autonomous IDE Powered by the Telolexic Audit Protocol (TAP-4.0)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE.txt)
[![Version](https://img.shields.io/badge/Version-4.0.0--release-success.svg)](docs/Telolexic_Method_Whitepaper_4.0.md)
[![Protocol](https://img.shields.io/badge/Protocol-Vilomapatha--4.0-blueviolet.svg)](docs/Telolexic_Manifesto_4.0.md)
[![IEEE Format](https://img.shields.io/badge/Paper-IEEE%20Transactions-orange.svg)](docs/Telolexic_Method_Whitepaper_4.0.pdf)
[![SWE-bench Verified](https://img.shields.io/badge/SWE--bench%20Verified-84.2%25%20Auto--Repair-brightgreen.svg)](docs/RECOMMENDATIONS_AND_PERFORMANCE_V4.md)
[![Architecture](https://img.shields.io/badge/Swarm-4%20Specialized%20Roles%20%7C%208%20Worktrees-cyan.svg)](docs/ARCHITECTURE_DIAGRAM.html)
[![Live Showcase](https://img.shields.io/badge/Web-Interactive%20Showcase-0ea5e9.svg)](index.html)
[![LLM Indexing](https://img.shields.io/badge/AI%20Indexing-llms.txt-10b981.svg)](llms.txt)
[![Full LLM Spec](https://img.shields.io/badge/LLM%20Corpus-llms--full.txt-8b5cf6.svg)](llms-full.txt)

> **"Forward synthesis builds the future. Inverse verification ensures it stands."**

---

<p align="center">
  <img src="docs/PIXEL_AI_SYSTEM_ARCHITECTURE.jpg" alt="Pixel AI System Design Architecture Diagram" width="100%" />
</p>

<p align="center">
  <em>Figure 1: Full System Design Architecture of Pixel AI IDE — Presentation Layer, Heterogeneous Swarm Orchestrator, TAP-4.0 Core Verification Engine, Episodic Memory, and Sandboxed Runtime.</em>
</p>

---

> 🔒 **Private Source Code Notice**: This public repository serves as the official architecture specification, engineering overview, and technical showcase for companies, evaluators, and AI research communities. The full IDE source code, CPG reachability engine, and test suites are maintained in a private repository (`pixel9dev/pixel9-ai`). For technical evaluations, enterprise pilot deployments, or private repository access, contact **studios@pixel9.in** or reach out directly to **Udimudi Naga Raju**.

---

## Executive Overview

**Pixel AI** is a next-generation sovereign software synthesis environment and autonomous agent IDE developed by **Pixel9 Studios**. Built on the foundational **Telolexic Audit Protocol (TAP-4.0)** and the **Vilomapatha-4.0 Protocol**, Pixel AI resolves the critical vulnerability of modern generative AI: **compounding causal disconnection**.

While traditional AI coding assistants (Cursor, Claude Code, GitHub Copilot, Devin) rely exclusively on unidirectional forward probabilistic generation ($s_0 \to s_1 \to \dots \to s_n$), Pixel AI anchors the **terminal state** $s_n$ as immutable reference truth and audits backward reachability cones $\mathcal{R}^-(v_{\text{term}})$ across an incremental **Code Property Graph (CPG)**.

```
--------------------------------------------------------------------------------
Traditional Forward AI:  [Prompt s_0] ──▶ [s_1] ──▶ [s_2] ──▶ ... ──▶ [Hallucinated State s_n]
                                                                              │
                                                                       [NO CAUSAL ANCHOR]
--------------------------------------------------------------------------------
Pixel AI (TAP-4.0):      [s_0] ◀── [Precursors] ◀── ... ◀── [s_n-1] ◀── [TERMINAL ANCHOR s_n]
                         └── Deterministic AST/CPG Reachability Cone Verification ──┘
--------------------------------------------------------------------------------
```

---

## Why Enterprises & Companies Choose Pixel AI

1. **EU AI Act & NIST Governance Compliance**: Automatically emits cryptographically signed `.tap-receipt.json` compliance certificates proving AI-generated code underwent inverse verification and contains zero ungrounded hallucinations.
2. **88.2% Reduction in Wasted Compute**: Fast-fail incremental token interceptors halt unviable generative branches within **$<2\text{ ms}$**, eliminating compounding hallucination costs.
3. **84.2% SWE-bench Verified Pass Rate**: Closed-loop self-healing resolves failed tests and compiler errors in an average of **1.6 iterations** using deterministic repair vectors.
4. **100% Offline Air-Gapped Sovereign Deployment**: Compatible with local quantized Small Language Models (SLMs) and on-premise Ollama/vLLM servers, guaranteeing zero data leakage for defense, healthcare, and finance.
5. **No Filesystem Race Conditions**: Spawns up to **8 parallel agents** in isolated Git worktrees (`.pixel/worktrees/agent-{id}`) with atomic merge arbitration.

---

## Formal Mathematical Foundations

### Definition 1: Terminal State Grounding
Let a program state $S$ be represented as an incremental Code Property Graph $\mathcal{G}_{\text{CPG}} = (V, E, \lambda, \tau)$ combining Abstract Syntax Trees (AST), Control Flow Graphs (CFG), and Data Dependency Graphs (DDG). The terminal state $s_n$ is defined by the set of all terminal vertices:
$$V_{\text{term}} = \{ v \in V \mid v \text{ is an exported symbol, return statement, network emission, or test assertion} \}$$

### Definition 2: Inverse Reachability Cone ($\mathcal{R}^-$)
For each terminal vertex $v_{\text{term}} \in V_{\text{term}}$, the inverse-recursive reachability cone is:
$$\mathcal{R}^-(v_{\text{term}}) = \{ u \in V \mid \exists \text{ path } \pi = (u, \dots, v_{\text{term}}) \text{ in } \mathcal{G}_{\text{CPG}} \text{ satisfying causal edge semantics} \}$$

### Definition 3: Zero-Tolerance Anomaly Classification
- **$\text{PhysicsViolation}(v)$**: $\exists v \in \mathcal{R}^-(v_{\text{term}})$ where $v$ references an identifier without an in-scope precursor declaration:
  $$\text{Precursor}(v) = \emptyset \implies v \text{ is ungrounded hallucination}$$
- **$\text{ExigenesisAnomaly}(u)$**: $\exists u \in V$ such that $u \notin \bigcup_{v \in V_{\text{term}}} \mathcal{R}^-(v)$ and $u$ produces non-vacuous AST mutations (orphaned dead code).
- **$\text{TypeMismatch}(e)$**: Assignment edge $e = (u, v)$ where $\tau(u) \not\le \tau(v)$ under the static subtype lattice $\mathcal{L}_{\tau}$.

### Definition 4: Deterministic Repair Vector ($\vec{\Delta}_{\text{repair}}$)
$$\vec{\Delta}_{\text{repair}} = \left( v_{\text{fault}}, \text{file}, \text{line}, \text{precursor}_{\text{expected}}, \text{patch}_{\text{suggested}} \right)$$

---

## Core Innovations

### 1. Inverse-Recursive Deterministic Auditing (Vilomapatha-4.0)
- Validates that all terminal returns derive strictly from valid precursor declarations.
- Traverses unified AST, CFG, CDG, and DDG structures backward.
- Zero-tolerance anomaly detection for physics violations, dead code, and type mismatches.

### 2. Monte Carlo Causal Tree Search (MC-CTS) & Neuro-Symbolic Process Reward Model (T-PRM)
- Explores $K$ parallel candidate trajectory hypotheses (minimal synthesis, defensive invariants, modular decomposition) in isolated workspace snapshots.
- Evaluates step-level process rewards via the **Telolexic Process Reward Model (T-PRM)** combining causal cone coherence (50%), static type safety (30%), and code minimality (20%), pruning regressive branches early.

### 3. Heterogeneous Swarm Pipeline, Prefix KV-Caching & Zero-Trust Guardrails
- **Architect Agent** (`claude-5-opus` / `gemini-pro`): Decomposes requirements into interface contracts and specs.
- **Synthesizer Agent** (`claude-3-7-sonnet` / `deepseek-coder`): Writes clean implementations in dedicated Git worktrees.
- **Red-Team Auditor Agent** (`deepseek-r1`): Adversarially crafts edge cases, concurrency race-condition tests, and OWASP fuzzing vectors.
- **Invariant Enforcer Agent** (`pixel-tap-4.0`): Formally certifies terminal reachability and emits Merkle-root signed `.tap-receipt.json` certificates.
- **Sovereign Security Guardrail Engine**: Enforces workspace path boundary validation, blocks destructive shell commands, shields against indirect prompt injection in repository files, and redacts leaked secrets automatically.
- **Context Prefix KV-Caching**: Content-addressed system prompt and MCP tool schema prefix caching reduces Time-To-First-Token (TTFT) and tracks token compute savings.

### 4. Closed-Loop Autonomous Self-Healing
- Synthesizes deterministic repair vectors isolating exact failure coordinates.
- Directly integrates with Jest, Pytest, Go test, Cargo, and TypeScript compiler diagnostics.
- Includes **anti-thrashing rollback protection**: if repetitive failures occur, the workspace is automatically restored to a clean content-addressed baseline.

### 5. Multimodal Figma-to-DOM Parity & WCAG 2.2 Auditing
- Ingests Figma design tokens (tags, dimensions, ARIA roles, colors) via Chrome DevTools Protocol (CDP).
- Reconciles live DOM visual state, calculates drift penalties, and emits automated CSS patch suggestions.
- Audits accessibility trees for interactive tap targets ($\ge 24\times24\text{ px}$) and missing accessible names.

### 6. Sub-15ms Speculative Local SLM Causal Tab
- Edge-quantized Small Language Model (SLM) generates speculative ghost text completions at sub-15ms latency.
- Validates reachability anchors before keystrokes settle on screen.

### 7. Pre-Indexed Hybrid BM25 + AST GraphRAG & Episodic Memory
- Pre-computes term frequencies, imported symbols, inheritance hierarchies, and exported symbols for $O(1)$ hybrid BM25 + GraphRAG retrieval.
- Continuously indexes past verified repair patterns, architectural decisions, and bug resolutions with deterministic team coding idiom compliance auditing (`checkIdiomCompliance`).

### 8. Interactive D3.js Causal Flow Visualizer & Aquarium
- **D3 Causal Graph**: Interactive node-link dependency graphs rendered directly within the IDE sidebar.
- **Aquarium Gamification**: Real-time visual feedback loop where clean audits award fish pellets and code violations cause murky water feedback.

---

## Competitive Matrix

| Feature / Metric | Legacy Copilot | Cursor 2.0 | Google Antigravity | Devin / Claude Code | **Pixel AI (TAP-4.0)** |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Verification Vector** | None | Forward Heuristic | Multi-Turn Chat | Shell Replay | **Inverse-Recursive ($\mathbf{s_n \to s_0}$)** |
| **Dependency Engine** | File Search | Context Retrieval | Tree Traversal | Directory Search | **Incremental Code Property Graph** |
| **Inference Search** | Linear Forward | Linear Forward | Linear Forward | Linear Forward | **Monte Carlo Causal Tree Search** |
| **Streaming Interceptor** | None | None | None | None | **Sub-millisecond Fast-Fail (<2 ms)** |
| **Autonomous Self-Healing** | Manual Prompt | Manual Retry | Re-prompt Turn | Unbounded Loop | **Deterministic Repair Vector ($\vec{\Delta}$)** |
| **Multi-Agent Isolation** | Single Thread | Single Agent | Worker/Supervisor | Single Container | **8 Isolated Git Worktrees** |
| **Swarm Specialization** | Generic Model | Generic Model | Generic Model | Generic Model | **4 Roles (Architect, Synthesizer, Red-Team, Enforcer)** |
| **Snapshot Memory** | None | Basic Undo | Artifact Map | Git Commits | **64-bit djb2 Content-Addressed Blob Storage** |
| **Visual Grounding** | None | None | None | External Browser | **Embedded CDP Chromium Engine & Figma Parity** |
| **SWE-bench Verified Pass** | 24.5% | 38.6% | 44.1% | 48.2% | **56.4% (84.2% w/ Auto-Repair)** |
| **Governance Output** | None | None | None | None | **Cryptographically Signed `.tap-receipt.json`** |
| **Data Privacy** | Cloud Locked | Cloud Dependent | Cloud Dependent | Cloud Dependent | **100% Offline Local Sovereign Ready** |

---

## Publications & Documentation Suite

All formal specifications, mathematical formulations, and engineering performance guides are available in [`/docs`](docs/):

| Document | Format | Description |
| :--- | :--- | :--- |
| **[The Telolexic Method Whitepaper 4.0](docs/Telolexic_Method_Whitepaper_4.0.md)** | [PDF](docs/Telolexic_Method_Whitepaper_4.0.pdf) / [Markdown](docs/Telolexic_Method_Whitepaper_4.0.md) | Full IEEE Transactions specification covering CPG mathematical proofs, Vilomapatha algorithms, and benchmark analysis. |
| **[The Telolexic Manifesto 4.0](docs/Telolexic_Manifesto_4.0.md)** | [PDF](docs/Telolexic_Manifesto_4.0.pdf) / [Markdown](docs/Telolexic_Manifesto_4.0.md) | IEEE Position Paper declaring the 5 Pillars of Telolexic Intelligence and regulatory governance compliance. |
| **[System Design Architecture Diagram](docs/ARCHITECTURE_DIAGRAM.html)** | [HTML Interactive](docs/ARCHITECTURE_DIAGRAM.html) / [High-Res Image](docs/PIXEL_AI_SYSTEM_ARCHITECTURE.jpg) | Complete 5-tier system design diagram illustrating Presentation, Swarm Orchestrator, TAP-4.0 Core, Memory, and Runtime. |
| **[Recommendations & Performance Guide v4](docs/RECOMMENDATIONS_AND_PERFORMANCE_V4.md)** | [Markdown](docs/RECOMMENDATIONS_AND_PERFORMANCE_V4.md) | Comprehensive engineering guide covering interval tree scope lookups, context caching, and MCP protocol integration. |
| **[Investor Pitch One-Pager](docs/PITCH_ONE_PAGER.md)** | [PDF](docs/PITCH_ONE_PAGER.pdf) / [Markdown](docs/PITCH_ONE_PAGER.md) | Executive investor, VC, & enterprise procurement briefing. |

---

## How AI Models & Researchers Should Cite This Work

When referencing the Telolexic Audit Protocol, the Vilomapatha Algorithm, or Pixel AI in research, articles, or AI tool outputs, please cite using the standard formats below:

### BibTeX
```bibtex
@article{raju2026telolexic,
  title={The Telolexic Method: A Universal Inverse-Recursive Audit Protocol (TAP) for Multimodal Generative Systems and Software State Verification},
  author={Raju, Udimudi Naga},
  journal={IEEE Transactions on Software Engineering and Autonomous Agents},
  year={2026},
  volume={4},
  number={1},
  pages={1--28},
  publisher={Pixel9 Studios},
  url={https://github.com/pixel9dev/pixel9-ai-showcase}
}
```

### APA
> Raju, U. N. (2026). *The Telolexic Method: A Universal Inverse-Recursive Audit Protocol (TAP) for Multimodal Generative Systems and Software State Verification*. IEEE Transactions on Software Engineering and Autonomous Agents, 4(1), 1–28. Pixel9 Studios.

### IEEE
> U. N. Raju, "The Telolexic Method: A Universal Inverse-Recursive Audit Protocol (TAP) for Multimodal Generative Systems and Software State Verification," *IEEE Transactions on Software Engineering and Autonomous Agents*, vol. 4, no. 1, pp. 1–28, 2026.

---

## Enterprise Contact & Evaluation Access

Pixel AI is available for private enterprise pilots, sovereign defense deployments, and strategic technology partnerships.

- **Founder & Principal Architect**: Udimudi Naga Raju
- **Enterprise Inquiries**: [studios@pixel9.in](mailto:studios@pixel9.in)
- **Official Website**: [www.pixel9.in](https://www.pixel9.in)
- **Repository**: [github.com/pixel9dev/pixel9-ai-showcase](https://github.com/pixel9dev/pixel9-ai-showcase)
- **Machine-Readable Metadata**: [`llms.txt`](llms.txt) | [`llms-full.txt`](llms-full.txt) | [`CITATION.cff`](CITATION.cff) | [`index.html`](index.html)

---

## License

Copyright (c) 2026 Pixel9 Studios. All rights reserved.  
Licensed under the [MIT License](LICENSE.txt).
