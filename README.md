<div align="center">
<h1 align="center"> 👉 SkillX 👈 </h1>
<b>SkillX: Automatically Constructing Skill Knowledge Bases for Agents</b>

[![Awesome](https://awesome.re/badge.svg)](https://github.com/zjunlp/SKillX) 
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
![](https://img.shields.io/github/last-commit/zjunlp/SKillX?color=green) 

<!-- <p align="center">
  <a href="https://arxiv.org/abs/2502.15589">📄arXiv</a> •
  <a href="https://x.com/zxlzr/status/1894729164609208338">𝕏 Blog</a> •
  <a href="https://huggingface.co/collections/zjunlp/SKillX-67f9faaaa518f2e00b17386b">🤗 Huggingface</a>
</p> -->

</div>

## Table of Contents

- 👀[Overview](#overview)
- 🔧[Installation](#installation)
- 🏃[Quick Start](#quick-start)
- 🎁[Acknowledgement](#acknowledgement)
- 🚩[Citation](#citation)

## 📖 Overview

**SkillX** is a fully automated framework that constructs a **reusable, plug-and-play skill knowledge base** for LLM agents from experience.

Instead of storing raw trajectories, workflows, or loosely structured reflections, SkillX distills agent experience into a **three-level skill hierarchy**:

- **Planning Skills** for high-level task organization
- **Functional Skills** for reusable tool-based subroutines
- **Atomic Skills** for execution-oriented tool usage patterns

Built with a strong backbone agent, SkillX produces a transferable skill library that can be directly plugged into weaker base agents and new environments. Across challenging long-horizon, user-interactive benchmarks such as **AppWorld**, **BFCL-v3**, and **τ2-Bench**, SkillX consistently improves both **task success** and **execution efficiency**.

<div align="center" style="width: 100%;">
  <img src="assets/overview.png" alt="Case GIF" style="width: 100%; max-width: 100%; height: auto;">
</div>

---

## Data Formats

### Trajectory Input (JSONL)

SkillX expects trajectories in the following schema:

```json
{
  "trajectory_id": "traj_001",
  "task_id": "task_001",
  "user_task": "How many songs are in my Spotify library?",
  "task_history": [
    {"role": "system", "content": "You are a helpful assistant..."},
    {"role": "assistant", "content": "I'll help you count..."},
    {"role": "user", "content": "Output:\n```\n{\"songs\": 150}\n```"}
  ],
  "reward": 1.0,
  "metadata": {}
}
```

## 🤖 Key Features

### Hierarchical Multi-Level Skill Design
SkillX transforms raw trajectories into a structured three-tier skill space:
- **Planning Skills** capture high-level decomposition and ordering
- **Functional Skills** represent reusable multi-step tool subroutines
- **Atomic Skills** encode practical tool usage constraints and patterns

### Fully Automated Skill KB Construction
SkillX provides an end-to-end automated pipeline that:
- rolls out agents on training tasks,
- extracts reusable skills from successful trajectories,
- consolidates and filters low-quality skills,
- and builds a reusable **plug-and-play skill knowledge base**.

### Iterative Skill Refinement
SkillX continuously improves the skill library through:
- **skill merging** for consolidating redundant behaviors,
- **quality filtering** for removing brittle or hallucinated skills,
- and **iterative updates** that add, modify, or keep skills based on execution feedback.

### Exploratory Skill Expansion
Beyond seed demonstrations, SkillX proactively discovers new skills by:
- identifying under-used and failure-prone tools,
- guiding environment exploration,
- synthesizing new tasks from exploratory trajectories,
- and expanding skill coverage beyond the original training distribution.

### Plug-and-Play Transfer Across Agents
The resulting skill library can be directly injected into different base agents, enabling **strong-to-weak transfer** without retraining the underlying model.

### Better Performance and Efficiency
SkillX consistently improves:
- **task success rate** on challenging benchmarks,
- **execution efficiency** by reducing unnecessary exploration and tool misuse,
- and **generalization** through structured, reusable experience abstraction.

---

## 📊 Highlights

- **~10% absolute improvement** for weaker base agents on multiple benchmarks
- Consistent gains on **AppWorld**, **BFCL-v3**, and **τ2-Bench**
- Stronger transferability than trajectory-based, workflow-based, and memory-based baselines
- Improved **execution efficiency** with fewer redundant steps
- Effective even when the skill library is built by a stronger model and used by weaker ones

---

## 🧠 Why SkillX?

Existing experience-learning methods often suffer from:

- **Isolated learning**: agents repeatedly rediscover similar behaviors
- **Weak transferability**: raw trajectories and reflections often do not generalize well
- **Capability bottlenecks**: self-extracted experience is limited by the agent’s own strength

SkillX addresses these issues by building a **structured skill knowledge base** that is:

- **reusable across tasks**
- **transferable across agents**
- **lightweight to retrieve**
- **easy to inject into prompts**
- **more robust than long-context progressive skill formats**

---

## 🏗️ Method Overview

SkillX consists of three core components:

### 1. Multi-Level Skills Extraction
From successful trajectories, SkillX automatically extracts:
- **Planning skills**: concise, reusable task plans
- **Functional skills**: reusable tool-composition procedures
- **Atomic skills**: tool-specific usage guidance, constraints, and failure notes

### 2. Iterative Skills Refinement
SkillX improves library quality through:
- **Skills Merge**: cluster and consolidate similar skills
- **Skills Filter**: remove non-portable, hallucinated, or invalid skills
- **Skills Update**: add, modify, or keep skills across iterations

### 3. Exploratory Skills Expansion
SkillX expands beyond observed demonstrations by:
- guiding exploration toward under-covered tools and failure modes,
- synthesizing new tasks from exploration,
- and rerunning extraction + refinement to grow the skill library.

---

## 📈 Main Results

SkillX improves agentic performance across multiple LLM backbones and benchmarks.

### Representative gains
- On **Qwen3-32B**, SkillX brings **around 10-point improvements** on several benchmarks
- On **Kimi-K2-Instruct-0905**, SkillX yields clear gains especially on **AppWorld**
- On **GLM-4.6**, SkillX still improves performance and execution efficiency despite the model already being strong

### Benchmarks
- **AppWorld**
- **BFCL-v3**
- **τ2-Bench**

### Key takeaway
SkillX outperforms strong experience-learning baselines such as:
- **A-Mem**
- **AWM**
- **ExpeL**
- **No-memory**

This shows that **how experience is represented** matters as much as, or more than, where it comes from.

---

## 🔍 What Makes SkillX Different?

Compared with prior experience formats:

- **Raw trajectories** are verbose and difficult to transfer
- **Insights/reflections** are often too abstract
- **Workflows** may miss low-level tool constraints
- **Claude-style skills** rely on long-context progressive disclosure and complex environment support

In contrast, SkillX offers:
- **hierarchical, itemized, reusable skills**
- **one-time prompt injection**
- **lightweight retrieval**
- **strong transfer across agents and environments**

---

## 🚀 Use Cases

SkillX is especially useful for:

- **tool-using LLM agents**
- **long-horizon task execution**
- **interactive application environments**
- **cross-agent knowledge transfer**
- **building reusable agent skill libraries from experience**

---

## 🧪 Benchmarks Used

### AppWorld
A realistic ecosystem of apps and APIs for long-horizon agent execution.

### BFCL-v3
A challenging benchmark for multi-turn function calling and tool use.

### τ2-Bench
A user-interactive benchmark focused on conversational tool-using agents.

---

## 📦 Planned Release

We will publicly release:

- the **SkillX codebase**
- the **automatically constructed skill knowledge base**
- and supporting resources for skill extraction, refinement, and retrieval

---

## 🙏 Acknowledgement
We deeply appreciate the invaluable effort contributed by our dedicated team of developers, supportive users, and esteemed industry partners: [Ant Digital Technologies, Ant Group](https://intl.antdigital.com/en).
This repository builds upon code from [ReMe](https://github.com/agentscope-ai/ReMe) and [AgentEvolver](https://github.com/modelscope/AgentEvolver). The baseline implementations are adapted from [A-MEM](https://github.com/agiresearch/a-mem), [AWM](https://github.com/zorazrw/agent-workflow-memory), and [Expel](https://github.com/LeapLabTHU/ExpeL). We sincerely thank all contributors for their outstanding work!

## 📚 Citation

If you find this work helpful, please consider citing:

```bibtex
@article{wang2026skillx,
  author     = {Chenxi Wang and 
                Zhuoyun Yu and 
                Xin Xie and 
                Wuguannan Yao and 
                Runnan Fang and 
                Shuofei Qiao and 
                Kexin Cao and 
                Guozhou Zheng and 
                Xiang Qi and 
                Peng Zhang and 
                Shumin Deng},
  title      = {SkillX: Automatically Constructing Skill Knowledge Bases for Agents},
  year       = {2026},
  eprint     = {2604.04804},
  archivePrefix = {arXiv},
  primaryClass = {cs.CL},
  url        = {https://arxiv.org/abs/2604.04804}
}
```

---
