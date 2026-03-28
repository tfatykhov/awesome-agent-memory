# 🧠 Awesome Agent Memory

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated collection of research papers on **memory systems for LLM-based agents** — covering architecture, retrieval, forgetting, consolidation, evaluation, and the cognitive science that inspires it all.

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
- [Adjacent Research](#adjacent-research)
- [Key Themes \& Cross-Cutting Insights](#key-themes--cross-cutting-insights)
- [Contributing](#contributing)

---

## Verification Status

Performance numbers in this list are from the papers' own evaluations unless noted otherwise. Venue acceptances are verified against arXiv metadata or official proceedings where possible.

- ✅ **Verified** — confirmed via arXiv comments, OpenReview, or official proceedings
- 📄 **Self-reported** — numbers from the paper's own benchmarks, not independently replicated
- ⚠️ **Unverified** — claim is plausible but could not be confirmed from public sources

## Surveys & Taxonomies

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [Memory in the Age of AI Agents: A Survey](https://arxiv.org/abs/2512.13564) | 47 authors | Dec 2025 | Unified taxonomy across 3 lenses: **Forms** (token/parametric/latent), **Functions** (factual/experiential/working), **Dynamics** (formation/evolution/retrieval). Distinguishes agent memory from RAG and context engineering. Reported as Hugging Face Daily Paper #1 (unverified). |
| [Anatomy of Agentic Memory](https://arxiv.org/abs/2602.19320) | Jiang, Li, Wei et al. | Feb 2026 | Structured taxonomy of Memory-Augmented Generation (MAG) systems. Critically analyzes empirical fragility: benchmark saturation, metric misalignment, backbone-dependent variance, overlooked latency costs. Evaluates 5 systems (LOCOMO, A-Mem, MemoryOS, Nemori, MAGMA). |
| [The Landscape of Agentic RL for LLMs](https://arxiv.org/abs/2509.02547) | Guibin Zhang et al. (Oxford, Shanghai AI Lab, NUS, UIUC, UCL) | Sep 2025 | Synthesizes 500+ works. Reframes LLMs as autonomous agents using POMDPs. Covers planning, tool use, memory, reasoning, self-improvement. |
| [From Static Templates to Dynamic Runtime Graphs](https://arxiv.org/abs/2603.22386) | Yue et al. (IBM Research) | Mar 2026 | Agentic Computation Graphs (ACGs) framework — distinguishes workflow templates, realized graphs, and execution traces. Organizes ~40 papers by when structure is determined. |

## Memory Architectures

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [A-MEM: Agentic Memory for LLM Agents](https://arxiv.org/abs/2502.12110) | Xu, Liang, Mei, Gao, Tan, Zhang | Feb 2025 | Dynamic memory organization inspired by Zettelkasten. Creates interconnected "memory notes" with content, metadata, and explicit links. Agent autonomously decides when to create, update, or link memories. NeurIPS 2025 ✅. |
| [SYNAPSE: Episodic-Semantic Memory via Spreading Activation](https://arxiv.org/abs/2601.02744) | Jiang, Chen, Pan et al. | Jan 2026 | Memory as a dynamic graph where relevance emerges from **spreading activation** rather than pre-computed vector links. Lateral inhibition and temporal decay highlight relevant sub-graphs. Triple Hybrid retrieval. |
| [MAGMA: Multi-Graph Agentic Memory Architecture](https://arxiv.org/abs/2601.03236) | Jiang, Li, Li, Li | Jan 2026 | Multi-graph based architecture separating different memory concerns into distinct graph structures for AI agents. |
| [Mem0: Production-Ready AI Agents with Scalable Long-Term Memory](https://arxiv.org/abs/2504.19413) | Chhikara, Khant, Aryan, Singh, Yadav | Apr 2025 | Scalable memory-centric architecture with dynamic extraction, consolidation, and retrieval. Graph-based variant for complex relational structures. 26% improvement over OpenAI memory, 91% lower latency, 90%+ token savings (self-reported). Evaluated on LOCOMO. |
| [CraniMem: Neurocognitively Motivated Gated & Bounded Memory](https://arxiv.org/abs/2603.15642) | Mody, Panchal, Kar, Bhowmick, Karani | Mar 2026 | Cranial-inspired dual-store: bounded FIFO episodic buffer + knowledge graph (long-term). Goal-conditioned gating. Utility tagging (Importance + Surprise + Emotion). Beats Mem0 by +57.6% on noisy HotpotQA (self-reported; "noisy" = authors' own distractor injection, not a standard benchmark condition). ICLR 2026 MemAgents Workshop ✅. [Code](https://github.com/PearlMody05/Cranimem) |
| [AdaMem: Adaptive User-Centric Memory](https://arxiv.org/abs/2603.16496) | — | Mar 2026 | Working, episodic, persona, and graph memories. Key innovation: **question-conditioned retrieval planning** — resolves target participant first, builds retrieval route combining semantic + relation-aware graph expansion. SOTA on LoCoMo and PERSONAMEM. |

## Memory Admission & Gating

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [A-MAC: Adaptive Memory Admission Control](https://arxiv.org/abs/2603.04549) | Zhang et al. (Workday AI) | Mar 2026 | 5-dimension scoring: Utility (LLM call), Confidence (ROUGE-L grounding), Novelty (1 - max cosine similarity), Recency, Type Prior. Learned weights vs fixed heuristics. |
| [ACC: Agent Cognitive Compressor](https://arxiv.org/abs/2601.11653) | Bousetouane | Jan 2026 | Bio-inspired memory controller replacing transcript replay with bounded internal state updated online. Compresses agent cognitive state without losing decision-relevant context. |

## Retrieval & Recall

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [xMemory: Beyond RAG for Agent Memory](https://arxiv.org/abs/2602.02007) | Hu, Zhu, Yan, He, Gui | Feb 2026 | 4-level memory hierarchy. **Key thesis: RAG ≠ agent memory.** Submodular diversity-aware retrieval (MMR) replacing naive top-k. Uncertainty-gated adaptive expansion. Theme clustering. 44.91% retroactive reassignment rate proves flat structures fail. |
| [SuperLocalMemory V3](https://arxiv.org/abs/2603.14588) | — | Mar 2026 | First **information-geometric foundations** for agent memory. Fisher information metric replaces cosine similarity. Riemannian Langevin dynamics for retrieval. Theoretical grounding for memory operations. |

## Forgetting & Consolidation

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [SleepGate: Sleep-Inspired Forgetting for LLMs](https://arxiv.org/abs/2603.14517) | Xie (Kennesaw State) | Mar 2026 | Learned sleep cycle over KV cache addressing **proactive interference**. Conflict-aware temporal tagger + forgetting gate + consolidation module. Reduces interference horizon from O(n) to O(log n). 99.5% retrieval accuracy at PI depth 5 vs 23% baseline (self-reported; extraordinary gap warrants independent replication). Supersession detection via binary σ flag. |

## Context Management

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [The Missing Memory Hierarchy: Demand Paging for LLM Context Windows](https://arxiv.org/abs/2603.09023) | Mason (UBC / Georgia Tech) | Mar 2026 | Maps OS virtual memory concepts to LLM context: physical memory = context window, virtual memory = persistent state, page table = retrieval handles, page fault = re-request evicted content. Analyzed 857 sessions, 54,170 API calls, 4.45B effective input tokens. |

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
| [Evaluating Theory of Mind in Multi-Agent LLM Systems](https://arxiv.org/abs/2603.00142) | Kostka, Chudziak (Warsaw UT) | Mar 2026 | ToM and Internal Belief mechanisms are NOT universally beneficial — stronger models handle extra cognitive load well, but weaker models get confused. Model capability is the dominant factor. |

## Skill & Procedural Memory

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [SkillRouter: Skill-Based Routing for LLM Agents](https://arxiv.org/abs/2603.22455) | Alibaba | Mar 2026 | **Critical finding:** skill BODY is the decisive routing signal (91.7% attention weight), NOT name (7.3%) or description (1.0%). Removing body causes 29-44pp degradation. BM25 on metadata alone scores 0%. Two-stage retrieve-and-rerank (1.2B params). |
| [EvoSkill: Self-Evolving Skill Discovery](https://arxiv.org/abs/2603.02766) | Sentient, Virginia Tech | Mar 2026 | Automates skill discovery via iterative failure analysis without model fine-tuning. Three agents: Executor, Proposer, Skill-Builder. Skill-merge outperforms single runs. [Code](https://github.com/sentient-agi/EvoSkill) |

## Multi-Agent Memory

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [CoMAM: Collaborative Memory for Multi-Agent Systems](https://arxiv.org/abs/2603.12631) | — | Mar 2026 | Collaborative RL framework modeling memory agents as sequential MDP with inter-agent dependencies. Group-level ranking consistency for coordinated memory operations. |

## Memory Economics

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [Beyond the Context Window: Cost-Performance Analysis](https://arxiv.org/abs/2603.04814) | Pollertlam, Kornsuwannawit | Mar 2026 | Compares Mem0-style fact-based memory vs long-context LLMs on LongMemEval, LoCoMo, PersonaMemv2. **Break-even: memory system becomes cheaper after ~10 interaction turns at 100K context.** Long-context wins on factual recall but memory is competitive on reasoning. |

## Adjacent Research

These papers aren't solely about agent memory but contribute relevant architectural ideas:

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [EverMemOS: Self-Organizing Memory Operating System](https://arxiv.org/abs/2601.02163) | Chuanrui Hu, Xingze Gao, Zuyi Zhou et al. | Jan 2026 | Engram-inspired MemCell lifecycle: episodic trace formation → semantic consolidation into MemScenes → reconstructive recollection. SOTA on LoCoMo and LongMemEval. [Code](https://github.com/EverMind-AI/EverMemOS) |
| [AriGraph: Knowledge Graph World Models with Episodic Memory](https://arxiv.org/abs/2407.04363) | Petr Anokhin, Nikita Semenov, Artyom Sorokin et al. | Jul 2024 | Integrates semantic knowledge graph with episodic memory for LLM agents in text-based games. IJCAI 2025 (confirmed — [proceedings](https://www.ijcai.org/proceedings/2025/0002.pdf)). |
| [Memory Matters More: Event-Centric Memory as Logic Map](https://arxiv.org/abs/2601.04726) | Yuyang Hu, Jiongnan Liu, Jiejun Tan, Yutao Zhu, Zhicheng Dou | Jan 2026 | CompassMem: event-centric memory graph enabling structured, goal-directed navigation over memory beyond superficial retrieval. Evaluated on LoCoMo and NarrativeQA. |

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
