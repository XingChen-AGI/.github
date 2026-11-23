<div align="center">
<h1>
  Xing4.1-Preview
</h1>
</div>

<p align="center"><b>Workhorse capacity at a fraction of the cost — a 285B-total / 17B-active MoE model<br>purpose-built for agentic coding and long-horizon agent workflows, with a native 1M context.</b></p>

<p align="center">
  🦉 <a href="https://github.com/XingChen-AGI/Xing4.1-Preview" target="_blank">GitHub</a> • 🤗 <a href="https://huggingface.co/XingChen-AGI/Xing4.1-Preview" target="_blank">Hugging Face</a> • 🤖 <a href="https://modelscope.cn/models/XingChen-AGI/Xing4.1-Preview" target="_blank">ModelScope</a> • 🪶 <a href="https://modelers.cn/user/XingChen-AGI" target="_blank">Modelers</a> • 🅰️ <a href="https://atomgit.com/XingChen-AGI" target="_blank">AtomGit</a> • ☁️ <a href="https://www.teleai.com.cn/" target="_blank">Tianyi AI Platform</a> • 📖 <a href="./README_zh.md">Chinese</a>
</p>

<p align="center">
  <a href="https://github.com/XingChen-AGI/Xing4.1-Preview"><img alt="Parameters" src="https://img.shields.io/badge/Params-285B%20%2F%2017B%20active-7C3AED"></a>
  <a href="https://github.com/XingChen-AGI/Xing4.1-Preview"><img alt="Context" src="https://img.shields.io/badge/Context-1M%20native-orange"></a>
  <a href="https://github.com/XingChen-AGI/Xing4.1-Preview/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-blue"></a>
</p>

# Table of Contents

