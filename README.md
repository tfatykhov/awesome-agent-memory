# 🧠 Awesome Agent Memory

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated collection of research papers on **memory systems for LLM-based agents** — covering architecture, retrieval, forgetting, consolidation, evaluation, the cognitive science that inspires it all, and the neuromorphic hardware that may one day implement it.

> **Why this list?** Every agent framework bolts on a vector store and calls it "memory." These papers show what memory *actually* requires: admission control, consolidation loops, forgetting mechanisms, typed multi-store architectures, and retrieval strategies that go far beyond cosine similarity.

**Maintained by** [@tfatykhov](https://github.com/tfatykhov) · Built alongside [Nous](https://github.com/tfatykhov/nous), a cognitive AI agent with typed multi-store memory.


### 🚀 Start Here

| If you want to... | Start with |
|---|---|
| **Understand the landscape** | [Memory Survey](https://arxiv.org/abs/2512.13564) (taxonomy) → [Anatomy](https://arxiv.org/abs/2602.19320) (critical analysis) |
| **Build agent memory** | [xMemory](https://arxiv.org/abs/2602.02007) (why RAG isn't enough) → [A-MAC](https://arxiv.org/abs/2603.04549) (admission control) → [Mem0](https://arxiv.org/abs/2504.19413) (production system) |
| **Add forgetting/consolidation** | [SleepGate](https://arxiv.org/abs/2603.14517) → [CraniMem](https://arxiv.org/abs/2603.15642) |
| **Evaluate your memory system** | [StructMemEval](https://arxiv.org/abs/2602.11243) → [Anatomy](https://arxiv.org/abs/2602.19320) (why benchmarks are broken) |
| **Train memory with RL** | [AgeMem](https://arxiv.org/abs/2601.01885) (tool-based ops) → [EMPO²](https://arxiv.org/abs/2602.23008) (exploration) → [MemFactory](https://arxiv.org/abs/2603.29493) (framework) |
| **Understand memory privacy risk** | [ADAM](https://arxiv.org/abs/2604.09747) (extraction attack) → [FSFM](https://arxiv.org/abs/2604.20300) (forgetting as defense) |
| **Unify memory ↔ skills ↔ rules** | [Experience Compression Spectrum](https://arxiv.org/abs/2604.15877) → [Externalization](https://arxiv.org/abs/2604.08224) |
| **Explore the neuroscience** | [Neuromorphic section](#neuromorphic--bio-inspired-memory) |

---

## Contents

- [Surveys \& Taxonomies](#surveys--taxonomies)
- [Memory Architectures](#memory-architectures)
- [Memory Admission \& Gating](#memory-admission--gating)
- [Retrieval \& Recall](#retrieval--recall)
- [Forgetting \& Consolidation](#forgetting--consolidation)
- [RL-Based Memory Policy](#rl-based-memory-policy)
- [Context Management](#context-management)
- [Evaluation \& Benchmarks](#evaluation--benchmarks)
- [Cognitive \& Neuroscience-Inspired](#cognitive--neuroscience-inspired)
- [Skill \& Procedural Memory](#skill--procedural-memory)
- [Multi-Agent Memory](#multi-agent-memory)
- [Memory Security \& Privacy](#memory-security--privacy)
- [Memory Economics](#memory-economics)
- [Neuromorphic \& Bio-Inspired Memory](#neuromorphic--bio-inspired-memory)
- [Adjacent Research](#adjacent-research)
- [Key Themes \& Cross-Cutting Insights](#key-themes--cross-cutting-insights)
- [Contributing](#contributing)

### Verification Legend

| Symbol | Meaning |
|--------|---------|
| ✅ | **Venue confirmed** — verified via official proceedings, OpenReview, or arXiv metadata |
| 📄 | **Self-reported** — metrics from authors' own evaluation; exercise caution |
| ⚠️ | **Unverified** — plausible claim but not independently confirmed |
| 🔬 | **Editor's synthesis** — cross-paper connection identified by the maintainer, not claimed by original authors |

---

## Surveys & Taxonomies

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [Memory in the Age of AI Agents: A Survey](https://arxiv.org/abs/2512.13564) | 47 authors | Dec 2025 | Unified taxonomy across 3 lenses: **Forms** (token/parametric/latent), **Functions** (factual/experiential/working), **Dynamics** (formation/evolution/retrieval). Distinguishes agent memory from RAG and context engineering. Hugging Face Daily Paper #1 ⚠️ (unverifiable — HF archive page returns 404). |
| [Anatomy of Agentic Memory](https://arxiv.org/abs/2602.19320) | Jiang, Li, Wei et al. | Feb 2026 | Structured taxonomy of Memory-Augmented Generation (MAG) systems. Critically analyzes empirical fragility: benchmark saturation, metric misalignment, backbone-dependent variance, overlooked latency costs. Evaluates 5 systems (LOCOMO, A-Mem, MemoryOS, Nemori, MAGMA). |
| [The Landscape of Agentic RL for LLMs](https://arxiv.org/abs/2509.02547) | Guibin Zhang et al. (Oxford, Shanghai AI Lab, NUS, UIUC, UCL) | Sep 2025 | Synthesizes 500+ works. Reframes LLMs as autonomous agents using POMDPs. Covers planning, tool use, memory, reasoning, self-improvement. |
| [From Static Templates to Dynamic Runtime Graphs](https://arxiv.org/abs/2603.22386) | Yue et al. (IBM Research) | Mar 2026 | Agentic Computation Graphs (ACGs) framework — distinguishes workflow templates, realized graphs, and execution traces. Organizes ~40 papers by when structure is determined. |
| [Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers](https://arxiv.org/abs/2603.07670) | Pengfei Du | Mar 2026 | Write–manage–read loop formalization. 3D taxonomy: temporal scope × representational substrate × control policy. Five mechanism families: context-resident compression, retrieval-augmented stores, reflective self-improvement, hierarchical virtual context, policy-learned management. Proposes vision of a "foundation model for memory control." |
| [Externalization in LLM Agents: A Unified Review of Memory, Skills, Protocols and Harness Engineering](https://arxiv.org/abs/2604.08224) | Zhou, Chai, Chen, Guo, Shan, Song, Xu et al. | Apr 2026 | Unified review across **four externalized components**: memory stores, reusable skills, interaction protocols, runtime harness. Argues modern agent capability comes from reorganizing the runtime around the model, not from changing weights. Connects memory literature with skill-discovery and protocol-design literatures that rarely cite each other. |
| [Experience Compression Spectrum: Unifying Memory, Skills, and Rules in LLM Agents](https://arxiv.org/abs/2604.15877) | Zhang, Wang, Cui, Qiu, Li, Zhu, He | Apr 2026 | Positions memory/skills/rules on a single compression axis (5–20× episodic, 50–500× procedural, 1000×+ declarative). Citation analysis of 1,136 references finds **<1% cross-community citation** between memory and skills literatures. Identifies the **"missing diagonal"** — no current system supports adaptive cross-level compression. |
| [From Storage to Experience: A Survey on the Evolution of LLM Agent Memory Mechanisms](https://arxiv.org/abs/2605.06716) | Luo, Tian, Cao, Luo et al. | May 2026 | **ACL 2026 Findings** ✅ — Maps the field's evolution from passive storage stores toward experience-centric, self-evolving memory. Companion paper-list: [Evolving-LLM-Agent-Memory-Survey](https://github.com/FeishuLuo/Evolving-LLM-Agent-Memory-Survey). |
| [Graph-based Agent Memory: Taxonomy, Techniques, and Applications](https://arxiv.org/abs/2602.05665) | Yang, Zhou, Xiao, Dong et al. | Feb 2026 | First focused taxonomy of **graph-based** agent memory: node/edge designs, construction strategies (entity-centric vs event-centric vs hybrid), retrieval (one-hop vs multi-hop vs subgraph), and update/forget operators. Useful companion to A-MEM, HeLa-Mem, GAM. |

## Memory Architectures

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [A-MEM: Agentic Memory for LLM Agents](https://arxiv.org/abs/2502.12110) | Xu, Liang, Mei, Gao, Tan, Zhang | Feb 2025 | Dynamic memory organization inspired by Zettelkasten. Creates interconnected "memory notes" with content, metadata, and explicit links. Agent autonomously decides when to create, update, or link memories. NeurIPS 2025 ✅. |
| [SYNAPSE: Episodic-Semantic Memory via Spreading Activation](https://arxiv.org/abs/2601.02744) | Jiang, Chen, Pan et al. | Jan 2026 | Memory as a dynamic graph where relevance emerges from **spreading activation** rather than pre-computed vector links. Lateral inhibition and temporal decay highlight relevant sub-graphs. Triple Hybrid retrieval. |
| [MAGMA: Multi-Graph Agentic Memory Architecture](https://arxiv.org/abs/2601.03236) | Jiang, Li, Li, Li | Jan 2026 | Multi-graph based architecture separating different memory concerns into distinct graph structures for AI agents. |
| [Mem0: Production-Ready AI Agents with Scalable Long-Term Memory](https://arxiv.org/abs/2504.19413) | Chhikara, Khant, Aryan, Singh, Yadav | Apr 2025 | Scalable memory-centric architecture with dynamic extraction, consolidation, and retrieval. Graph-based variant for complex relational structures. 26% improvement over OpenAI memory, 91% lower latency, 90%+ token savings 📄 (self-reported). Evaluated on LOCOMO. |
| [CraniMem: Neurocognitively Motivated Gated & Bounded Memory](https://arxiv.org/abs/2603.15642) | Mody, Panchal, Kar, Bhowmick, Karani | Mar 2026 | Cranial-inspired dual-store: bounded FIFO episodic buffer + knowledge graph (long-term). Goal-conditioned gating. Utility tagging (Importance + Surprise + Emotion). Beats Mem0 by +57.6% on noisy HotpotQA 📄 (self-reported; "noisy" = authors' own distractor injection, not standard benchmark). ICLR 2026 MemAgents Workshop ✅. [Code](https://github.com/PearlMody05/Cranimem) |
| [AdaMem: Adaptive User-Centric Memory](https://arxiv.org/abs/2603.16496) | — | Mar 2026 | Working, episodic, persona, and graph memories. Key innovation: **question-conditioned retrieval planning** — resolves target participant first, builds retrieval route combining semantic + relation-aware graph expansion. SOTA on LoCoMo and PERSONAMEM. |
| [PlugMem: A Task-Agnostic Plugin Memory Module](https://arxiv.org/abs/2603.03296) | Yang, Galley, Wang, Gao, Han, Zhai (Microsoft Research, UIUC) | Mar 2026 | Converts raw interactions into **propositional** (facts) + **prescriptive** (skills) knowledge, organized in a knowledge-centric memory graph. Knowledge — not entities or chunks — is the unit of memory access. Single plug-and-play module outperforms task-specific designs across 3 diverse benchmarks. Highest **information density**: more useful info per context token consumed 📄. |
| [Memora: Harmonic Memory Representation](https://arxiv.org/abs/2602.03315) | Xia, Zhang, Dixit, Harimurugan, Wang, Ruhle, Sim, Bansal, Rajmohan (Microsoft Research) | Feb 2026 | Proves that **RAG and KG memory are special cases** of this unified framework. Primary abstractions index concrete memory values; "cue anchors" expand retrieval beyond semantic similarity. New SOTA on **both** LoCoMo AND LongMemEval 📄. |
| [MemMA: Coordinating the Memory Cycle through Multi-Agent Reasoning](https://arxiv.org/abs/2603.18718) | Lin, Zhang, Lu, Liu, Tang, He, Zhang, Wang (Microsoft Research) | Mar 2026 | Multi-agent framework: Meta-Thinker → Memory Manager → Query Reasoner. **Backward path innovation**: synthesizes probe QA pairs, verifies memory, converts failures into repairs BEFORE finalizing. Plug-and-play — improves 3 different storage backends on LoCoMo. [Code](https://github.com/MinhuaLin/MemMA) |
| [H-Mem: Hybrid Multi-Dimensional Memory](https://aclanthology.org/2026.eacl-long.363/) | Ye, Huang, Chen, Zhang (Rutgers) | Mar 2026 | Organizes memory across **time AND topic** dimensions simultaneously. Mimics associative + hierarchical properties of human memory. EACL 2026 ✅. |
| [H-MEM: Hierarchical Memory for High-Efficiency Long-Term Reasoning](https://arxiv.org/abs/2507.22925) | Sun et al. | Mar 2026 | Multi-level memory storage with positional index encoding of sub-memory at each layer. Confidence-weighted retrieval — attaches memory weights to provide LLMs with uncertainty reference. Key finding: retrieval is ineffective without structured hierarchical storage. EACL 2026 ✅. |
| [GAM: Hierarchical Graph-based Agentic Memory for LLM Agents](https://arxiv.org/abs/2604.12285) | Wu, Zhang, Lin, Xu, Xu, Chen, Zou et al. | Apr 2026 | Explicitly **decouples encoding from consolidation**: an event-progression graph captures stream updates online; integration into the topic-associative network is deferred until a semantic shift is detected. Addresses the tension between stream-based fluidity and structured retention. |
| [HeLa-Mem: Hebbian Learning and Associative Memory for LLM Agents](https://arxiv.org/abs/2604.16839) | Zhu, Li, Zhang, Liu, Yang | Apr 2026 | **ACL 2026** ✅ — Bio-inspired dual-graph: (1) episodic graph evolves via Hebbian co-activation; (2) semantic store populated via **Hebbian Distillation** — a Reflective Agent identifies densely-connected hubs and distills them into reusable semantic knowledge. Beats prior SOTA on LoCoMo across 4 categories with fewer context tokens 📄. [Code](https://github.com/ReinerBRO/HeLa-Mem) |
| [LightMem: Lightweight LLM Agent Memory with Small Language Models](https://arxiv.org/abs/2604.07798) | Zhang, Zhang, Chen, Huang, Zheng et al. | Apr 2026 | **ACL 2026** ✅ — SLM-driven memory with strict online/offline separation. STM/MTM/LTM tiers with two-stage retrieval (vector coarse → semantic re-rank). **~2.5 F1 over A-MEM on LoCoMo, 83ms retrieval, 581ms end-to-end** 📄. Shows that careful SLM use can replace repeated large-model memory calls. |
| [MemMachine: Ground-Truth-Preserving Memory for Personalized AI Agents](https://arxiv.org/abs/2604.04853) | Wang, Yu, Love, Zhang, Wong, Scargall, Fan et al. | Apr 2026 | Open-source system integrating short-term, long-term episodic, and profile memory in a ground-truth-preserving pipeline. Targets multi-session degradation in standard RAG. |
| [Omni-SimpleMem: Autoresearch-Guided Lifelong Multimodal Memory](https://arxiv.org/abs/2604.01007) | Liu, Ling, Qiu, Liu, Han, Xia, Tu et al. | Apr 2026 | Uses **autonomous research-agent search** over the design space (architecture × retrieval × prompts × data pipeline) to discover effective lifelong multimodal memory configurations. The first paper to treat memory architecture itself as a search target. |
| [Human-Inspired Memory Architecture for LLM Agents](https://arxiv.org/abs/2605.08538) | Kerestecioglu, Robsky, Vasters, Sharma, Kesselman (Microsoft) | May 2026 | Biologically-grounded architecture with **six cognitive mechanisms**: sleep-phase consolidation, interference-based forgetting, **engram maturation**, **reconsolidation on retrieval**, entity knowledge graphs, hybrid multi-cue retrieval. Introduces a synthetic calibration methodology that derives all thresholds *without* benchmark exposure — eliminates a common eval-leakage source. First streaming M-tier LongMemEval eval (475 sessions). Dedup-based consolidation: 97.2% retention precision, 58% store reduction (+21.8 pp) on a 13K-issue VSCode dataset 📄. |

## Memory Admission & Gating

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [A-MAC: Adaptive Memory Admission Control](https://arxiv.org/abs/2603.04549) | Zhang et al. (Workday AI) | Sep 2025 | 5-dimension scoring: Utility (LLM call), Confidence (ROUGE-L grounding), Novelty (1 - max cosine similarity), Recency, Type Prior. Learned weights vs fixed heuristics. |
| [ACC: Agent Cognitive Compressor](https://arxiv.org/abs/2601.11653) | Bousetouane | Jan 2026 | Bio-inspired memory controller replacing transcript replay with bounded internal state updated online. Compresses agent cognitive state without losing decision-relevant context. |
| [MemReader: From Passive to Active Extraction for Long-Term Agent Memory](https://arxiv.org/abs/2604.07877) | Kang, Li, Chen, Tang, Xiong, Li | Apr 2026 | First **RL-trained active extraction policy** (vs passive transcription). MemReader-4B uses GRPO + ReAct to evaluate value/ambiguity/completeness, then chooses **WRITE / DEFER / RETRIEVE-CONTEXT / DISCARD** before admission. Integrated into MemOS. Addresses memory pollution from noisy dialogue and cross-turn dependencies. |

## Retrieval & Recall

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [xMemory: Beyond RAG for Agent Memory](https://arxiv.org/abs/2602.02007) | Hu, Zhu, Yan, He, Gui | Feb 2026 | 4-level memory hierarchy. **Key thesis: RAG ≠ agent memory.** Submodular diversity-aware retrieval (MMR) replacing naive top-k. Uncertainty-gated adaptive expansion. Theme clustering. 44.91% retroactive reassignment rate proves flat structures fail. ⚠️ Conference status unverified. |
| [SuperLocalMemory V3](https://arxiv.org/abs/2603.14588) | — | Mar 2026 | First **information-geometric foundations** for agent memory. Fisher information metric replaces cosine similarity. Riemannian Langevin dynamics for retrieval. Theoretical grounding for memory operations. |
| [ExpRAG: Retrieval-Augmented LLM Agents Learning to Learn from Experience](https://arxiv.org/abs/2603.18272) | Ferraz, Deffayet, Nikoulina, Déjean, Clinchant | Mar 2026 | Trains agents to USE retrieved trajectories in-context (retrieval-augmented fine-tuning). Standard LoRA collapses on OOD tasks; ExpRAG-LoRA generalizes to held-out hard tasks. Combines experience retrieval with fine-tuning — neither alone is sufficient. |
| [To Know is to Construct: Schema-Constrained Generation for Agent Memory (SCG-MEM)](https://arxiv.org/abs/2604.20117) | Zheng, Song, Li, Yang | Apr 2026 | Replaces dense retrieval with **schema-constrained decoding**. Piaget-inspired: assimilation (grounding into existing schemas) vs accommodation (expanding schemas with novel concepts). Solves "structural hallucination" — LLMs generating references to non-existent memory keys. Constructivist alternative to similarity-based recall. |

## Forgetting & Consolidation

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [SleepGate: Sleep-Inspired Forgetting for LLMs](https://arxiv.org/abs/2603.14517) | Xie (Kennesaw State) | Mar 2026 | Learned sleep cycle over KV cache addressing **proactive interference**. Conflict-aware temporal tagger + forgetting gate + consolidation module. Reduces interference horizon from O(n) to O(log n). 99.5% retrieval accuracy at PI depth 5 vs 23% baseline 📄 (self-reported; extraordinary gap warrants independent replication). Supersession detection via binary σ flag. |
| [SCM: Sleep-Consolidated Memory with Algorithmic Forgetting](https://arxiv.org/abs/2604.20943) | Shinde | Apr 2026 | Five components inspired by human memory: limited-capacity working memory, multi-dimensional importance tagging, **offline sleep-stage consolidation with distinct NREM and REM phases**, intentional value-based forgetting, and a computational self-model for introspection. Reports perfect 10-turn recall, **90.9% noise reduction**, sub-millisecond search 📄. Research preview. |
| [FSFM: A Biologically-Inspired Framework for Selective Forgetting of Agent Memory](https://arxiv.org/abs/2604.20300) | Gu, Xiong, Wang, Ren, Li, Zhang, Guo et al. | Apr 2026 | Grounds selective forgetting in **hippocampal indexing/consolidation theory and the Ebbinghaus curve**. Argues that in resource-constrained environments a forgetting mechanism is as crucial as retention — and that memory security depends on the agent's ability to actively drop sensitive history. |

## RL-Based Memory Policy

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [AgeMem: Agentic Memory — Learning Unified LTM and STM Management](https://arxiv.org/abs/2601.01885) | Yu, Yao, Xie, Tan, Feng, Li, Wu | Jan 2026 | Exposes store/retrieve/update/summarize/discard as **tool-based actions**. Agent learns WHEN and WHAT to do via 3-stage progressive RL + step-wise GRPO. Outperforms all heuristic-based baselines across 5 benchmarks. Key thesis: memory operations should be **learned**, not hard-coded 📄. |
| [EMPO²: Exploratory Memory-Augmented On- and Off-Policy Optimization](https://arxiv.org/abs/2602.23008) | Liu, Kim, Luo, Li, Yang | Feb 2026 | Uses memory not just for recall but for **exploring novel states**. Hybrid on/off-policy RL — **128.6% improvement** over GRPO on ScienceWorld 📄. Adapts to new tasks with just a few memory-augmented trials, zero parameter updates. ICLR 2026 ✅. |
| [MemFactory: Unified Inference & Training Framework for Agent Memory](https://arxiv.org/abs/2603.29493) | Guo, Li, Tang, Xiong, Li | Mar 2026 | "LLaMA-Factory for memory agents" — first unified modular framework. Lego-like plug-and-play memory components. Natively integrates GRPO for RL-based memory policy training. Supports Memory-R1, RMM, MemAgent paradigms out of the box. Up to 14.8% improvement over base models 📄. |
| [Memory-R2: Fair Credit Assignment for Long-Horizon Memory-Augmented LLM Agents](https://arxiv.org/abs/2605.21768) | Yan, Bahloul, Nie, Schwarzmann, Trivisonno, Tresp, Ma | May 2026 | Identifies a fundamental flaw in GRPO for memory-RL: once rollouts write different memories, they no longer share the same effective environment, so trajectory-level group comparisons are *unfair*. Introduces **LoGo-GRPO** (Local + Global) — global keeps end-to-end long-horizon reward; local re-rollouts compare memory-op outcomes from the same intermediate state. Shared-parameter co-learning for fact extractor + memory manager. Progressive curriculum 8→16→32 sessions. |
| [What Training Data Teaches RL Memory Agents: Curriculum Effects in Memory-Augmented QA](https://arxiv.org/abs/2605.23067) | He, Lin, Liu, Wu, Xie, Zhou, Xiao | May 2026 | Controlled study holding architecture/RL/hyperparams fixed and varying *only* curriculum across in-domain (LoCoMo), mixed (LoCoMo+LongMemEval), and OOD (LongMemEval). **Key findings:** curriculum is a fine-grained lever on *specialization*, not a uniform scaling factor; per-type differences dwarf aggregate differences (single-number benchmark comparisons systematically underreport); binary EM reward produces no signal at G=4 group size — continuous rewards needed for single-GPU regime. Practical RL-memory training playbook. [Code](https://github.com/EvaxHe/rl-memory-curriculum) |

## Context Management

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [The Missing Memory Hierarchy: Demand Paging for LLM Context Windows](https://arxiv.org/abs/2603.09023) | Mason (UBC / Georgia Tech) | Sep 2025 | Maps OS virtual memory concepts to LLM context: physical memory = context window, virtual memory = persistent state, page table = retrieval handles, page fault = re-request evicted content. Analyzed 857 sessions, 54,170 API calls, 4.45B effective input tokens. |

## Evaluation & Benchmarks

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [StructMemEval: Evaluating Memory Structure in LLM Agents](https://arxiv.org/abs/2602.11243) | Shutova, Olenina, Vinogradov, Sinitsin | Feb 2026 | Tests agents' ability to **organize** memory (not just retrieve). Tasks: transaction ledgers, to-do lists, trees. Key finding: LLMs don't spontaneously recognize when to apply memory structure — they succeed only when explicitly prompted. |
| [MemoryAgentBench: Evaluating Memory via Incremental Multi-Turn Interactions](https://arxiv.org/abs/2507.05257) | Hu et al. (HUST) | Jul 2025 (revised Mar 2026) | Tests 4 memory competencies in realistic incremental accumulation. Key finding: no current method masters all 4 competencies simultaneously. ICLR 2026 ✅. [Code](https://github.com/HUST-AI-HYZ/MemoryAgentBench) |
| [From Recall to Forgetting: Benchmarking Long-Term Memory for Personalized Agents (Memora + FAMA)](https://arxiv.org/abs/2604.20006) | Uddin, Shubham, Blanco, Baral, Wang (ASU) | Apr 2026 | **ACL 2026 Findings** ✅ — Introduces **Memora**, a weeks-to-months benchmark over three tasks: remembering, reasoning, recommending. Introduces **FAMA (Forgetting-Aware Memory Accuracy)** — a metric that *penalizes* reliance on obsolete or invalidated memory rather than just rewarding recall. Evaluation of 4 LLMs and 6 memory agents finds frequent reuse of invalid memories and failures to reconcile evolving knowledge. ⚠️ Not to be confused with Microsoft's *Memora: Harmonic Memory Representation* (2602.03315). |
| [STALE: Can LLM Agents Know When Their Memories Are No Longer Valid?](https://arxiv.org/abs/2605.06527) | Chao, Bai, Sheng, Li, Sun | May 2026 | Benchmark for **Implicit Conflict** — a later observation invalidates an earlier memory *without explicit negation*, requiring inference + commonsense to detect. 400 expert-validated scenarios, 1,200 queries, contexts up to 150K tokens. Three-dimensional probing: **State Resolution**, **Premise Resistance**, **Implicit Policy Adaptation**. Best frontier LLM only 55.2% overall. Companion prototype **CUPMem** uses structured state consolidation + propagation-aware search. Complements FAMA. |
| [MemoryArena: Benchmarking Agent Memory in Interdependent Multi-Session Agentic Tasks](https://arxiv.org/abs/2602.16313) | He, Wang, Zhi, Hu, Chen, Yin, Wu, Ouyang, Wang, Pei, McAuley, Choi, Pentland | Feb 2026 | Memory-Agent-Environment loop benchmark across **web navigation, preference-constrained planning, progressive information search, sequential formal reasoning**. Key result: agents near-saturated on LoCoMo **perform poorly** in MemoryArena, exposing a gap between long-context memorization benchmarks and *interdependent* agentic memory use. [Project](https://memoryarena.github.io) |

## Cognitive & Neuroscience-Inspired

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [Episodic Memory is the Missing Piece for Long-Term LLM Agents](https://arxiv.org/abs/2502.06975) | Pink et al. (UT Austin) | Feb 2025 | Position paper arguing episodic memory — supporting single-shot learning of instance-specific contexts — is the critical missing capability. Defines 5 properties: temporal, instance-specific, single-shot, inspectable, compositional. |
| [MAP: Modular Agentic Planner](https://www.nature.com/articles/s41467-025-63804-5) | Correa, Samwick, Gershman et al. (Microsoft Research, Harvard) | Oct 2023 / Nature Comms 2025 | Brain-inspired architecture decomposing planning into PFC-associated modules: conflict monitoring, state prediction, state evaluation, task decomposition, task coordination. [arXiv:2310.00194](https://arxiv.org/abs/2310.00194). |
| [SCL: Structured Cognitive Loop with Governance Layer](https://arxiv.org/abs/2511.17673) | Kim | Nov 2025 | R-CCAM: Retrieval → Cognition → Control → Action → Memory. **Soft Symbolic Control** = governance layer applying symbolic constraints to probabilistic inference. Zero policy violations, complete decision traceability. |
| [Procedural Memory Is Not All You Need](https://arxiv.org/abs/2505.03434) | Wheeler, Jeunen | May 2025 | LLMs are constrained by reliance on procedural memory (pattern-driven tasks). For "wicked" learning environments with shifting rules and ambiguous feedback, different memory types are required. ACM UMAP '25. |
| [Evaluating Theory of Mind in Multi-Agent LLM Systems](https://arxiv.org/abs/2603.00142) | Kostka, Chudziak (Warsaw UT) | Sep 2025 | ToM and Internal Belief mechanisms are NOT universally beneficial — stronger models handle extra cognitive load well, but weaker models get confused. Model capability is the dominant factor. |

## Skill & Procedural Memory

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [SkillRouter: Skill-Based Routing for LLM Agents](https://arxiv.org/abs/2603.22455) | Alibaba | Sep 2025 | **Critical finding:** skill BODY is the decisive routing signal (91.7% attention weight), NOT name (7.3%) or description (1.0%). Removing body causes 29-44pp degradation. BM25 on metadata alone scores 0%. Two-stage retrieve-and-rerank (1.2B params). |
| [EvoSkill: Self-Evolving Skill Discovery](https://arxiv.org/abs/2603.02766) | Sentient, Virginia Tech | Sep 2025 | Automates skill discovery via iterative failure analysis without model fine-tuning. Three agents: Executor, Proposer, Skill-Builder. Skill-merge outperforms single runs. [Code](https://github.com/sentient-agi/EvoSkill) |
| [Trajectory-Informed Memory Generation for Self-Improving Agent Systems](https://arxiv.org/abs/2603.10600) | Fang, Isahagian, Jayaram, Kumar, Muthusamy, Oum, Thomas (IBM Research) | Mar 2026 | Extracts **typed actionable tips** from execution trajectories: **strategy** tips (clean successes), **recovery** tips (failure-then-recovery), **optimization** tips (inefficient-but-successful). Closes the gap between episodic logs and reusable procedural knowledge — useful as a complement to EvoSkill and SkillRouter. |

## Multi-Agent Memory

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [CoMAM: Collaborative Memory for Multi-Agent Systems](https://arxiv.org/abs/2603.12631) | — | Sep 2025 | Collaborative RL framework modeling memory agents as sequential MDP with inter-agent dependencies. Group-level ranking consistency for coordinated memory operations. |
| [DCM-Agent: Dual-Cluster Memory for Multi-Paradigm Ambiguity](https://arxiv.org/abs/2604.20183) | Zhang, Wan, Zhang, Yang, Zhang, Wei, Liu | Apr 2026 | Tackles structural ambiguity in optimization problems where one problem admits multiple conflicting modeling paradigms. Training-free dual-cluster memory keeps competing paradigm solutions separated so the agent can pick or blend at inference time. Relevant to multi-agent settings where agents disagree on framing. |

## Memory Security & Privacy

> *April 2026 marks memory security emerging as a first-class research concern. As agent memories grow rich with user data, they become attack surfaces.*

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [ADAM: A Systematic Data Extraction Attack on Agent Memory via Adaptive Querying](https://arxiv.org/abs/2604.09747) | Lyu, He, Wang, Hu, Li, Chen, Li, Chen | Apr 2026 | First systematic privacy attack on agent memory. Combines **data-distribution estimation** of a victim agent's memory with **entropy-guided adaptive querying** to maximize leakage. Achieves **up to 100% Attack Success Rate** on extracting stored memories 📄 — substantially outperforming prior attacks. Establishes the need for privacy-preserving memory designs as a first-class research direction. |
| [SSGM: Stability and Safety Governed Memory for LLM Agents](https://arxiv.org/abs/2603.11768) | Lam, Li, Zhang, Zhao | Mar 2026 (rev May 2026) | Conceptual governance framework that **decouples memory evolution from execution** by enforcing consistency verification, temporal decay modeling, and dynamic access control *before* any memory consolidation. Provides a taxonomy of memory corruption risks: **topology-induced knowledge leakage**, **semantic drift via iterative summarization**, and consolidation hazards. Complementary defensive framing to ADAM. |

## Memory Economics

| Paper | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [Beyond the Context Window: Cost-Performance Analysis](https://arxiv.org/abs/2603.04814) | Pollertlam, Kornsuwannawit | Sep 2025 | Compares Mem0-style fact-based memory vs long-context LLMs on LongMemEval, LoCoMo, PersonaMemv2. **Break-even: memory system becomes cheaper after ~10 interaction turns at 100K context.** Long-context wins on factual recall but memory is competitive on reasoning. |

## Neuromorphic & Bio-Inspired Memory

> *Most agent memory research ignores 50 years of neuroscience. This section bridges that gap — presenting the biological mechanisms that may underlie what LLM memory papers have independently re-discovered (forgetting, gating, dual-phase encoding), alongside the spiking neural network implementations that model them directly. Cross-references to LLM papers below are 🔬 editor's synthesis.*

| Paper / Project | Authors | Date | Key Contribution |
|-------|---------|------|------------------|
| [A Bio-realistic Synthetic Hippocampus for Robotic Cognition](https://link.springer.com/article/10.1007/s12668-025-02229-2) | Talanov et al. | Oct 2025 | Synthetic hippocampal architecture with **dual-phase operation**: online sensorimotor encoding during wake, offline consolidation via SWR-triggered replay during sleep. SNN on neuromorphic substrates (≤1W). Goal-prioritised plasticity prevents catastrophic forgetting. Models the biological mechanisms that parallel what SleepGate and CraniMem implement in software 🔬. BioNanoScience. Open access. |
| [The Memristive Implementation of the Hippocampus: A Hypothesis](https://link.springer.com/article/10.1007/s12668-025-02124-w) | Talanov et al. | Aug 2025 | Hardware-level hippocampal memory using stochastic polycrystalline nano-fiber mesh as memristive substrate. Key insight: the **inherent randomness** of material structure mimics probabilistic biological synaptic networks. Demonstrates resistive switching tunability for implementing dynamic memory functions — bidirectional replay, synaptic up/down-scaling, consolidation. BioNanoScience. Open access. |
| [Simulation of Serotonin Mechanisms in NEUCOGAR Cognitive Architecture](https://www.sciencedirect.com/science/article/abs/pii/S2212683X15000663) | Talanov, Gafarov, Vallverdú et al. | 2018 | Maps neuromodulatory mechanisms to computational models: **dopamine → attention**, **serotonin → inhibition**. The "cube of emotions" model. Demonstrates that mammalian emotional-state control via monoamine neurotransmitters can be re-implemented computationally. Foundation for neuromodulator-gated memory admission. Procedia Computer Science. |
| [tinyHippo](https://github.com/max-talanov/tinyHippo) | Talanov | Active | CA1 + CA3 hippocampal microcircuit simulation in NEST with Izhikevich neurons. Implements **bidirectional replay**, theta-modulated encoding/retrieval phase separation, and SWR-triggered consolidation. The biological reference implementation — validates the mechanisms that Membrain engineers and SleepGate abstracts. MIT license. |
| [Membrain](https://github.com/tfatykhov/membrain) | Fatykhov | Active | Neuromorphic memory bridge using **FlyHash encoding** and BiCameralMemory SNN (Nengo/Voja learning). Hopfield-style attractor dynamics for pattern completion (tested up to 20% noise in PoC). Stochastic consolidation with SleepSignal. gRPC API for agent integration. The engineering abstraction layer between biological models (tinyHippo) and cognitive agents (Nous). |

**The Stack:** These projects form a natural hierarchy — **tinyHippo** (biological model, validates mechanisms) → **Membrain** (engineering abstraction, SNN service) → **Nous** (cognitive agent, consumes memory). The papers provide the theoretical foundation; the repos provide working implementations.

**Why this matters for agent memory 🔬:** The LLM papers in this list independently converge on mechanisms that neuroscience has studied for decades. The following correspondences are **editor's synthesis** — the LLM papers don't explicitly cite these neuroscience sources, but the structural parallels are striking:
- SleepGate's learned forgetting ↔ hippocampal SWR consolidation during sleep (Talanov 2025a)
- CraniMem's utility gating ↔ neuromodulator-gated admission (Talanov/NEUCOGAR 2018)
- A-MEM's dual-phase encoding ↔ online/offline hippocampal states (Talanov 2025a, tinyHippo)
- xMemory's hierarchical consolidation ↔ cortical-hippocampal memory transfer (Talanov 2025b)

## Adjacent Research

These papers aren't solely about agent memory but contribute relevant architectural ideas:

| Paper | Date | Relevance |
|-------|------|-----------|
| [EverMemOS](https://arxiv.org/abs/2601.02163) — Liu, Bai, Chen et al. | Jan 2026 | Self-Organizing Memory Operating System for structured long-horizon reasoning. |
| [AriGraph](https://arxiv.org/abs/2407.04363) — Anokhin, Radionov et al. | IJCAI 2025 ✅ | Knowledge Graph World Models with episodic + semantic memory. [Proceedings](https://www.ijcai.org/proceedings/2025/) |
| [Memory Matters More Than You Think](https://arxiv.org/abs/2601.04726) — Zhou, Li et al. (Renmin U.) | Jan 2026 | Event-centric memory with Logic Map for agent searching and reasoning. |

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

### 7. 🎮 RL Is Replacing Heuristic Memory Management
**Papers:** AgeMem, EMPO², MemFactory, Memory-R1

The dominant shift in 2026: from hand-coded admission/retrieval rules to **reinforcement-learned memory policies**. AgeMem exposes all memory operations as tool-based actions and learns when to use them via GRPO. EMPO² takes this further by using memory for exploration, not just recall. MemFactory provides the infrastructure to train these policies. This is the most consequential paradigm shift since the field recognized that RAG ≠ memory.

### 8. 🔒 Memory Privacy Becomes a First-Class Concern
**Papers:** ADAM, FSFM

April 2026 surfaced the first systematic memory-extraction attack (ADAM, up to 100% ASR) — and the first forgetting frameworks (FSFM) that explicitly frame *selective forgetting* as a privacy primitive, not just a retention/efficiency one. Expect memory threat-modeling, audit interfaces, and unlearning APIs to follow.

### 9. 🪜 Memory ↔ Skills ↔ Rules as a Compression Spectrum
**Papers:** Experience Compression Spectrum, Externalization in LLM Agents

The memory and skill-discovery communities have been solving the same problem (extract reusable knowledge from interaction traces) without citing each other — cross-community citation rate is **below 1%**. The Compression Spectrum reframes both as points on a single axis (5–20× → 50–500× → 1000×+ compression), and identifies the **missing diagonal**: no current system supports adaptive cross-level compression.

### 10. 🧱 Active, Constructive Memory Operations
**Papers:** MemReader (active extraction), SCG-MEM (schema-constrained generation), HeLa-Mem (Hebbian distillation)

Two paradigm shifts in April 2026: (1) **MemReader** moves extraction from passive transcription to an RL-learned WRITE/DEFER/RETRIEVE-CONTEXT/DISCARD policy. (2) **SCG-MEM** replaces dense retrieval with schema-constrained *decoding* (Piaget-style assimilation vs accommodation). Together they suggest the future of memory is generative-constructive, not retrieve-and-paste.

## Open Questions

- **How should admission gates interact with consolidation loops?** (A-MAC + SleepGate integration)
- **What's the right forgetting curve for different memory types?** (No paper addresses type-specific decay)
- **Can skill routing be unified with memory retrieval?** (SkillRouter + xMemory convergence)
- **What's the minimum viable memory architecture?** (Most papers add complexity — none simplify)
- **How should backward verification loops (MemMA probe-verify-repair) integrate with forward memory policy?** (MemMA + AgeMem convergence)
- **Can RL-learned memory policies transfer across domains?** (EMPO² shows OOD promise — but limited evaluation)
- **Can constructivist memory (schema-bound decoding, SCG-MEM) replace similarity-based retrieval?**
- **Can the "missing diagonal" be filled — adaptive cross-level compression between episodic/procedural/declarative?**
- **How robust is agent memory against systematic extraction attacks (ADAM-class threats)?**
- **What is the right interface between active extraction (MemReader) and admission gating (A-MAC)?**
- **Does Hebbian distillation (HeLa-Mem) outperform LLM-driven semantic abstraction at scale?**

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
