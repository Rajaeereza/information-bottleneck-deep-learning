# On the Information Bottleneck Theory of Deep Learning

**Course Project · Information Theory and Inference · University of Padova · 2022–2023**  
Reza Rajaee · Sarvenaz Babakhani

---

## Overview

The Information Bottleneck (IB) theory, originally proposed by Tishby et al., offers a theoretical framework for understanding how deep neural networks learn and generalise. It suggests that training proceeds in two phases — an initial fitting phase where mutual information between the representation T and the input X increases, followed by a compression phase where I(X;T) decreases while I(Y;T) is preserved. This project systematically investigates the conditions under which this compression phase appears, building on the critical re-examination by Saxe et al.

We reproduce and extend the key experimental findings of Saxe et al. across multiple network architectures, activation functions, optimizers, and mutual information estimation methods, using the MNIST dataset as a controlled testbed.

---

## Dataset

**MNIST** — 10,000 samples, greyscale images of size 1×28×28, 10 classes.

---

## Experimental design

### Networks

Four architectures were studied:

- **CNN1** — convolutional network with layer sizes (1350, 384, 972, 2400)
- **CNN2** — convolutional network with layer sizes (4356, 486, 432, 384)
- **CNN3** — convolutional network with layer sizes (4356, 6936, 3888, 2400)
- **FF** — fully connected feedforward network (12→10→7→5→4→3→2)

### Mutual information estimation

Two methods were compared for estimating I(X;T) and I(Y;T):

- **Binning** — discrete histogram-based estimation
- **KDE** — Kernel Density Estimation, providing upper and lower bounds on mutual information

### Activation functions

- **Tanh** — double-sided saturating nonlinearity
- **ReLU** — single-sided saturating nonlinearity

### Optimizers

- **Adam**
- **SGD** — Stochastic Gradient Descent
- **BGD** — Batch Gradient Descent

All combinations were evaluated, producing a systematic comparison across estimation method × activation × optimizer × architecture.

---

## Observations

The following observations are drawn from the experimental results and are consistent with the findings of Saxe et al.:

**Activation function is the dominant factor.** The information plane trajectory differs substantially between Tanh and ReLU across all network architectures and optimizers. Tanh consistently produces curved trajectories in the information plane suggesting a compression phase, while ReLU trajectories appear more monotonic without a clear compression phase — consistent with the theoretical prediction that double-sided saturating nonlinearities drive compression as activations enter saturation.

**Compression is not an artifact of stochasticity.** BGD experiments with Tanh reproduce qualitatively similar information plane trajectories to SGD, with smoother curves due to the deterministic nature of batch gradient descent. This supports the Saxe et al. finding that the compression phase does not arise from stochasticity in training.

**Estimation method substantially affects the observed trajectory.** KDE and Binning produce qualitatively different information plane shapes for the same network and training run, particularly for ReLU networks. This highlights that the apparent presence or absence of compression can be an artifact of the estimation method rather than a genuine property of the network's representations.

**Architecture affects trajectory shape but not the qualitative conclusions.** Across CNN1, CNN2, CNN3, and FF, the fundamental difference between Tanh and ReLU is preserved, though the specific trajectories and scales of I(X;T) vary with the architecture's depth and layer sizes.

---

## Key questions addressed

- Does the compression phase in the information plane depend on the activation function?
- Does stochasticity in training drive the compression phase, or does it also appear with batch gradient descent?
- How does the choice of mutual information estimator affect the observed information plane trajectory?
- Do these findings generalise across different CNN architectures and a feedforward network?

---

## Technical skills

| Area | Details |
|---|---|
| Information theory | Mutual information estimation · Information Bottleneck framework · information plane analysis |
| Deep learning | CNN architectures · feedforward networks · Tanh · ReLU · Adam · SGD · BGD |
| MI estimation | Binning method · Kernel Density Estimation (KDE) · upper and lower bounds |
| Scientific Python | PyTorch · NumPy · Matplotlib · MNIST data handling |
| Experimental design | Systematic comparison across architectures · activations · optimizers · estimators |

---

## Reference

Saxe AM, Bansal Y, Dapello J, Advani M, Kolchinsky A, Tracey BD, Cox DD. *On the Information Bottleneck Theory of Deep Learning.* ICLR, 2019.

---

## Repository note

This repository contains the code and results from a course project. The results are organised by experimental condition (estimation method, activation function, optimizer, architecture). A cleaned and documented version of the codebase is planned.

---

*Course project completed 2022–2023. University of Padova, Department of Physics and Astronomy.*
