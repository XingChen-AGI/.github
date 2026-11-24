<div align="center">

# XingChen-AGI

The open-source organization of **China Telecom AI Technology Co., Ltd.**, releasing open models across large language models, multimodal, computer vision, and speech.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/XingChen-AGI/Xing4.1-Preview/blob/main/LICENSE)
[![Params 285B / 17B](https://img.shields.io/badge/Params-285B%20%2F%2017B%20active-7C3AED)](https://github.com/XingChen-AGI/Xing4.1-Preview)
[![Context 1M](https://img.shields.io/badge/Context-1M%20native-orange)](https://github.com/XingChen-AGI/Xing4.1-Preview)

---

</div>

## Who we are

**XingChen-AGI** is the open-source organization of China Telecom AI Technology Co., Ltd. We release open models across four areas:

1. **Large language models** — agent-era models that move from passive Q&A to task execution: long-context planning, multi-step reasoning, tool calling, and structured output.
2. **Multimodal models** — vision-and-language understanding, including document intelligence that turns scanned documents, PDFs, tables, formulas and charts into clean, machine-readable data.
3. **Computer vision (CV)** — models for visual understanding and perception.
4. **Speech** — models for speech recognition and spoken-language understanding.

---

## Featured project

### Xing4.1-Preview — our newest workhorse

- Repo: [GitHub](https://github.com/XingChen-AGI/Xing4.1-Preview) · [Hugging Face](https://huggingface.co/XingChen-AGI/Xing4.1-Preview) · [ModelScope](https://modelscope.cn/models/XingChen-AGI/Xing4.1-Preview) · License: Apache 2.0

**Trained end-to-end on 8,192 Ascend 910C accelerators, the open-source MindSpore framework, and an in-house training system.** A **285B-total / 17B-active Mixture-of-Experts (MoE)** model purpose-built for **agentic coding and long-horizon agent workflows**, with a **native 1M context** and an architecture co-designed around the accelerator's matrix-heavy compute profile rather than ported onto it.

| Dimension | Value |
|---|---|
| Total / Activated params | **285B / 17B** (~6% activation) |
| Architecture | MoE · MLA + DSA |
| Routed / shared experts | **256 routed experts · Top-8 active · 1 shared** |
| Context length | **1M native** (full 1M via the public API: up to 896K input / 128K output) |
| License | Apache 2.0 |
| Release date | **2026-11-23** |

**Benchmarks** — on agentic and reasoning benchmarks it sits in the same competitive band as same-class flash models: **49.7** on Claw-Eval (pass^3), **20.6** on Terminal-Bench 4.0 (GPU-sandbox tasks skipped), **45.3** on AutomationBench v1.0.6 and **50.7** on Apex-Agents v1.1. Competitor scores are taken from their public reports; the full table with notes is in the [model card](https://github.com/XingChen-AGI/Xing4.1-Preview#evaluation).

**Weights are released in PyTorch (Hugging Face Transformers) format** — the native training format is MindSpore; the weights were fully converted before release (safetensors shards), so they load directly in Transformers, SGLang and vLLM. Precision builds: [FP8](https://huggingface.co/XingChen-AGI/Xing4.1-Preview-FP8) · [NVFP4](https://huggingface.co/XingChen-AGI/Xing4.1-Preview-NVFP4).

**Native in the open ecosystem** — Xing4.1-Preview runs directly on the fine-tuning and serving integrations already merged upstream for the Xing 4 family: [**ms-swift**](https://github.com/modelscope/ms-swift) (`v4.6.0+`) and [**LLaMA-Factory**](https://github.com/hiyouga/LLaMA-Factory) (main branch) for fine-tuning, [**SGLang**](https://github.com/sgl-project/sglang) (main branch) and the official **vLLM** [plugin](https://github.com/XingChen-AGI/xing4-vllm-plugin) for serving, with [TensorRT-LLM](https://github.com/NVIDIA/TensorRT-LLM) support under upstream review. The Xing4.0 series additionally runs on [**llama.cpp**](https://github.com/ggml-org/llama.cpp) (`b12174+`) for local GGUF inference and [KTransformers](https://github.com/kvcache-ai/ktransformers), which do not apply to Xing4.1-Preview.

**Related papers:** [Xing4 Technical Report](https://arxiv.org/abs/2611.22115) · [cmHC](https://arxiv.org/abs/2611.27193)

### Xing4.0 series — our first agentic workhorse

- [GitHub](https://github.com/XingChen-AGI/Xing4.0-29B-A4B) · [Hugging Face](https://huggingface.co/XingChen-AGI/Xing4.0-29B-A4B) · [ModelScope](https://modelscope.cn/) · License: Apache 2.0

**[Xing4.0-29B-A4B](https://github.com/XingChen-AGI/Xing4.0-29B-A4B)**: a 29B / 4B-active MoE with a native 256K context (extensible to 512K), **SWE-bench Verified 75.0** and **SuperCLUE Agent 93.52** (ranked #3), open under Apache 2.0 with BF16 / FP8 / W8A8 / GGUF builds. Xing4.0 and Xing4.1 use different architectures (Xing4.1 adopts MLA + DSA), but because their upstream interfaces stay compatible, Xing4.1 reuses the merged fine-tuning and serving support listed above (llama.cpp and KTransformers remain Xing4.0-only).

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
| ModelScope | [modelscope.cn/XingChen-AGI](https://modelscope.cn/organization/XingChen-AGI) |
| AtomGit | [atomgit.com/XingChen-AGI](https://atomgit.com/XingChen-AGI) |
| Modelers | [modelers.cn/XingChen-AGI](https://modelers.cn/user/XingChen-AGI) |
| Tianyi AI Open Platform | [teleai.com.cn](https://www.teleai.com.cn/) |

---

## Get started

```bash
# clone the workhorse
git clone https://github.com/XingChen-AGI/Xing4.1-Preview.git
```

Or try the models through the OpenAI-compatible API on the [Tianyi AI open platform](https://www.teleai.com.cn/).

---

<p align="center">
<b>Built by China Telecom Artificial Intelligence Technology Co., Ltd.</b>
</p>
