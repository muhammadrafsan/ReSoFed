<h1 align="center">
ReSoFed: Reliability-Guided Model Souping for Robust Federated Learning in Heterogeneous Classroom Environments
</h1>

<p align="center">
  <strong>Official implementation of the paper [CVPR 2026 Workshop]</strong>
</p>

> **ReSoFed** is a privacy-preserving federated learning framework that improves robustness under heterogeneous conditions using reliability-guided model aggregation.

📄 **Paper**: Coming Soon  
📦 **Code**: https://github.com/muhammadrafsan/ReSoFed   
📊 **Dataset**: SCB (Student Classroom Behavior)

---

## Overview

Computer vision systems are increasingly used in educational environments for tasks like classroom activity recognition and student engagement analysis. However:

- 🔒 **Data privacy constraints** prevent centralized training  
- 🌍 **Heterogeneous environments** (lighting, camera, viewpoints) create non-IID data  
- ⚠️ Standard FL methods (e.g., FedAvg) suffer from **negative transfer**

👉 To address this, we propose **ReSoFed**, a **reliability-guided federated aggregation framework**.

---

## Key Idea

Instead of treating all clients equally, **ReSoFed** evaluates how well each client generalizes across domains, and:

1. Selects only reliable clients (via greedy model souping)  
2. Assigns higher weights to better generalizing models  

---

## Methodology


<p align="center">
<img width="1122" height="480" alt="image" src="https://github.com/user-attachments/assets/96958efd-1e26-4cac-9d73-1bb93d6f4af8" />
</p>
<p align="center"> 
<span style="color: #6a737d;">
<b>FIGURE:</b> Overview of the proposed <b>ReSoFed</b> framework. It first estimates client reliability, 
performs greedy model soup-based selection, and then applies reliability-aware aggregation 
to produce a robust global model. 
</span></p>


### 🔹 Step 1: Cross-Domain Reliability Estimation

Each client model is evaluated on a **server-held validation set**:

```math
r_k = Eval(\theta_k, D_{val})
```

### 🔹 Step 2: Greedy Model Soup-Based Selection

- Clients are sorted by reliability
- Iteratively add models only if performance improves
- Filters out weak / overfitted clients

### 🔹 Step 3: Reliability-Aware Aggregation

Final global model:

```math
\theta_{global} = \sum_{k \in S} \alpha_k \theta_k
```
where the aggregation weights are defined as:
```math
\alpha_k = \frac{r_k}{\sum_{j \in S}  \ r_j}
```

---

## Experimental Setup

**Dataset:** SCB (Student Classroom Behavior)   

**Clients:** 5 simulated conditions   

**Heterogeneity:**
- Clean capture
- Brightness shift
- Motion blur
- Compression artifacts
- Occlusion  

**Models:**
- **CNNs:** ResNet-50, EfficientNet-V2-S, ConvNeXt-B
- **Transformers:** ViT B-16, Swin-V2-Tiny, Swin-V2-Base

---

## Results

ReSoFed consistently outperforms standard federated learning (FedAvg) across multiple architectures.

| Model             | FedAvg Acc (%) | ReSoFed Acc (%) |
| ----------------- | -------------- | --------------- |
| ResNet-50         | 73.82          | **78.50**       |
| EfficientNet-V2-S | 78.93          | **81.61**       |
| ConvNeXt-Base     | 81.82          | **82.75**       |
| ViT-B/16          | 80.47          | **81.00**       |
| Swin-V2-Tiny      | 81.23          | **81.68**       |
| Swin-V2-Base      | 81.96          | **82.35**       |

---

## Key Contributions
✅ Reliability-guided federated aggregation framework  
✅ Cross-domain validation-based reliability estimation  
✅ Greedy model soup for client selection  
✅ Architecture-agnostic and privacy-preserving  
✅ Significant improvements over FedAvg  

---

> Contact me at rafsan.kabir@ucalgary.ca
