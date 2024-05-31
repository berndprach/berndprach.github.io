---
title: "1-Lipschitz Layers Compared: Memory, Speed and Certifiable Robustness"
collection: publications
permalink: /publication/1LipschitzLayersCompared
excerpt: 'We compare existing of creating 1-Lipschitz convolutions.'
date: 2024-06-20
venue: 'CVPR'
slidesurl: 'http://berndprach.github.io/files/slides1.pdf'
paperurl: 'https://arxiv.org/abs/2311.16833'
citation: 'Prach, B., Brau, F., Buttazzo, G., & Lampert, C. H. (2023). 1-Lipschitz Layers Compared: Memory, Speed, and Certifiable Robustness. arXiv preprint arXiv:2311.16833.'
---

<img src="https://github.com/berndprach/berndprach.github.io/blob/master/images/star_plot_line.png" alt="Radar plot of results" width="800"/>


## Links:
- [GitHub](https://github.com/berndprach/1LipschitzLayersCompared)
- [ArXiv](https://arxiv.org/abs/2311.16833)

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

