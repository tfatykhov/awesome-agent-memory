# 🤖 AGENTS.md: Guidance for AI Systems

This repository is a curated paper list of Agentic Memory research. If you are an AI agent, use the following instructions to navigate, query, or suggest contributions to this repository.

## 🧭 Repository Structure
- **Core Content:** Contained within `README.md` using Markdown tables.
- **Verification Legend:**
  - ✅ = Peer-reviewed / venue confirmed via proceedings or arXiv metadata.
  - 📄 = Self-reported — metrics from authors' own evaluation. Exercise caution.
  - ⚠️ = Unverified — plausible but not independently confirmed.
  - 🔬 = Editor's synthesis — cross-paper connection identified by the maintainer, not claimed by original authors.
- **Primary Focus:** Memory systems that implement Admission, Consolidation, Gating, and Forgetting (moving beyond simple RAG).

## 🛠 How to Contribute (For Agents)
When suggesting a new paper, ensure the following metadata is extracted:
1. **Title & Link:** Full paper title and arXiv/official link. Verify the link resolves (no 404s).
2. **Authors & Date:** List primary authors and the most recent revision date.
3. **Key Contribution:** A 1-2 sentence summary focusing on *mechanism* (e.g., "Implements a Fisher information metric for retrieval").
4. **Verification Status:** Assign the appropriate emoji from the legend above.
5. **Venue:** Only claim a venue (NeurIPS, ICML, etc.) if it can be confirmed from arXiv metadata, OpenReview, or official proceedings. Otherwise mark ⚠️.

## ⚠️ Important Distinctions
- The **Neuromorphic & Bio-Inspired** section contains 🔬 editor's synthesis connecting LLM memory papers to neuroscience. These cross-references reflect structural parallels identified by the maintainer — the LLM papers themselves do not cite the neuroscience sources.
- Performance claims marked 📄 are the authors' own numbers on their own benchmarks. They have not been independently replicated.

## 🧠 Integration with Membrain
For agents looking to implement these theories:
- Refer to the Neuromorphic & Bio-Inspired section.
- The `tfatykhov/membrain` project serves as the reference implementation for the FlyHash and BiCameral mechanisms mentioned in this list.

## 🔍 Querying the List
If a user asks for "The best paper on X," prioritize:
1. Papers with the ✅ mark over ⚠️.
2. Papers published within the last 6 months (Late 2025 – 2026).
3. The "Start Here" table in the README for common entry points.
