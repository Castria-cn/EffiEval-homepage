---
layout: default
title: EffiEval – Efficient & Generalizable Model Evaluation
---

## 🔑 Key Takeaways
> - **能力覆盖最大化**：用 *Model Utility Index (MUI)* 选子集，保证代表性。  
> - **无需训练 & 与性能解耦**：样本选择过程不依赖模型分数，避免评估偏差。  
> - **跨模型可迁移**：用 Llama‑3.1‑8B 选出来的子集，同样适用于 Qwen、Gemma 等 17 款模型。  
> - **仅用 5 % 样本即可保持 τ > 0.9**，显著降低 GPU 评测成本。  [oai_citation:0‡MUI_Data_selection__AAAI2026_ (1).pdf](file-service://file-Rxn6UW1LPLZXPMSfje5reE)

<a id="abstract"></a>
## Abstract
{{ page.excerpt | default: "intro"}}

## 1 Introduction
随着大语言模型规模不断扩大，现有基准（如 MMLU、HELM）评测一次需数百 GPU·小时，评测成本快速飙升 …  
*（此处继续粘贴引言内容 or 摘要简写）*

## EffiEval
> **核心思想：** 

<img src="/assets/img/figures1.gif" alt="EffiEval 框架" style="max-width:100%;height:auto;display:block;margin:0 auto;">


### 2.1 Model Utility Index（MUI）
MUI 度量任务 *t* 激活的神经元占总神经元的比例：  

\[
\text{MUI}(t)=\frac{|N_\text{activated}(t)|}{N_\text{total}}
\]

### 2.2 贪心最大覆盖算法
伪代码见论文 *Algorithm 1*，复杂度 $O(k·K)$，近似比 $(1-1/e)$ …

## 3 实验



## 4 Conclusion


---

## 📜 BibTeX

```bibtex
