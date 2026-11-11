<div align="center">

# XingChen-AGI

The open-source organization of **China Telecom AI Technology Co., Ltd.**, building agent-era large language models and multimodal document intelligence.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/XingChen-AGI/Xing4.0-29B-A4B/blob/main/LICENSE)
[![SWE-bench Verified 75.0](https://img.shields.io/badge/SWE--bench%20Verified-75.0-brightgreen)](https://github.com/XingChen-AGI/Xing4.0-29B-A4B)
[![Context 256K](https://img.shields.io/badge/Context-256K%20%E2%86%92%20512K-orange)](https://github.com/XingChen-AGI/Xing4.0-29B-A4B)

---

</div>

## Who we are

**XingChen-AGI** is the open-source organization of China Telecom AI Technology Co., Ltd. We focus on two things:

1. **Agent-era large language models** that move from passive Q&A to task execution — long-context planning, multi-step reasoning, tool calling, and structured output.
2. **Multimodal document intelligence** that turns scanned documents, PDFs, tables, formulas and charts into clean, machine-readable data.

---

## Flagship project

### Xing4.0-29B-A4B — our agentic flagship

- Repo: [GitHub](https://github.com/XingChen-AGI/Xing4.0-29B-A4B) · [Hugging Face](https://huggingface.co/XingChen-AGI/Xing4.0-29B-A4B) · [ModelScope](https://modelscope.cn/) · License: Apache 2.0

A **Mixture-of-Experts (MoE)** model — trained end-to-end on a fully in-house stack, from silicon to software.

| Dimension | Value |
|---|---|
| Total / Activated params | **29B / 4B** (activated ratio ~13.8%) |
| Architecture | MoE · mHC + MLA + MTP |
| Context length | Native **256K**, extensible to **512K** |
| Training corpus | **1.5 trillion** high-quality bilingual tokens |
| Quantization | BF16 / FP8 / INT4 — 4-bit runs in **~15GB VRAM** (RTX 3090 / 4090) |

**Benchmarks**

- **SWE-bench Verified 75.0** — a flagship code-agent score
- **SuperCLUE Agent 93.52** (ranked **#3**)

**Native upstream support, merged into the mainlines:**

- **llama.cpp** ([#31589](https://github.com/ggml-org/llama.cpp/pull/31589), **b12174+**) — mainline GGUF inference on CPU / CUDA with zero new ggml operators
- **SGLang** ([#39793](https://github.com/sgl-project/sglang/pull/39793)) — native serving support
- **Training**: ms-swift ([#10275](https://github.com/modelscope/ms-swift/pull/10275)) and LLaMA-Factory ([#10754](https://github.com/hiyouga/LlamaFactory/pull/10754)) merged
- **vLLM** — via the official plugin ([Xing4.0-plugin](https://github.com/XingChen-AGI/Xing4.0-plugin)); also integrates with OpenCode, Claude Code
- **More**: GPTQModel, MLX (mlx-vlm / unsloth-zoo), PocketLLM, LocalAI GGUF gallery, RelicLLM (NPU GGUF)

Related work:

- [Xing4.0-plugin](https://github.com/XingChen-AGI/Xing4.0-plugin) — load and serve Xing4.0-29B-A4B in vLLM as an out-of-tree plugin
- [CMPA-SLU](https://github.com/XingChen-AGI/CMPA-SLU) — spoken-language understanding research code

---

### Xing4.0-29B-Intent — schema-guided structured output

- [GitHub](https://github.com/XingChen-AGI/Xing4.0-29B-Intent) · [Hugging Face](https://huggingface.co/XingChen-AGI/Xing4.0-29B-Intent) · [ModelScope](https://modelscope.cn/models/XingChen-AGI/Xing4.0-29B-Intent) · License: Apache 2.0

A task-specific model for **schema-guided intent recognition and structured information extraction** — turns natural language into structured JSON for business systems: intelligent assistants, request routing and document extraction.

- **Four tasks in one model**: intent recognition & slot filling · named entity recognition · relation extraction · event extraction — unified `category + args` output, configured by schema
- **Top overall score (58)** ahead of Gemini-3.6-Flash (49), Qwen3.8-Max (46) and GPT-5.6-Sol (45) — **best on 5 of 6 metrics**
- **Companion dataset**: 2.75M samples unifying 61 public datasets in one schema-guided format (4 task types · 19 domains · 52 languages)
- [XingIntent SDK](https://github.com/XingChen-AGI/Xing4.0-29B-Intent/tree/main/XingIntentSDK) — schema-driven training and structured inference tooling
- Precision build: [FP8](https://huggingface.co/XingChen-AGI/Xing4.0-29B-Intent-FP8)

---

## TeleOCR

A compact (~1.2B) document-parsing VLM (formerly *NaviDC-OCR*) that robustly parses complex layouts, tables, formulas and scientific charts — including distorted real-world captures.

- **OmniDocBench V1.6 — #1** with **96.87**
- **Wild-OmniDocBench — 88.53**
- **ICDAR 2026 Sci-Chart Document Mining Challenge — Winner**

Weights & code are open-sourced on [Hugging Face](https://huggingface.co/XingChen-AGI) and [GitHub](https://github.com/caipeng328/TeleOCR).

---

## Where to find us

| Platform | Handle |
| --- | --- |
| GitHub (here) | `XingChen-AGI` |
| Hugging Face | [huggingface.co/XingChen-AGI](https://huggingface.co/XingChen-AGI) |
| ModelScope | `XingChen-AGI` |
| Gitee / Modelers / AtomGit | `XingChen-AGI` |
| Tianyi AI Open Platform | [teleai.com.cn](https://www.teleai.com.cn/) |

---

## Get started

```bash
# clone the flagship
git clone https://github.com/XingChen-AGI/Xing4.0-29B-A4B.git
cd Xing4.0-29B-A4B

# serve it with vLLM via our official plugin
cd ../Xing4.0-plugin && pip install .
```

Or try it on the [Tianyi AI open platform](https://www.teleai.com.cn/).

---

<p align="center">
<b>Built by China Telecom Artificial Intelligence Technology Co., Ltd.</b>
</p>
