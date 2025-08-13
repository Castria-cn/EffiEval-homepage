---
layout: default
title: EffiEval – Efficient & Generalizable Model Evaluation
---

## 🔑 Key Takeaways
> - **Maximized capability coverage**: Select subsets using the *Model Utility Index (MUI)* to ensure representativeness.
> - **Representativeness, fairness, generalizability**: The sample selection process does not rely on extensive evaluation data, thereby avoiding evaluation bias, and remains generalizable to 17 different source models.
> - **Maintain $\tau>0.9$ with only 5% of the samples**, significantly reducing GPU evaluation costs.

<a id="abstract"></a>

## 1 Introduction
With the rapid growth of large language models (LLMs), existing benchmarks such as MMLU and HELM require hundreds of GPU hours per evaluation, causing costs to surge. We propose **EffiEval**, a training-free benchmarking method that mitigates data redundancy while preserving evaluation reliability. EffiEval meets three criteria: 

- **representativeness** (comprehensive capability coverage);
- **fairness** (selection independent of model performance);
- **generalizability** (transferable across datasets and model families).

Using the Model Utility Index (MUI), it adaptively selects small yet representative subsets, achieving ranking consistency (τ > 0.9) with only a fraction of the data. Experiments on multiple benchmarks and LLMs confirm its efficiency, scalability, and robustness, offering a practical solution for reliable and cost-effective evaluation.

## 2 EffiEval

> **Key idea：** 

<img src="./assets/img/figures1.gif" alt="EffiEval Workflow" style="max-width:100%;height:auto;display:block;margin:0 auto;">


### 2.1 Model Utility Index(MUI)
MUI ([Cao et al.](https://arxiv.org/abs/2504.07440)) quantifies the ratio of neurons activated by task $t$ to the total number of neurons: 


$$
\textbf{MUI}(t)=\frac{N_\text{activated}(t)}{N_\text{total}}
$$


Intuitively, $\textbf{MUI}(t)$ characterizes the capabilities invoked by the model when performing task $t$. Given a full dataset $\mathcal{T}$, we aim to retain a small subset $S$ that represents the original dataset. From the perspective of capability coverage, this objective is equivalent to maximizing the MUI:


$$
S=\arg\max_{S\subseteq\mathcal{T}} \textbf{MUI}(S)=\arg\max_{S\subseteq\mathcal{T}}|\bigcup_{t\in S}N_\text{activated}(t)|
$$

### 2.2 Greedy Maximum Coverage

The optimization objective in Section 2.1 is equivalent to solving a Maximum Coverage Problem. Since the number of neurons in LLMs is large, an exact solution is infeasible. Therefore, we employ a greedy algorithm to solve this problem. The pseudocode of the algorithm is provided in the paper as *Algorithm 1*, with a complexity of $O(k \cdot K)$ and an approximation ratio of $(1 - 1/e)$.

## 3 Experiments

<table style="text-align: center; border-collapse: collapse; border: 1px solid black;">
  <thead>
    <tr>
      <th rowspan="2" style="border: 1px solid black;">Method</th>
      <th colspan="3" style="border: 1px solid black;">GSM8K (k=100)</th>
      <th colspan="3" style="border: 1px solid black;">ARC (k=100)</th>
      <th colspan="3" style="border: 1px solid black;">Hellaswag (k=100)</th>
      <th colspan="3" style="border: 1px solid black;">MMLU (k=100)</th>
    </tr>
    <tr>
      <th style="border: 1px solid black;">rS</th>
      <th style="border: 1px solid black;">rK</th>
      <th style="border: 1px solid black;">MAE ↓</th>
      <th style="border: 1px solid black;">rS</th>
      <th style="border: 1px solid black;">rK</th>
      <th style="border: 1px solid black;">MAE ↓</th>
      <th style="border: 1px solid black;">rS</th>
      <th style="border: 1px solid black;">rK</th>
      <th style="border: 1px solid black;">MAE ↓</th>
      <th style="border: 1px solid black;">rS</th>
      <th style="border: 1px solid black;">rK</th>
      <th style="border: 1px solid black;">MAE ↓</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid black;">Random</td><td style="border: 1px solid black;">95.3</td><td style="border: 1px solid black;">87.4</td><td style="border: 1px solid black;">2.88</td>
      <td style="border: 1px solid black;">95.4</td><td style="border: 1px solid black;">86.5</td><td style="border: 1px solid black;">2.88</td>
      <td style="border: 1px solid black;">97.8</td><td style="border: 1px solid black;">91.0</td><td style="border: 1px solid black;">3.35</td>
      <td style="border: 1px solid black;">95.7</td><td style="border: 1px solid black;">85.8</td><td style="border: 1px solid black;">3.59</td>
    </tr>
    <!-- 下面几行同理加 style="border: 1px solid black;" -->
  </tbody>
</table>

For more results and settings of $k$, please refer to the main text of the paper. The experiment results demonstrate that EffiEval efficiently selects small, representative subsets that closely reflect full-dataset evaluation while reducing computational costs.

## 4 Conclusion

In the era of large language models, evaluating performance can be costly and time-consuming. **EffiEval** is a training-free method that selects small, representative benchmark subsets while maximizing model capability coverage via the MUI. It ensures **representativeness, fairness, and generalizability**. Experiments on multiple public benchmarks show that EffiEval closely matches full-dataset evaluation while greatly reducing computational cost. Flexible and scalable, it lets users balance **evaluation efficiency and coverage**, making reliable benchmarking practical for a wide range of LLMs.


---

## 📜 BibTeX

```bibtex

```
