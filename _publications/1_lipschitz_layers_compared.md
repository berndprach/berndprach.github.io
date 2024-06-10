---
title: "1-Lipschitz Layers Compared: Memory, Speed and Certifiable Robustness"
collection: publications
permalink: /publication/1LipschitzLayersCompared
excerpt: 'We compare existing methods of creating 1-Lipschitz convolutions, analysing them both theoretically as well as experimentally.'
date: 2024-06-20
venue: 'CVPR'
paperurl: 'https://arxiv.org/pdf/2311.16833'
# citation: 'Prach, Bernd, Fabio Brau, Giorgio Buttazzo, and Christoph H. Lampert. "1-Lipschitz Layers Compared: Memory, Speed, and Certifiable Robustness." arXiv preprint arXiv:2311.16833 (2023).'
---

<img src="/images/star_plot_line.png" alt="Radar plot of results" width="1200"/>


## Links:
- [ArXiv](https://arxiv.org/abs/2311.16833)
- [GitHub](https://github.com/berndprach/1LipschitzLayersCompared)
- [Poster](https://drive.google.com/file/d/1774juF7XtxgJTUi8g0a8B8sH8AuSvRj7/view?usp=sharing)


## Poster:
<img src="/images/poster.png" alt="Poster" width="1200"/>


## Abstract:
The robustness of neural networks against input perturbations with bounded magnitude represents a serious concern 
in the deployment of deep learning models in safety-critical systems. Recently, the scientific community has 
focused on enhancing certifiable robustness guarantees by crafting 1-Lipschitz neural networks that leverage 
Lipschitz bounded dense and convolutional layers. Different methods have been proposed in the literature to 
achieve this goal, however, comparing the performance of such methods is not straightforward, since different 
metrics can be relevant (e.g., training time, memory usage, accuracy, certifiable robustness) for different 
applications. Therefore, this work provides a thorough comparison between different methods, covering theoretical 
aspects such as computational complexity and memory requirements, as well as empirical measurements of time per 
epoch, required memory, accuracy and certifiable robust accuracy. The paper also provides some guidelines and 
recommendations to support the user in selecting the methods that work best depending on the available resources. 
We provide code at [github.com/berndprach/1LipschitzLayersCompared](https://github.com/berndprach/1LipschitzLayersCompared).

