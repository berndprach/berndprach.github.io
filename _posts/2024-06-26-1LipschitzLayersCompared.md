---
title: '1-Lipschitz Layer Compared'
date: 2024-06-26
permalink: /blog-posts/2024/06/1-LipschitzLayersCompared/
tags:
  - 1-Lipschitz
  - Certified Robust Classification
---

<img src="/images/star_plot_line.png" alt="Radar plot of results" width="1200"/>

In our recent CVPR paper, "1-Lipschitz Layers Compared: Memory, Speed and Certifiable Robustness” we compared different methods of creating 1-Lipschitz convolutions.
In this blog post we try to give some additional background on why 1-Lipschitz methods are an interesting research topic, and discuss some results from the paper.

**This post is currently work in progress!**

Why 1-Lipschitz networks?
======

Current image classification models are not robust! 
Tiny, invisible perturbations of the input, known as adversarial examples[^ae], can change the predictions of the models.

[^ae]: Szegedy et al. 2014; Goodfellow, Shlens, and Szegedy 2015

<img src="/images/blog-posts/adv_panda.png" alt="Adversarial Panda" width="600"/>

We study adversarial example mostly to learn more about neural networks,
and potentlially build models that e.g. generalize better in the future.

However, the existence of adversarial examples could also lead to some problems, such as
 - users not trusting the models,
 - security issues, and
 - it makes it impossible to build (faithful) interpretable models.

In order to create classifiers that are **guaranteed** to be free of adversarial examples,
many recent works have proposed methods of parameterizing 1-Lipschitz networks.

We call a function, a layer or a network 1-Lipschitz if the difference of two outputs is at most as big as the difference of the corresponding two inputs, or mathematically:

$$ ||f(x) - f(y)||_2 \le ||x - y||_2 $$

for all inputs x and y.

Once we know how to build 1-Lipschitz layers, we can simply construct 1-Lipschitz networks by stacking multiple of those layers.


When classifying an image using a 1-Lipschitz network, by construction, any perturbation of the input image can change the output of the network by at most the same amount. 
Therefore, if the difference of the larges 2 class scores of the original image is large enough, 
we can be sure that no perturbation of certain magnitude can change the order of outputs, and therefore the prediction of the model.
<img src="/images/blog-posts/ls_margin.png" alt="Robust Classification" width="600"/>


Existing 1-Lipschitz Convolutions
======
Recently, many works have tried to construct 1-Lipschitz layers. It is relatively easy to construct 1-Lipschitz fully connected layers.
For example we can orthogonalize the weight matrices using a differentiable algorithm such as Bjork and Bowie, or we can divide the outputs of the layer by its operator norm, obtained using power iterations.
However, it is a bit more tricky to create 1-Lipschitz convolutions. For example, whilst we could apply conditions on the Jacobian of the layer, it is generally inpractical because of the size of this matrix.

We will introduce 7 methods of creating 1-Lipschitz convolutions from the literature:


<h2 style="display:inline;">BCOP</h2>
<p style="color:grey;font-size:70%;"> (Q. Li et al., 2019, NeurIPS) </p>
The methods BCOP (Block Orthogonal Convolution Parameterization) constructs the kernel of a \\( k \times k \\) convolution
from a set of \\( (2k − 1) \\) parameter matrices. 
Each of these matrices is orthogonalized using an algorithm by Bjorck & Bowie[^BnB].
Then, a \\( k \times k \\) kernel is constructed from those matrices in a
way that guarantees that the resulting layer is orthogonal.

[^BnB]: &#197;. Bj&ouml;rck and C. Bowie, 1971, SIAM Journal on Numerical Analysis


<h2 style="display:inline;">Cayley</h2>
<p style="color:grey;font-size:70%;"> (Trockman and Kolter, 2021, ICLR) </p>

Cayley Convolutions make use of the fact that circular padded convolutions are vector-matrix products in the Fourier domain.
As long as all those vector-matrix products have orthogonal matrices, the full convolution will have an orthogonal Jacobian.
The orthogonal matrices used in this are parameterized using the Cayely Transform[^Cayley]:
For any skew-symmetric matrix \\(A\\) the matrix \\(Q\\) is orthogonal, where \\(Q\\) is defined as

$$ Q = (I-A) (I+A)^{-1}. $$

[^Cayley]: Arthur Cayley, 1846, Journal fur die reine und angewandte Mathematik


<h2 style="display:inline;">SOC</h2>
<p style="color:grey;font-size:70%;"> (Singla and Feizi, 2021, ICML) </p>
Skew orthogonal convolutions (SOC) use an exponential convolution[\exc] in order to obtain a 1-Lipschitz layer:
Given a kernel \\(K\\), the exponential convolution can be defined as

$$ \exp(K)(x) = x + \frac{K \ast x}{1} + \frac{K \ast^2 x}{2!} + \dots + \frac{K \ast^t x}{t!} + \dots, $$

where \\(\ast^t\\) denotes a convolution applied \\(t\\) times.
The authors proved that any exponential convolution has an orthogonal Jacobian matrix as long as L is skew-symmetric,
providing a way of parameterizing 1-Lipschitz layers. 
In their work, the sum of the infinite series is approximated by computing only the first 5 terms during training and the first 12 terms during the inference, 
and L is normalized to have unitary spectral norm.

[^exc]: Hoogeboom et al., 2020, The convolution exponential and generalized Sylvester flows.


<h2 style="display:inline;">AOL</h2>
<p style="color:grey;font-size:70%;"> (Prach and Lampert, 2022, ECCV) </p>
  
We introduced Almost Orthogonal Lipschitz (AOL) as a rescaling method that guarantees a layer to be 1-Lipschitz.
For a fully connected layer with a parameter matrix \\(P\\), we define a diagonal rescaling matrix \\(D\\) with 

$$ D_{ii} = \big( \sum_j |P^\top P|_{ij} \big)^{-1/2}. $$

With this choice of \\(D\\), we show that the spectral norm of \\( PD \\) is bounded by 1,
which implies that the the linear given by \\( l(x)=PDx + b \\) is 1-Lipschitz.

We can also apply this rescaling to a convolution. In order to do this we need to consider the Jacobian \\(J\\) of the
convolution (instead of \\(P\\)) in the equation above.
We show how to efficiently evaluate the rescaling (or more precisely an upper bound of it) by
expressing the entries of \\( J^\top J \\) explicitely in terms of the kernel values.



### Citation
The layers were introduced in the following papers:
- **[AOL]** (Prach and Lampert, 2022, ECCV)
- **[BCOP]** Q. Li et al., 2019, NeurIPS; 
- **[CPL]** Meunier et al., 2022, ICML;
- **[Cayley]** Trockman and Kolter, 2021, ICLR; 
- **[LOT]** Xu, L. Li, and B. Li, 2022, NeurIPS; 
- **[SLL]** Araujo et al., 2023, ICLR;
- **[SOC]** Singla and Feizi, 2021, ICML;

Comparison
======

Theoretical
------

