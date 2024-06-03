---
title: "1-Lipschitz Neural Networks are more expressive with N-Activations"
collection: publications
permalink: /publication/NActivation
excerpt: 'We show a shortcoming with currently popular activation functions in 1-Lipschitz networks, both empirically and experimentally. Then we propose an activation function that provably overcomes this limitation.'
date: 2023-11-10
venue: 'arXiv'
paperurl: 'https://arxiv.org/pdf/2311.06103'
citation: 'Prach, Bernd, and Christoph H. Lampert. "1-Lipschitz Neural Networks are more expressive with N-Activations." arXiv preprint arXiv:2311.06103 (2023).'
---

<img src="/images/n_activation.png" alt="Radar plot of results" width="1200"/>


## Links:
- [ArXiv](https://arxiv.org/abs/2311.06103)
- [GitHub](https://github.com/berndprach/NActivation)


## Abstract:
A crucial property for achieving secure, trustworthy and interpretable deep learning systems is their robustness: small changes to a system's inputs should not result in large changes to its outputs. 
Mathematically, this means one strives for networks with a small Lipschitz constant. Several recent works have focused on how to construct such Lipschitz networks, typically by imposing constraints 
on the weight matrices. In this work, we study an orthogonal aspect, namely the role of the activation function. We show that commonly used activation functions, such as MaxMin, as well as all piece-wise 
linear ones with two segments unnecessarily restrict the class of representable functions, even in the simplest one-dimensional setting. We furthermore introduce the new N-activation function that is 
provably more expressive than currently popular activation functions. We provide code at [this https URL](https://github.com/berndprach/NActivation).

