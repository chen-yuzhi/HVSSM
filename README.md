# H-VSSM: A Hilbert-Driven Context-Shunting Framework for Robust Structural Defect Detection

[![Paper](https://img.shields.io/badge/Paper-ICME2026-blue)](https://github.com/chen-yuzhi/HVSSM)
[![Framework](https://img.shields.io/badge/PyTorch-2.1-red)](https://pytorch.org/)
[![SOTA](https://img.shields.io/badge/SOTA-DeepCrack-green)](https://github.com/chen-yuzhi/HVSSM)

This is the official implementation of the paper: **"H-VSSM: A Hilbert-Driven Context-Shunting Framework for Robust Structural Defect Detection"**, accepted by **ICME 2026**.

这是论文 **"H-VSSM: A Hilbert-Driven Context-Shunting Framework for Robust Structural Defect Detection"** 的官方实现，该论文已被 **ICME 2026** 接收。

---

## 💡 Abstract | 摘要
**English:** While Visual State Space Models (VSSMs) offer linear complexity, their standard anisotropic scanning strategies disrupt 2D spatial locality, which is detrimental to the topological continuity of fine-grained structural cracks. We propose **H-VSSM**, a Hilbert-driven framework to maximize topological fidelity. Central to our approach is the **Fluid Hilbert-based Structure-Aware Selective Scan (H-SS2D)**, which ensures geometrically adjacent pixels remain contiguous in the 1D sequence. We also introduce a **Feature Shunt Attention Module (FSAM)** and an **Edge Information Enhanced Module (EIEM)** for multi-scale context aggregation. H-VSSM achieves a state-of-the-art F1 score of **94.02%** on the DeepCrack dataset.

**中文:** 尽管视觉状态空间模型 (VSSMs) 具有线性复杂度，但其标准的各向异性扫描策略破坏了 2D 空间局部性，这对细粒度结构裂缝的拓扑连通性极为不利。我们提出了 **H-VSSM**，目的是最大化拓扑保真度的希尔伯特驱动框架。核心贡献是 **基于流体希尔伯特曲线的结构感知选择性扫描 (H-SS2D)**，它保证了几何上相邻的像素在 1D 序列中保持邻近。此外，引入了 **特征分流注意力模块 (FSAM)** 以及 **边缘信息增强模块 (EIEM)** 用于多尺度上下文聚合。H-VSSM 在 DeepCrack 数据集上达到了 **94.02%** 的 F1 分数，刷新了记录。

---

## 🛠️ Key Features | 核心特性
* **H-SS2D (Hilbert Scan):** Mitigates "neighborhood breaking" by using Peano-Hilbert curves to preserve 2D locality.

   **希尔伯特扫描:** 通过 Peano-Hilbert 曲线保持 2D 局部性，缓解“邻域破坏”现象。
* **FSAM (Feature Shunting):** A divide-and-conquer strategy to isolate high-frequency crack textures from complex backgrounds.
    
    **特征分流模块:** 采用分而治之的策略，将高频裂缝纹理与复杂背景噪声分离。
* **EIEM (Edge Enhancement):** Aggregates multi-scale context to recover fragmented boundary details.
  
   **边缘增强模块:** 聚合多尺度上下文信息，修复破碎的边缘细节。

---

## 📊 Performance | 实验表现
### Quantitative Comparison (DeepCrack Dataset)
| Methods | ODS | OIS | Precision | Recall | F1 Score | mIoU |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| SCSegamba (CVPR 25) | 0.8938 | 0.8990 | 0.9097 | 0.9124 | 0.9110 | 0.9022 |
| **H-VSSM (Ours)** | **0.9287** | **0.9317** | **0.9406** | **0.9398** | **0.9402** | **0.9322** |

H-VSSM significantly outperforms previous SOTA methods across multiple benchmarks (**DeepCrack, CrackMap, TUT**).

H-VSSM 在多个基准数据集上显著优于之前的 SOTA 方法。


## 🚀 Getting Started | 快速入门

### Requirements | 环境配置
* Ubuntu 22.04
* Python 3.10
* PyTorch 2.1+
* NVIDIA GPU (24GB VRAM recommended, e.g., RTX 4090)

```bash
# Clone the repository
git clone [https://github.com/chenyuzhi/HVSSM.git](https://github.com/chenyuzhi/HVSSM.git)
cd HVSSM

# Install dependencies
pip install -r requirements.txt


# Single GPU training
python train.py --config configs/hvssm_deepcrack.yaml --batch_size 1 --lr 1e-4

# Multi-GPU training (Distributed)
python -m torch.distributed.launch --nproc_per_node=2 train.py --config configs/hvssm_deepcrack.yaml

# Test on DeepCrack dataset
python test.py --weights checkpoint/best_model.pth --dataset deepcrack --img_size 512

```

## Citation | 引用
If you find our work useful for your research, please cite:

如果您发现我们的工作对您的研究有帮助，请考虑引用：

```bash
@inproceedings{wang2026hvssm,
  title={H-VSSM: A Hilbert-Driven Context-Shunting Framework for Robust Structural Defect Detection},
  author={Wang, TianYou and Yang, Ye and Ma, JiaQi and Wang, ShenYang and Chen, YuZhi},
  booktitle={Proceedings of the IEEE International Conference on Multimedia and Expo (ICME)},
  year={2026}
}
```
