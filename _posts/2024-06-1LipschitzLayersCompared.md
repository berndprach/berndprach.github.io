---
title: '1-Lipschitz Layer Compared'
date: 2024-06-26
permalink: /blog-posts/2024/06/1-LipschitzLayersCompared/
tags:
  - 1-Lipschitz
  - Certified Robust Classification
---

<img src="/images/star_plot_line.png" alt="Radar plot of results" width="1200"/>


Why 1-Lipschitz networks?
======

Current image classification models are not robust! 
Tiny, invisible perturbations of the input, known as adversarial examples, can change the predictions of the models.

<img src="/images/blog-posts/adv_panda.png" alt="Adversarial Panda" width="1200"/>
(Szegedy et al. 2014; Goodfellow, Shlens, and Szegedy 2015)

We study adversarial example mostly to learn more about neural networks,
and potentlially build models that e.g. generalize better in the future.

However, the existence of adversarial examples could also lead to some problems, such as
 - users not trusting the models,
 - security issues, and
 - it makes it impossible to build (faithful) interpretable models.

In order to create classifiers that are **guaranteed** to be free of adversarial examples,
many recent works have proposed methods of parameterizing 1-Lipschitz networks.

We call a function, a layer or a network 1-Lipschitz if the difference of two outputs is at most as big as the difference of the corresponding two inputs, or mathematically:
$$ \|f(x) - f(y)\|_2 \le \|x - y\|_2 $$
for all inputs x and y.

Once we know how to build 1-Lipschitz layers, we can simply construct 1-Lipschitz networks by stacking multiple of those layers.


When classifying an image using a 1-Lipschitz network, by construction, any perturbation of the input image can change the output of the network by at most the same amount. 
Therefore, if the difference of the larges 2 class scores of the original image is large enough, 
we can be sure that no perturbation of certain magnitude can change the order of outputs, and therefore the prediction of the model.
<img src="/images/blog-posts/ls_margin.png" alt="Robust Classification" width="1200"/>


Comparison
======

Theoretical
------

