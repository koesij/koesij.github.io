---
layout: single
title: "Out of equilibrium response and fluctuation-dissipation violations across scales in flocking systems"
categories: ["physics read"]
tags: ["classical", "active matter", "out of equilibrium"]
use_math: true
author_profile: false
sidebar: false
    # nav: "counts"
---

## Ferretti, Federica, et al. "Out of equilibrium response and fluctuation-dissipation violations across scales in flocking systems." *arXiv preprint arXiv:2405.12874* (2024).

## Abstract

> In this work, we consider a minimal model of flocking and investigate response behavior under directional perturbations. We show that equilibrium dynamical fluctuation-dissipation relations between response and correlations are violated, both at the local and at the global level. 



### The model and the perturbation protocol

$$
\text{Equations of motion:}\\
\frac{d\boldsymbol{v}_i}{dt}=-\frac{\partial{\mathcal{H}}}{\partial{\boldsymbol{v}_i}}+\boldsymbol{\xi}_i,\ \frac{d\boldsymbol{r}_i}{dt}=\boldsymbol{v}_i
\\
\text{white noise with variance }\braket{\xi_{i\alpha}(t)\xi_{j\beta}(t)}=2T\delta_{ij}\delta_{\alpha \beta}\delta(t-t'): \boldsymbol{\xi}_i
\\
\\
\text{The pseudo Hamiltonian:}\\
\mathcal{H}=\frac{J}{2}\sum_{ij}n_{ij}(\boldsymbol{v}_i-\boldsymbol{v}_j)^2+\frac{g}{2}\sum_i(\vert \boldsymbol{v}_i \vert - v_0)^2
\\
\text{adjacency matrix: }\left\{ \begin{align}
& n_{ij}=1 \text{ if } \vert \boldsymbol{r}_i - \boldsymbol{r}_j \vert \leq r_c \\
& n_{ij}=0 \text{ if } \vert \boldsymbol{r}_i - \boldsymbol{r}_j \vert > r_c 
\end{align}
\right.
\\
\\
\text{Perturbation protocol: }\mathcal{H}\rightarrow\mathcal{H}-\sum_{i}\boldsymbol{h_i}\cdot\boldsymbol{v}_i 
$$

