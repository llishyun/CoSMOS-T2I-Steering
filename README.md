# 🧠 CoSMOS: Controlling Semantics and Object Counts via Mean-Oriented Steering

This repository contains the official implementation of **CoSMOS**, a training-free inference-time steering method for improving **object count fidelity** in text-to-image (T2I) diffusion models such as Stable Diffusion. CoSMOS dynamically injects steering vectors into cross-attention layers during the early denoising steps of the generation process.

---
## 📊 Qualitive Results
<p align="center">
  <img width="693" alt="image" src="https://github.com/user-attachments/assets/486cfd86-0090-4f1c-b56c-f19266a35684" />
</p>

## 📊 Quantitive Results
<p align="center">
  <img width="633" alt="image" src="https://github.com/user-attachments/assets/e5116400-ebaf-4f39-8607-1b573799a1af" />
</p>

---

## 🔍 Motivation

Text-to-image(T2I) generation models have improved greatly and have been widely
used in many applications. However, **T2I models still encounter challenges in
accurately representing the requested number of objects in the user prompt**. In
this work, we alleviate this problem by investing an inference-time intervention
framework that injects steering vectors into the cross-attention layers of a pre-
trained Stable Diffusion model. Our approach **modulates the attention query
projections using pre-computed direction vectors, without requiring any model
fine-tuning**. To improve robustness and adaptability, we introduce a **dynamic
scaling mechanism** for the steering strength, computed from the distance and
alignment between current latent representations and a reference distribution. We
explore both **single-vector and step-wise variants** of the method and show that our
approach enhances control over object count in generated images while preserving
image fidelity. This demonstrates that inference-time steering, though simple in
implementation, can serve as an effective mechanism for improving numerical
fidelity in T2I models. 

## 🛠️ Architecture
<p align="center">
  <img width="690" alt="image" src="https://github.com/user-attachments/assets/527cf36e-118c-4442-a8e4-3f74891d5229" />
</p>

## ✨ Features

- ⚙️ **No fine-tuning required** — works at inference time only
- 🎯 **Numerical fidelity improvement** — better control over object counts
- 🔀 **Single-vector & Multiple-vector options**
- 📐 **Dynamic α** — adaptive steering strength based on semantic gap
- 📊 Supports both qualitative & quantitative evaluations


## 📄 Paper

* **Title:** *CoSMOS: Controlling Semantics and Object Counts via Mean-Oriented Steering*  
* **Authors:** Hyoryung Kim, Hyemin Boo, Seunghyeon Lee, Myungjin Lee (Equal Contributions)
* **Affiliation:** Department of Artificial Intelligence, Ewha Womans University  
* **Paper:** [`CoSMOS: Controlling Semantics and Objects Counts via Mean Oriented Steering`](paper/CoSMOS__Controlling_Semantics_and_Objects_Counts_via_Mean_Oriented_Steering.pdf)

---

## 📁 Project Structure

```
├── excel/ # Datasets with (prompt, seed)
│ ├── internal_dataset.xlsx # Latents used for steering vector
│ └── external_dataset.csv # Prompts for testing generalization
│
├── paper/ # Project paper
│ └── CoSMOS__...pdf
│
├── src/ # Source notebooks
│ ├── compute_steering_vector.ipynb # Builds steering vectors
│ ├── evaluate.ipynb # Uses LLaVa to count generated objects
│ ├── extract_npy.ipynb # Extracts cross-attention vectors
│ ├── main.ipynb # Full pipeline
│ └── visualize.ipynb # Visualization with KDE plots
```


## 🚀 Getting Started

### Clone the Repository
```bash
git clone https://github.com/<your-username>/CoSMOS-T2I-Steering.git
cd CoSMOS-T2I-Steering
```


---

## 🙋 Acknowledgements
This work was conducted at Ewha Womans University and inspired by prior work on Inference-Time Intervention (ITI) and attention steering in diffusion models.
```
@article{li2024inference,
  title={Inference-time intervention: Eliciting truthful answers from a language model},
  author={Li, Kenneth and Patel, Oam and Vi{\'e}gas, Fernanda and Pfister, Hanspeter and Wattenberg, Martin},
  journal={Advances in Neural Information Processing Systems},
  volume={36},
  year={2024}
}
```
