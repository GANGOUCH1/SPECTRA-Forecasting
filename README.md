# SPECTRA: Sparse Periodic Extraction for Conditional Time-series Retrieval Augmentation

This repository contains the layout, performance evaluations, and theoretical framework for **SPECTRA** (Sparse Periodic Extraction for Conditional Time-series Retrieval Augmentation). 

SPECTRA introduces a lightweight, end-to-end architecture that solves the scalability, memory, and latency bottlenecks of conventional Retrieval-Augmented Forecasting (RAFT) methods without compromising on predictive precision.

---

## 👥 Authors & Affiliations
*   **Elhoussaine Gangouch** (elhoussainegangouch@gmail.com) — *UM6P (Université Mohammed VI Polytechnique)*
*   **Issam Ait Yahia** — *Université Mohammed VI Polytechnique*
*   **Abdelkader El Mahdaouy** — *Mohammed VI Polytechnique University*
*   **Ismail Berrada** — *Université Mohammed VI Polytechnique*

---

## 🚀 Core Contributions

*   **Data-Domain Sparsity:** Shifts the time-series retrieval paradigm away from traditional *data-point retrieval* to *periodic-motif retrieval*.
*   **100× Storage Reduction:** Replaces dense, overlapping historical sliding windows ($O(N)$) with a highly compressed Sparse Periodic Dictionary ($O(N/L)$).
*   **10× Inference Speedup:** Achieves an inference throughput of **200 samples/second**, matching the speeds of non-retrieval linear baselines while keeping high-fidelity retrieval capacity.
*   **Mathematical Justification:** Leverages the **Nyquist-Shannon Sampling Theorem** via frequency-domain constraint rules. The learnable Spectral Extractor (Conv1D + Pooling) band-limits raw inputs to perform strided sampling without aliasing.

---

## 📊 Performance & Efficiency Benchmarks (ETTh1 Summary)

SPECTRA establishes a new **Pareto-Optimal Frontier**, yielding lower overall error thresholds compared to dense baselines while cutting operational overhead.


| Retrieval Strategy | Database Management Strategy | Evaluation MSE | Inference Latency | Throughput |
| :--- | :--- | :---: | :---: | :---: |
| **Dense RAFT** | Full Sliding History ($S = 1$) | 0.367 | 145 ms | 19 samp/s |
| **Random Sparse** | Naive Unstructured Subsampling | 0.412 | — | — |
| **SPECTRA (Ours)** | **Periodic Stride ($S = T$)** | **0.361** | **14 ms** | **200 samp/s** |

---

## 🧠 Extended Empirical Insights (From Appendix)

### 1. Robust Denoising Mechanics
Standard dense retrieval relies on raw Euclidean space metrics, making it highly sensitive to high-frequency stochastic noise. As shown via query injection experiments, SPECTRA projects values into a lower-dimensional periodic motif space, successfully filtering out anomalies and showing a shallow, linear noise degradation curve.

### 2. Manifold Topology Verification
Applying t-SNE dimensional scaling to our stored keys confirms that the embeddings form a clean, stable circular topology (**Limit Cycle**). This geometric phase coherence allows the model to interpolate smoothly and accurately across sparse historical anchors.

---

## 🛠️ Operational Architecture

