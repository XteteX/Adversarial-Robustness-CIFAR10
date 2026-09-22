# Adversarial-Robustness-CIFAR100
# Vulnerability and Defense of CNNs against Adversarial Attacks (CIFAR-100)

This repository contains the code and experimental results for a research project investigating the vulnerability of Convolutional Neural Networks (CNNs) to adversarial perturbations, specifically focusing on the linear nature of neural networks as proposed by Goodfellow et al. (2015).

## 📌 Project Overview
Modern deep learning models exhibit a fundamental vulnerability to adversarial examples—inputs intentionally perturbed by an imperceptible margin to force a misclassification. This project:
1. **Demonstrates the vulnerability** of a custom CNN trained on the CIFAR-10 dataset using the Fast Gradient Sign Method (FGSM) and Projected Gradient Descent (PGD).
2. **Implements a defense mechanism** via Adversarial Training.
3. **Evaluates the robustness tradeoff**, comparing the base model and the robust model against single-step and iterative attacks.

## 🛠️ Methodology
* **Dataset:** CIFAR-10 (with Data Augmentation: RandomHorizontalFlip, RandomCrop)
* **Base Model:** Custom VGG-style CNN (Conv2d, BatchNorm, MaxPool, Dropout) achieving ~81% clean test accuracy.
* **Attacks Implemented:** 
  * **FGSM** (White-box, single-step)
  * **PGD** (White-box, iterative, 7 steps)
* **Defense:** Adversarial Training (mixing 50% clean and 50% FGSM-perturbed data in the training loop).

## 📊 Experimental Results

### 1. Visualizing Adversarial Examples
Below are examples of how imperceptible noise successfully fools the base model.

`![Adversarial Examples](https://drive.google.com/file/d/177hrO9pjydQBQxR7dCVHwIDNRLTnRQEc/view?usp=drive_link)`

### 2. Base Model vs. Protected Model Accuracy
The adversarial training significantly improved the model's resistance to single-step attacks (FGSM) but highlighted the phenomenon of gradient masking when facing iterative attacks (PGD).

*(Вставь сюда сохраненную картинку с двумя графиками)*
`![Accuracy Tradeoff Graphs](https://drive.google.com/file/d/1qz5eIkpm0eQ0rqF-XHUoPN9wM0wRMtbd/view?usp=drive_link)`

| Attack | Epsilon | Base Model Accuracy | Protected Model Accuracy |
| :--- | :---: | :---: | :---: |
| Clean | 0 | 81.8% | 54.3% |
| FGSM | 0.1 | 1.5% | 40.6% |
| FGSM | 0.25| 3.2% | 18.6% |
| PGD (7 steps)| 0.1 | 0.0% | 2.7% |

## 💡 Key Takeaway
The defense successfully mitigates single-step attacks (FGSM robustness increased from 1.5% to 40.6%). However, the complete failure against PGD confirms that training solely on single-step adversarial examples induces gradient masking rather than true robust optimization.

## 💻 How to Run
You can run the full experiment directly in your browser:
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1D4GCtKdHCBjRARfpm-DjVV1SmlrRKsM0#scrollTo=neS5Q5sOeaPZ)
