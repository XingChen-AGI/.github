<div align="center">

# ⭐ XingChen-AGI · 星辰开源

### From "answering questions" to "getting things done" — 让百亿参数模型从"会回答"变成"会做事"

The open-source organization of **China Telecom AI Technology Co., Ltd. (中电信人工智能科技)**，
building agent-era large language models and multimodal document intelligence on a **fully domestic stack**.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/XingChen-AGI/Xing4.0-29B-A4B/blob/main/LICENSE)
[![SWE-bench Verified 75.0](https://img.shields.io/badge/SWE--bench%20Verified-75.0-brightgreen)](https://github.com/XingChen-AGI/Xing4.0-29B-A4B)
[![Context 256K](https://img.shields.io/badge/Context-256K%20%E2%86%92%20512K-orange)](https://github.com/XingChen-AGI/Xing4.0-29B-A4B)
[![HuggingFace](https://img.shields.io/badge/HF-XingChen--AGI-yellow)](https://huggingface.co/XingChen-AGI)
[![ModelScope](https://img.shields.io/badge/ModelScope-XingChen--AGI-blue)](https://modelscope.cn/)

---

</div>

## 🌱 Who we are

**XingChen-AGI** is the open-source organization of China Telecom AI Technology Co., Ltd. We focus on two things:

1. **Agent-era large language models** that move from *passive Q&A* to *task execution* — long-context planning, multi-step reasoning, tool calling, and structured output.
2. **Multimodal document intelligence** that turns scanned documents, PDFs, tables, formulas and charts into clean, machine-readable data.

---

## 🚀 Flagship project

### Xing4.0-29B-A4B — our agentic flagship

[![GitHub](https://img.shields.io/badge/GitHub%20Repo-Xing4.0--29B--A4B-181717?logo=github)](https://github.com/XingChen-AGI/Xing4.0-29B-A4B)
[![HuggingFace](https://img.shields.io/badge/HF-XingChen--AGI%2FXing4.0--29B--A4B-yellow)](https://huggingface.co/XingChen-AGI/Xing4.0-29B-A4B)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue)](https://github.com/XingChen-AGI/Xing4.0-29B-A4B/blob/main/LICENSE)

A **Mixture-of-Experts (MoE)** model trained on Huawei Ascend superclusters with the **MindSpore** framework — natively domestic, from silicon to software, with **no PyTorch dependency** in training.

| Dimension | Value |
|---|---|
| Total / Activated params | **29B / 4B** (activated ratio ~13.8%) |
| Architecture | MoE · mHC + MLA + MTP |
| Context length | Native **256K**, extensible to **512K** |
| Training corpus | **1.5 trillion** high-quality bilingual tokens |
| Quantization | BF16 / FP8 / INT4 — 4-bit runs in **~15GB VRAM** (RTX 3090 / 4090) |
| License | Apache 2.0 |

**Benchmarks**

- **SWE-bench Verified 75.0** — a flagship code-agent score
- **SuperCLUE Agent 93.52** (ranked **#3**)
- Integrates with **LLaMA-Factory, vLLM, SGLang, OpenCode, Claude Code** out of the box

**Everything on one card.** From *intent understanding* to *multi-step planning* to *tool invocation* — built to ship real work, not just chat.

- 🧩 [Xing4.0-plugin](https://github.com/XingChen-AGI/Xing4.0-plugin) — load & serve Xing4.0-29B-A4B in **vLLM** as an out-of-tree plugin
- 🗣 [CMPA-SLU](https://github.com/XingChen-AGI/CMPA-SLU) — spoken-language understanding research code

---

## 🧠 Also on our radar: TeleOCR

A compact (≈1.2B) document-parsing VLM (formerly *NaviDC-OCR*) that robustly parses **complex layouts, tables, formulas and scientific charts** — including distorted real-world captures.

- **OmniDocBench V1.6 — #1** with **96.87**
- **Wild-OmniDocBench — 88.53**
- **ICDAR 2026 Sci-Chart Document Mining Challenge — Winner**

Weights & code are open-sourced on [HuggingFace](https://huggingface.co/XingChen-AGI) and [GitHub](https://github.com/caipeng328/TeleOCR).

---

## 🛠 Why build on XingChen-AGI

- **🇨🇳 Fully domestic pipeline** — Ascend training → MindSpore → self-developed architecture → domestic inference (Ascend / Hygon / Moore Threads…). "**Native domestic**", not "ported to domestic".
- **💰 Cost-efficient MoE** — ~15GB VRAM inference on a single consumer GPU; only 4B params activated per token.
- **🔓 Open & auditable** — Apache-2.0 weights (BF16 / FP8 / INT4), open inference code, official integration docs.
- **🏢 Enterprise-grade** — trusted engineering for real production workloads.

---

## 🌐 Where to find us

| Platform | Handle |
| --- | --- |
| GitHub (here) | `XingChen-AGI` |
| Hugging Face | [huggingface.co/XingChen-AGI](https://huggingface.co/XingChen-AGI) |
| ModelScope (魔搭) | `XingChen-AGI` |
| Gitee / Modelers / AtomGit | `XingChen-AGI` |
| Tianyi AI Open Platform (天翼AI开放平台) | [teleai.com.cn](https://www.teleai.com.cn/) |

---

## ✨ Get started in minutes

```bash
# clone the flagship
git clone https://github.com/XingChen-AGI/Xing4.0-29B-A4B.git
cd Xing4.0-29B-A4B

# serve it with vLLM via our official plugin
cd ../Xing4.0-plugin && pip install .
```

Or try it on the [Tianyi AI open platform](https://www.teleai.com.cn/) (天翼AI开放平台).

---

<p align="center">
<i>Let's bring open models into real production — together with developers, researchers and enterprises.</i><br/>
<b>Built by 中电信人工智能科技（北京）有限公司</b> · Made with ❤️ for the open-source community
</p>

> AI生成
