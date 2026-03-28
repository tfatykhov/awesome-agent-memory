# 🧠 Awesome Agent Memory

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated collection of research papers on **memory systems for LLM-based agents** — covering architecture, retrieval, forgetting, consolidation, evaluation, the cognitive science that inspires it all, and the neuromorphic hardware that may one day implement it.

> **Why this list?** Every agent framework bolts on a vector store and calls it "memory." These papers show what memory *actually* requires: admission control, consolidation loops, forgetting mechanisms, typed multi-store architectures, and retrieval strategies that go far beyond cosine similarity.

**Maintained by** [@tfatykhov](https://github.com/tfatykhov) · Built alongside [Nous](https://cognition-engines.ai/nous.html), a cognitive AI agent using the FORGE architecture.

---

## Contents

- [Surveys \& Taxonomies](#surveys--taxonomies)
- [Memory Architectures](#memory-architectures)
- [Memory Admission \& Gating](#memory-admission--gating)
- [Retrieval \& Recall](#retrieval--recall)
- [Forgetting \& Consolidation](#forgetting--consolidation)
- [Context Management](#context-management)
- [Evaluation \& Benchmarks](#evaluation--benchmarks)
- [Cognitive \& Neuroscience-Inspired](#cognitive--neuroscience-inspired)
- [Skill \& Procedural Memory](#skill--procedural-memory)
- [Multi-Agent Memory](#multi-agent-memory)
- [Memory Economics](#memory-economics)
- [Neuromorphic \& Bio-Inspired Memory](#neuromorphic--bio-inspired-memory)
- [Adjacent Research](#adjacent-research)
- [Key Themes \& Cross-Cutting Insights](#key-themes--cross-cutting-insights)
- [Contributing](#contributing)

---

## Surveys & Taxonomies

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [Memory in the Age of AI Agents: A Survey](https://arxiv.org/abs/2512.13564) | 47 authors | Dec 2025 | Unified taxonomy across 3 lenses: **Forms** (token/parametric/latent), **Functions** (factual/experiential/working), **Dynamics** (formation/evolution/retrieval). Distinguishes agent memory from RAG and context engineering. Hugging Face Daily Paper #1. |
| [Anatomy of Agentic Memory](https://arxiv.org/abs/2602.19320) | Jiang, Li, Wei et al. | Feb 2026 | Structured taxonomy of Memory-Augmented Generation (MAG) systems. Critically analyzes empirical fragility: benchmark saturation, metric misalignment, backbone-dependent variance, overlooked latency costs. Evaluates 5 systems (LOCOMO, A-Mem, MemoryOS, Nemori, MAGMA). |
| [The Landscape of Agentic RL for LLMs](https://arxiv.org/abs/2509.02547) | Oxford, Shanghai AI Lab, NUS, UIUC, UCL et al. | Sep 2025 | Synthesizes 500+ works. Reframes LLMs as autonomous agents using POMDPs. Covers planning, tool use, memory, reasoning, self-improvement. |
| [From Static Templates to Dynamic Runtime Graphs](https://arxiv.org/abs/2603.22386) | Yue et al. (IBM Research) | Sep 2025 | Agentic Computation Graphs (ACGs) framework — distinguishes workflow templates, realized graphs, and execution traces. Organizes ~40 papers by when structure is determined. |

## Memory Architectures

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [A-MEM: Agentic Memory for LLM Agents](https://arxiv.org/abs/2502.12110) | Xu, Liang, Mei, Gao, Tan, Zhang | Feb 2025 | Dynamic memory organization inspired by Zettelkasten. Creates interconnected "memory notes" with content, metadata, and explicit links. Agent autonomously decides when to create, update, or link memories. NeurIPS 2025. |
| [SYNAPSE: Episodic-Semantic Memory via Spreading Activation](https://arxiv.org/abs/2601.02744) | Jiang, Chen, Pan et al. | Jan 2026 | Memory as a dynamic graph where relevance emerges from **spreading activation** rather than pre-computed vector links. Lateral inhibition and temporal decay highlight relevant sub-graphs. Triple Hybrid retrieval. |
| [MAGMA: Multi-Graph Agentic Memory Architecture](https://arxiv.org/abs/2601.03236) | Jiang, Li, Li, Li | Jan 2026 | Multi-graph based architecture separating different memory concerns into distinct graph structures for AI agents. |
| [Mem0: Production-Ready AI Agents with Scalable Long-Term Memory](https://arxiv.org/abs/2504.19413) | Chhikara, Khant, Aryan, Singh, Yadav | Apr 2025 | Scalable memory-centric architecture with dynamic extraction, consolidation, and retrieval. Graph-based variant for complex relational structures. 26% improvement over OpenAI memory, 91% lower latency, 90%+ token savings. Evaluated on LOCOMO. |
| [CraniMem: Neurocognitively Motivated Gated & Bounded Memory](https://arxiv.org/abs/2603.15642) | Mody, Panchal, Kar, Bhowmick, Karani | Sep 2025 | Cranial-inspired dual-store: bounded FIFO episodic buffer + knowledge graph (long-term). Goal-conditioned gating. Utility tagging (Importance + Surprise + Emotion). Beats Mem0 by +57.6% on noisy HotpotQA. ICLR 2026 MemAgents Workshop. [Code](https://github.com/PearlMody05/Cranimem) |
| [AdaMem: Adaptive User-Centric Memory](https://arxiv.org/abs/2603.16496) | — | Sep 2025 | Working, episodic, persona, and graph memories. Key innovation: **question-conditioned retrieval planning** — resolves target participant first, builds retrieval route combining semantic + relation-aware graph expansion. SOTA on LoCoMo and PERSONAMEM. |

## Memory Admission & Gating

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [A-MAC: Adaptive Memory Admission Control](https://arxiv.org/abs/2603.04549) | Zhang et al. (Workday AI) | Sep 2025 | 5-dimension scoring: Utility (LLM call), Confidence (ROUGE-L grounding), Novelty (1 - max cosine similarity), Recency, Type Prior. Learned weights vs fixed heuristics. |
| [ACC: Agent Cognitive Compressor](https://arxiv.org/abs/2601.11653) | Bousetouane | Jan 2026 | Bio-inspired memory controller replacing transcript replay with bounded internal state updated online. Compresses agent cognitive state without losing decision-relevant context. |

## Retrieval & Recall

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [xMemory: Beyond RAG for Agent Memory](https://arxiv.org/abs/2602.02007) | Hu, Zhu, Yan, He, Gui | Feb 2026 | 4-level memory hierarchy. **Key thesis: RAG ≠ agent memory.** Submodular diversity-aware retrieval (MMR) replacing naive top-k. Uncertainty-gated adaptive expansion. Theme clustering. 44.91% retroactive reassignment rate proves flat structures fail. ICML 2026. |
| [SuperLocalMemory V3](https://arxiv.org/abs/2603.14588) | — | Sep 2025 | First **information-geometric foundations** for agent memory. Fisher information metric replaces cosine similarity. Riemannian Langevin dynamics for retrieval. Theoretical grounding for memory operations. |

## Forgetting & Consolidation

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [SleepGate: Sleep-Inspired Forgetting for LLMs](https://arxiv.org/abs/2603.14517) | Xie (Kennesaw State) | Sep 2025 | Learned sleep cycle over KV cache addressing **proactive interference**. Conflict-aware temporal tagger + forgetting gate + consolidation module. Reduces interference horizon from O(n) to O(log n). 99.5% retrieval accuracy at PI depth 5 vs 23% baseline. Supersession detection via binary σ flag. |

## Context Management

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [The Missing Memory Hierarchy: Demand Paging for LLM Context Windows](https://arxiv.org/abs/2603.09023) | Mason (UBC / Georgia Tech) | Sep 2025 | Maps OS virtual memory concepts to LLM context: physical memory = context window, virtual memory = persistent state, page table = retrieval handles, page fault = re-request evicted content. Analyzed 857 sessions, 54,170 API calls, 4.45B effective input tokens. |

## Evaluation & Benchmarks

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [StructMemEval: Evaluating Memory Structure in LLM Agents](https://arxiv.org/abs/2602.11243) | Shutova, Olenina, Vinogradov, Sinitsin | Feb 2026 | Tests agents' ability to **organize** memory (not just retrieve). Tasks: transaction ledgers, to-do lists, trees. Key finding: LLMs don't spontaneously recognize when to apply memory structure — they succeed only when explicitly prompted. |

## Cognitive & Neuroscience-Inspired

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [Episodic Memory is the Missing Piece for Long-Term LLM Agents](https://arxiv.org/abs/2502.06975) | Pink et al. (UT Austin) | Feb 2025 | Position paper arguing episodic memory — supporting single-shot learning of instance-specific contexts — is the critical missing capability. Defines 5 properties: temporal, instance-specific, single-shot, inspectable, compositional. |
| [MAP: Modular Agentic Planner](https://www.nature.com/natcomms/) | — | 2025 | Brain-inspired architecture decomposing planning into PFC-associated modules: conflict monitoring, state prediction, state evaluation, task decomposition, task coordination. Nature Communications. |
| [SCL: Structured Cognitive Loop with Governance Layer](https://arxiv.org/abs/2511.17673) | Kim | Nov 2025 | R-CCAM: Retrieval → Cognition → Control → Action → Memory. **Soft Symbolic Control** = governance layer applying symbolic constraints to probabilistic inference. Zero policy violations, complete decision traceability. |
| [Procedural Memory Is Not All You Need](https://arxiv.org/abs/2505.03434) | Wheeler, Jeunen | May 2025 | LLMs are constrained by reliance on procedural memory (pattern-driven tasks). For "wicked" learning environments with shifting rules and ambiguous feedback, different memory types are required. ACM UMAP '25. |
| [Evaluating Theory of Mind in Multi-Agent LLM Systems](https://arxiv.org/abs/2603.00142) | Kostka, Chudziak (Warsaw UT) | Sep 2025 | ToM and Internal Belief mechanisms are NOT universally beneficial — stronger models handle extra cognitive load well, but weaker models get confused. Model capability is the dominant factor. |

## Skill & Procedural Memory

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [SkillRouter: Skill-Based Routing for LLM Agents](https://arxiv.org/abs/2603.22455) | Alibaba | Sep 2025 | **Critical finding:** skill BODY is the decisive routing signal (91.7% attention weight), NOT name (7.3%) or description (1.0%). Removing body causes 29-44pp degradation. BM25 on metadata alone scores 0%. Two-stage retrieve-and-rerank (1.2B params). |
| [EvoSkill: Self-Evolving Skill Discovery](https://arxiv.org/abs/2603.02766) | Sentient, Virginia Tech | Sep 2025 | Automates skill discovery via iterative failure analysis without model fine-tuning. Three agents: Executor, Proposer, Skill-Builder. Skill-merge outperforms single runs. [Code](https://github.com/sentient-agi/EvoSkill) |

## Multi-Agent Memory

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [CoMAM: Collaborative Memory for Multi-Agent Systems](https://arxiv.org/abs/2603.12631) | — | Sep 2025 | Collaborative RL framework modeling memory agents as sequential MDP with inter-agent dependencies. Group-level ranking consistency for coordinated memory operations. |

## Memory Economics

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [Beyond the Context Window: Cost-Performance Analysis](https://arxiv.org/abs/2603.04814) | Pollertlam, Kornsuwannawit | Sep 2025 | Compares Mem0-style fact-based memory vs long-context LLMs on LongMemEval, LoCoMo, PersonaMemv2. **Break-even: memory system becomes cheaper after ~10 interaction turns at 100K context.** Long-context wins on factual recall but memory is competitive on reasoning. |

## Neuromorphic & Bio-Inspired Memory

> *Most agent memory research ignores 50 years of neuroscience. This section bridges that gap — connecting the biological mechanisms that LLM memory papers abstract from (SleepGate's forgetting, CraniMem's gating, A-MEM's dual-phase encoding) to the spiking neural network implementations that model them directly.*

| Paper / Project | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [A Bio-realistic Synthetic Hippocampus for Robotic Cognition](https://link.springer.com/article/10.1007/s12668-025-02229-2) | Talanov et al. | Oct 2025 | Synthetic hippocampal architecture with **dual-phase operation**: online sensorimotor encoding during wake, offline consolidation via SWR-triggered replay during sleep. SNN on neuromorphic substrates (≤1W). Goal-prioritised plasticity prevents catastrophic forgetting. Directly models the biology that SleepGate and CraniMem abstract. BioNanoScience. Open access. |
| [The Memristive Implementation of the Hippocampus: A Hypothesis](https://link.springer.com/article/10.1007/s12668-025-02124-w) | Talanov et al. | Aug 2025 | Hardware-level hippocampal memory using stochastic polycrystalline nano-fiber mesh as memristive substrate. Key insight: the **inherent randomness** of material structure mimics probabilistic biological synaptic networks. Demonstrates resistive switching tunability for implementing dynamic memory functions — bidirectional replay, synaptic up/down-scaling, consolidation. BioNanoScience. Open access. |
| [Simulation of Serotonin Mechanisms in NEUCOGAR Cognitive Architecture](https://www.sciencedirect.com/science/article/abs/pii/S2212683X15000663) | Talanov, Gafarov, Vallverdú et al. | 2018 | Maps neuromodulatory mechanisms to computational models: **dopamine → attention**, **serotonin → inhibition**. The "cube of emotions" model. Demonstrates that mammalian emotional-state control via monoamine neurotransmitters can be re-implemented computationally. Foundation for neuromodulator-gated memory admission. Procedia Computer Science. |
| [tinyHippo](https://github.com/max-talanov/tinyHippo) | Talanov | Active | CA1 + CA3 hippocampal microcircuit simulation in NEST with Izhikevich neurons. Implements **bidirectional replay**, theta-modulated encoding/retrieval phase separation, and SWR-triggered consolidation. The biological reference implementation — validates the mechanisms that Membrain engineers and SleepGate abstracts. MIT license. |
| [Membrain](https://github.com/tfatykhov/membrain) | Fatykhov | Active | Neuromorphic memory bridge using **FlyHash encoding** and BiCameralMemory SNN (Nengo/Voja learning). Hopfield-style attractor dynamics for pattern completion (100% at 20% noise). Stochastic consolidation with SleepSignal. gRPC API for agent integration. The engineering abstraction layer between biological models (tinyHippo) and cognitive agents (Nous). |

**The Stack:** These projects form a natural hierarchy — **tinyHippo** (biological model, validates mechanisms) → **Membrain** (engineering abstraction, SNN service) → **Nous** (cognitive agent, consumes memory). The papers provide the theoretical foundation; the repos provide working implementations.

**Why this matters for agent memory:** The LLM papers in this list independently converge on mechanisms that neuroscience has studied for decades:
- SleepGate's learned forgetting ← hippocampal SWR consolidation during sleep (Talanov 2025a)
- CraniMem's utility gating ← neuromodulator-gated admission (Talanov/NEUCOGAR 2018)
- A-MEM's dual-phase encoding ← online/offline hippocampal states (Talanov 2025a, tinyHippo)
- xMemory's hierarchical consolidation ← cortical-hippocampal memory transfer (Talanov 2025b)

## Adjacent Research

These papers aren't solely about agent memory but contribute relevant architectural ideas:

| Paper | Date | Relevance |
|-------|------|-----------|
| EverMemOS | Jan 2026 | Self-Organizing Memory Operating System for structured long-horizon reasoning. |
| AriGraph (IJCAI 2025) | 2025 | Knowledge Graph World Models with episodic + semantic memory. |
| Memory Matters More | Jan 2026 | Event-centric memory as a logic map for agent searching and reasoning. |

---

## Key Themes & Cross-Cutting Insights

These papers, taken together, converge on several architectural principles:

### 1. 🚪 Gated Admission — Not Everything Deserves to be Remembered
**Papers:** A-MAC, CraniMem, SleepGate, ACC

The strongest systems **filter before storing**. CraniMem uses goal-conditioned cosine gating; A-MAC scores across 5 dimensions (utility, confidence, novelty, recency, type). The alternative — storing everything and retrieving selectively — leads to noise accumulation and proactive interference.

### 2. 📦 Typed Multi-Store — One Vector Store Is Not Memory
**Papers:** xMemory, SYNAPSE, AdaMem, CraniMem, Mem0, Episodic Memory

Every serious architecture separates memory by type (episodic, semantic, procedural, working). xMemory's 4-level hierarchy shows **44.91% of memories get retroactively reassigned** — proving flat structures fundamentally fail. The human brain doesn't use one store; neither should your agent.

### 3. 🔄 Consolidation Loops — Memory Must Evolve
**Papers:** SleepGate, CraniMem, SYNAPSE, A-MEM

Raw episodic traces should consolidate into durable semantic knowledge over time. SleepGate's sleep cycles, CraniMem's replay-based promotion, and SYNAPSE's spreading activation all implement variants of this. Without consolidation, memory becomes a write-only log.

### 4. 🗑️ Forgetting as a Feature — Not a Bug
**Papers:** SleepGate, Procedural Memory, xMemory

SleepGate reduces proactive interference from O(n) to O(log n) through learned forgetting. This is the most under-implemented capability in agent frameworks — most systems only add memories, never remove or decay them. Forgetting is what keeps memory **useful** rather than just large.

### 5. 📊 RAG ≠ Agent Memory
**Papers:** xMemory, Memory Survey, Anatomy of Agentic Memory

The clearest thesis across this literature: retrieval-augmented generation is a **retrieval strategy**, not a memory system. Agent memory requires admission, evolution, consolidation, forgetting, typed storage, and context-aware retrieval. RAG addresses only the last item.

### 6. 🧪 Evaluation Is Broken
**Papers:** Anatomy of Agentic Memory, StructMemEval

Current benchmarks are saturated, metrics misalign with semantic utility, and results vary wildly by backbone model. StructMemEval reveals agents can't organize memory autonomously. The field needs better evaluation before it can claim progress.

---

## Open Questions

- **How should admission gates interact with consolidation loops?** (A-MAC + SleepGate integration)
- **What's the right forgetting curve for different memory types?** (No paper addresses type-specific decay)
- **Can skill routing be unified with memory retrieval?** (SkillRouter + xMemory convergence)
- **What's the minimum viable memory architecture?** (Most papers add complexity — none simplify)

---

## Contributing

This list grows as the field grows. To contribute:

1. Open an issue or PR with the paper title, arXiv/DOI link, authors, date, and a 1-2 sentence summary of the key contribution
2. Suggest which section it belongs in (or propose a new one)
3. Bonus: note how it relates to or challenges existing papers in the list

Papers should be peer-reviewed, at reputable workshops (e.g., ICLR MemAgents), or highly cited preprints. We prioritize papers with **novel architectural ideas** over incremental benchmark improvements.

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

This list is released under CC0. The papers themselves retain their original licenses.
