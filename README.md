<div align="center">
<h1>Unified Thinker: A General Reasoning Modular Core for Image Generation</h1>

Sashuai Zhou<sup>1,2*</sup>, Qiang Zhou<sup>2*</sup>, Jijin Hu<sup>2*</sup>, Hanqing Yang<sup>2*</sup>, Yue Cao<sup>3</sup>, Junpeng Ma<sup>4</sup>,  
Yinchao Ma<sup>2</sup>, Jun Song<sup>2†</sup>, Tiezheng Ge<sup>2</sup>, Cheng Yu<sup>2</sup>, Bo Zheng<sup>2</sup>, Zhou Zhao<sup>1†</sup><br><br><sup>1</sup>Zhejiang University &emsp;&emsp; <sup>2</sup>Alibaba Group &emsp;&emsp; <sup>3</sup>Nanjing University &emsp;&emsp; <sup>4</sup>Fudan University  <br>
<sup>*</sup> Equal contribution &emsp; <sup>†</sup> Corresponding authors
<br><br>

<a href="https://arxiv.org/abs/2601.03127"><img src="https://img.shields.io/badge/arXiv-2601.03127-b31b1b" alt="arXiv"></a> <a href="Models"><img src="https://img.shields.io/badge/Models-Coming%20Soon-9e9e9e" alt="Models Coming Soon"></a>
<a href="#"><img src="https://img.shields.io/badge/Data-HieraReason--40K%20Coming%20Soon-9e9e9e" alt="Data Coming Soon"></a>


</div>

Unified Thinker is a **task-agnostic reasoning core** for general image generation. It decouples a trainable **Thinker** (MLLM) from an image **Generator** (e.g., diffusion models), enabling **executable planning** that bridges the persistent **reasoning–execution gap** in reasoning-driven image generation and editing.

![pipeline](assets/case_page-0001.jpg)
---

## News
- Paper is now available.
- **[Planned]** Code / checkpoints / HieraReason-40K will be released soon. Stay tuned.

---

<!-- ## Abstract (Short)

Despite strong visual fidelity, open-source generative models still struggle with logic-intensive instructions. Unified Thinker introduces a modular think-then-execute architecture: the Thinker converts instructions into a **hierarchical, generator-friendly plan** (intent summary, explicit constraints, ordered sub-goals, and an executable prompt/spec), while the Generator focuses on pixel synthesis. A two-stage training recipe—**joint supervised fine-tuning** plus **execution-led dual-phase RL (GRPO)**—grounds reasoning in pixel-level feedback and improves instruction following on both **text-to-image** and **image editing** tasks. -->
<!-- --- -->

## Highlights

- **Decoupled Thinker–Generator design**: upgrade reasoning without retraining the entire generator.
- **Unified planning format** across **T2I** (creation) and **I2I** (edit-only modification).
- **HieraReason-40K**: hierarchical reasoning traces + executable enhanced prompts for cold start.
- **Dual-phase RL** with generator-in-the-loop to align plans with actual visual outcomes.
- **Cross-generator transfer**: Thinker can be plugged into different diffusion backbones.

---

## Project Status

This repository currently serves as the **project homepage**.

- [ ] Training & inference code
- [ ] Model checkpoints (Thinker / Generator adapters)
- [ ] HieraReason-40K data & processing scripts
- [ ] Reproduction scripts for benchmarks

If you would like to be notified when releases happen, please **watch** this repo.

---

## Method Overview

**Thinker (MLLM)**  
Input: instruction (+ optional reference image)  
Output: structured reasoning trace + **executable visual specification** (enhanced prompt)

**Generator (Diffusion model)**  
Input: enhanced prompt/spec (+ optional reference image for editing)  
Output: final image

Training:
1. **Stage 1 — Joint Supervised Fine-Tuning**  
   - Teach the Thinker the planning interface using HieraReason-40K  
   - Align Generator to the enhanced prompts
2. **Stage 2 — Dual-Phase Reinforcement Learning**  
   - **Phase 2.1 (Thinker RL)**: select plans that yield better images under constraint-based rewards  
   - **Phase 2.2 (Generator RL)**: improve execution fidelity with stochastic rollouts + relative advantages

<!-- ---

## Data: HieraReason-40K (Coming Soon)

We construct **HieraReason-40K**, a curated corpus that pairs complex instructions (optionally with reference images) with:
- hierarchical reasoning traces
- a final **enhanced prompt/spec** that is directly executable by downstream diffusion models

Release details (format, license, download) will be provided upon publication.

---

## Results

Unified Thinker is evaluated on four settings:
- reasoning-based text-to-image generation (e.g., **WiseBench**)
- reasoning-based image editing (e.g., **RISEBench**)
- general text-to-image generation (e.g., **PRISM**)
- general instruction-based image editing (e.g., **GEditBench**)

<!-- Please refer to the paper for full quantitative comparisons and ablations. -->

--- 
## Citation

If you find this work useful, please cite:

```bibtex
@misc{zhou2026unifiedthinker,
      title={Unified Thinker: A General Reasoning Modular Core for Image Generation}, 
      author={Sashuai Zhou and Qiang Zhou and Jijin Hu and Hanqing Yang and Yue Cao and Junpeng Ma and Yinchao Ma and Jun Song and Tiezheng Ge and Cheng Yu and Bo Zheng and Zhou Zhao},
      year={2026},
      eprint={2601.03127},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2601.03127}, 
}