- [Introduction](#introduction)
- [News](#news)
- [Model](#model)
- [Evaluation](#evaluation)
- [Quickstart](#quickstart)
- [Use Cases](#use-cases)
- [Disclaimer](#disclaimer)
- [License & Citation](#license--citation)

# Introduction

**Xing4.1-Preview** is the newest large language model in the [Xing series](https://huggingface.co/XingChen-AGI) (formerly [TeleChat](https://github.com/Tele-AI/TeleChat3)), developed by China Telecom AI Technology Co., Ltd.

- **Agentic coding and long-horizon agent tasks** — purpose-built for work that requires sustained progress, multi-step reasoning, and many turns of interaction: planning across long contexts, tool calling, and structured output.
- **285B total / 17B active (MoE)** — frontier-class capability at roughly 17B-class serving cost.
- **Native 1M context** — served in full by the public API (up to 896K input / 128K output per request).
- **Fully in-house training stack** — trained end-to-end on domestic accelerators with an in-house training framework; the architecture was co-designed around the accelerator's matrix-heavy compute profile from the ground up.
- **Deep thinking, structured output, and function calling** — a toggleable thinking mode (no effort tiers), schema-guided structured output, and function calling through an OpenAI-compatible interface.

This is a **preview release**: open weights and the API are available now. Benchmark results are in [Evaluation](#evaluation), and the technical report is published as [arXiv 2611.22115](https://arxiv.org/abs/2611.22115).

# News

- 2026-11-23 Open-sourced **Xing4.1-Preview** [[HuggingFace](https://huggingface.co/XingChen-AGI/Xing4.1-Preview) | [ModelScope](https://modelscope.cn/models/XingChen-AGI/Xing4.1-Preview) | [Tianyi AI Platform](https://www.teleai.com.cn/)]

# Model

The architecture of **Xing4.1-Preview**:

| | Attention Type | Attention Sparsity | Routed Experts | Active Experts per Token | Shared Experts | Total / Active Params | Context Length |
|---|---|---|---|---|---|---|---|
| Xing4.1-Preview | MLA | DSA | 256 | Top-8 | 1 | 285B / 17B | 1M native |

Key design choices:

- **DSA (Dynamic Sparse Attention)** reduces long-context attention cost and memory traffic while keeping matrix multiplication — what the training accelerators do best — at the center of the computation graph.
- **A wider, shallower network** raises the arithmetic intensity and data-reuse efficiency of core matmul operators while cutting per-layer serial overhead.
- **MLA + DSA** jointly shrink the KV cache and the traffic that reads it, relieving the memory-bandwidth bottleneck for long sequences.
- **Co-designed training infrastructure** — sharded-data-parallel communication optimization, a distributed Muon optimizer with cross-replica deduplication, DSA long-sequence system optimizations, and fine-grained selective recomputation — lifts end-to-end training throughput by **~15–30%**, with the largest gains on long sequences.

# Evaluation

Xing4.1-Preview is evaluated on agentic and reasoning benchmarks against same-class flash models:

| Benchmark | Xing4.1-Preview | Hy4-flash | GLM-5.3-Flash | Deepseek-v4-flash-0731 |
|---|---:|---:|---:|---:|
| Terminal-Bench 4.0 | **20.6**† | 19.2 | 35.4 | 7.0 |
| AutomationBench v1.0.6 | **45.3** | 52.2 | 48.4 | 37.7 |
| Apex-Agents v1.1 | **50.7** | 63.1 | 51.5 | 55.3 |
| HLE w/ tools | **45.7**‡ | 55.2 | 52.2 | 51.5 |
| Claw-Eval (pass^3) | **49.7** | — | — | 49.3 |

Notes:

1. For all models other than Xing4.1-Preview, each score is taken from that model's public report.
2. † Terminal-Bench 4.0: GPU sandbox tasks were skipped for Xing4.1-Preview.
3. ‡ HLE: Xing4.1-Preview was evaluated on text-only data only.

The comparison set covers agentic execution, tool use, and general reasoning, and results vary by task — we recommend judging fitness on the workloads that match your use case rather than on a single aggregate.

# Quickstart

Xing4.1-Preview is available through an OpenAI-compatible API on the [Tianyi AI open platform](https://www.teleai.com.cn/).

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_API_KEY",
    base_url="https://api-maas.teleai.com.cn/v1",
)

response = client.chat.completions.create(
    model="Xing4.1-Preview",
    messages=[
        {"role": "user", "content": "Write a single-file HTML page for a team-building cost estimator with live totals."}
    ],
)

print(response.choices[0].message.content)
```

- **Context window**: the public API serves the full **1M** context (up to **896K** input / **128K** output per request).
- **Thinking mode**: supported as an on/off toggle (no effort tiers).
- **Structured output & function calling**: supported through the OpenAI-compatible interface.

**Recommended parameters:** `temperature=0.8`, `top_p=1.0`, `max_tokens=128K`.

## Self-hosting

> [!NOTE]
> Xing4.1-Preview uses the Xing 4 family's serving stack. Replace `${MODEL_PATH}` with a local path or the hub id `XingChen-AGI/Xing4.1-Preview`. As a 285B BF16 MoE (~521 GiB), the weights alone need roughly **8×80 GB** GPUs at `--tensor-parallel-size 8`, and longer contexts need proportionally more. The native context is 1M — set the context flags (`--max-model-len` / `--context-length`) to what your hardware can hold. Parser identifiers and prebuilt image tags follow the official deployment guide in this repository.

**vLLM** — official out-of-tree plugin ([XingChen-AGI/xing4-vllm-plugin](https://github.com/XingChen-AGI/xing4-vllm-plugin)):

```bash
vllm serve ${MODEL_PATH} \
    --host 0.0.0.0 \
    --port 8000 \
    --served-model-name Xing4.1-Preview \
    --tensor-parallel-size 8 \
    --trust-remote-code \
    --gpu-memory-utilization 0.90 \
    --max-num-seqs 4 \
    --enable-auto-tool-choice \
    --reasoning-parser xing4_0 \
    --tool-call-parser xing4_0
```

**SGLang** — native support in the main branch:

```bash
sglang serve --model-path ${MODEL_PATH} \
    --trust-remote-code \
    --host 0.0.0.0 \
    --port 8000 \
    --served-model-name Xing4.1-Preview \
    --tp-size 8 \
    --mem-fraction-static 0.90 \
    --max-running-requests 4 \
    --reasoning-parser xing4_0 \
    --tool-call-parser xing4_0
```

Once started, the OpenAI-compatible endpoint is available at `http://localhost:8000/v1`.

# Use Cases

- **Agentic collaborative work** — multi-step office workflows, cross-tool orchestration, and report generation that reconciles multiple conflicting sources.
- **Deep research** — sustained, multi-source investigation with structured, auditable deliverables.
- **Agentic coding** — complete frontend generation (single-file, zero-dependency, offline-runnable web apps), 3D and creative coding, and data-analysis pipelines.
- **Document-heavy back-office** — schema-guided structured extraction for business systems.

# Disclaimer

Like all generative language models, Xing4.1-Preview can produce inaccurate or unexpected outputs. Outputs are generated automatically and do not represent the views of China Telecom. Verify important information independently. Do not use the model for any purpose that violates applicable laws and regulations.

# License & Citation

Weights and code in this repository are released under the [Apache 2.0 License](./LICENSE).

## Citation

```bibtex
@misc{lab2026telechatxing4advancingfrontier,
      title={TeleChat to Xing4: Advancing Frontier Agentic Models on Domestic Chips and Frameworks}, 
      author={Xingchen AGI Lab and Baotian Hu and Bingkai Yang and Boyang Wang and Changzai Pan and Chao Lyu and Chao Wang and Chen Li and Chenshuo Pan and Chenyu Lin and Chenyuan Zhang and Chongming Liu and Dawei Fan and Di Wu and Dong Guo and Dong Li and Dongfang Li and Enlin Liu and Fanye Xiao and Fengkai Li and Fubei Yao and Gang Lin and Han Gao and Hanming Wu and Haowei He and Huapeng Liu and Hua Wang and Huinan Xu and Jiahong Xiong and Jiaxin Peng and Jianxiang Ma and Jianxing Zhuge and Jie Zhang and Ji Xiong and Jinglin Chen and Jingqi Li and Jingxuan Li and Jiwang Ye and Junchen Li and Junbiao Li and Junyang Wu and Kaidong Yu and Kaipeng Jia and Kehai Chen and Kuai Li and Laobin Liu and Lei Li and Libo Qin and Lingling Shi and Luwen Pu and Menghao Xu and Mengjiao Bao and Mengqi Chen and Min Zhang and Mingrui Wang and Naying Wang and Peicong Han and Peiming Guo and Pengfei Li and Qiang Feng and Qi Wang and Qingjun Zhu and Qingli Li and Qitai Ding and Qiyi Xie and Quanchao Zhao and Rongbao Han and Rui Xue and Ruiyu Fang and Ruiting Song and Shijie Li and Shiquan Wang and Shuangyong Song and Sishi Xiong and Teng Su and Wankang Bao and Weijie Zhang and Wei Mao and Weiwei Fu and Weiyang Huang and Wenmin Deng and Wenqing Hu and Wujie Zhong and Xi Yu and Xiaohui Hu and Xiaomin Fang and Xiaomeng Huang and Xiaoqiong Shi and Xiaotong Shang and Xiaoyu Li and Xinglei Xu and Xin Jiang and Xin Wang and Xin Zhang and Xinzhang Liu and Xue Liu and Xuefeng Bai and Xuewei He and Yahan Li and Yanhan Zhang and Yanlei Xue and Yanzhang Wu and Yang Yu and Yi Liu and Yin Zhang and Yingyan Li and Yitong Yao and Yixuan Li and Yongqiang Xia and Yongxiang Li and Yinzhou Zhu and Yu Zhao and Yuhao Jiang and Yunpeng Zhang and Yuting Lin and Yuxuan Wu and Yuyao Huang and Yuyi Wang and Zebo Peng and Zhenwu Pei and Zhenxiong Li and Zhao Wang and Zhaoxi Zhang and Zhihao Yang and Zhiqiang Dong and Zhiwei Yan and Zhilong Lu and Zhonghao Guo and Zhongheng Wu and Zhongjiang He and Zhongqiu Li and Zhu Yuan and Zhuoru Jiang and Zhuoyi Wei and Zijia Guo and Zilu Huang and Zhipeng Guo and Zirui Li and Zihan Wang},
      year={2026},
      eprint={2611.22115},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2611.22115}, 
}
```

---

<p align="center">
  <b>Built by China Telecom AI Technology Co., Ltd.</b><br>
  <a href="https://github.com/XingChen-AGI">XingChen-AGI Open-Source Organization</a>
</p>
