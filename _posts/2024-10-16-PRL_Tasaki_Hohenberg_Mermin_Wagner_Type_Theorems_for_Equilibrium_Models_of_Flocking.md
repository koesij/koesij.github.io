---
layout: single
title: "Hohenberg-Mermin-Wagner-Type Theorems for Equilibrium Models of Flocking"
categories: ["physics read"]
tags: ["classical", "active matter", "out of equilibrium"]
use_math: true
author_profile: false
sidebar: false
    # nav: "counts"
---

## Tasaki, Hal. "Hohenberg-mermin-wagner-type theorems for equilibrium models of flocking." *Physical Review Letters* 125.22 (2020): 220601.

### Abstract

>We study a class of two-dimensional models of classical hard-core particles with Vicsek type “exchange interaction” that aligns the directions of motion of nearby particles. By extending the Hohenberg-MerminWagner theorem for the absence of spontaneous magnetization and the McBryan-Spencer bound for correlation functions, we prove that the models do not spontaneously break the rotational symmetry in their equilibrium states at any nonzero temperature.
>



#### About Vicsek model

 The **Vicsek model** is a famous example of collective motion, where self-propelled particles align with their neighbors, forming **flocks or clusters**. This model has received attention not only for explaining biological phenomena like flocking but also for introducing **new universality classes** in statistical mechanics.



#### Contradiction with the Hohenberg-Mermin-Wagner Theorem

 **SSB in 2D equilibrium systems** with continuous symmetry (like rotational symmetry) is **forbidden** by the **Hohenberg-Mermin-Wagner theorem**. However, the Vicsek model exhibits SSB, which suggests that the model does not fit into the traditional framework of equilibrium statistical mechanics.

The paper seeks to answer the following:

1. Can Vicsek-type models exhibit SSB in **thermal equilibrium**?

2. If not, what is the **physical origin** of the SSB seen in the Vicsek model?



#### The Model

 This paper studies a system of N particles in a **two-dimensional region** $[0, L]^2$ with periodic boundary conditions. The particle density is fixed as $\rho=\frac{N}{L^2}$. Each particle has position of $r_j \in [0, L]^2$, velocity of $v_j=(v^x_j, v^y_j)\in \mathbb{R}^2$ for $(j=1,...,N)$.

The $H$ of the system is as below:


$$
H=\sum_j\frac{m}{2}\vert v_j\vert^2+\sum_{j<k}\{u(r_j-r_k)-J(r_j-r_k)\frac{v_j}{\vert v_j \vert}\cdot\frac{v_k}{\vert v_k \vert}\}-h\sum_j \frac{v_j^x}{\vert v_j \vert}
$$


 A hard-core interaction potential between particles. It is infinite if particles get closer than a certain distance a_0 , ensuring they do not overlap:


$$
u(r)=\left\{ \begin{align}
& 0 \ \ \   \vert r \vert > a_0\\
& \infty \ \ \   \vert r \vert \leq a_0 \\
\end{align}
\right.
$$
 

The strength of the alignment interaction, which is non-zero only if particles $j$ and $k$ are within a distance $a_1$:


$$
J(r)=\left\{ \begin{align}
& J_0 \ \ \     \vert r \vert >a_1\\
& 0 \ \ \   \vert r \vert \leq a_1\\
\end{align}
\right.
$$


Unlike the Vicsek model, this Hamiltonian **does not include a self-propulsion term**. In the Vicsek model, particles move with a fixed speed in the direction of their velocity, requiring continuous energy input (i.e., non-equilibrium dynamics). In this model, particles only interact through alignment and hard-core interactions, with no built-in propulsion mechanism driving them forward.



#### Key Results

The absence of self-propulsion fundamentally limits the ability of the system to exhibit spontaneous symmetry breaking (SSB), as shown by the following results:



**No Spontaneous Symmetry Breaking (SSB):**

The paper extends the **Hohenberg-Mermin-Wagner theorem** to show that, even with alignment interactions, the system **cannot break rotational symmetry** at any finite temperature:


$$
\lim_{h \to 0} \lim_{L \to \infty} \frac{1}{N} \sum_{j=1}^N \langle v_{x,j} \rangle_{\beta, h} = 0
$$


This result indicates that in equilibrium, the average velocity in the x-direction is zero, and no preferred direction emerges.



**McBryan-Spencer Bound on Correlations:**

The correlation function for the particle velocities decays at least as a power law with distance:


$$
C_l(\beta) = \frac{\langle v_j \cdot v_k \chi_l \rangle_{\beta, 0}}{\langle \chi_l \rangle_{\beta, 0}} \leq \left( \frac{a_0}{l} \right)^\eta
$$


This decay shows that **long-range order** does not develop in equilibrium.



#### Conclusion

 The paper concludes that a **class of two-dimensional particle systems with Vicsek-type “exchange interaction” never exhibits spontaneous breakdown of rotational symmetry** in equilibrium. This means that **SSB** cannot arise in equilibrium systems like the one studied here, even with velocity alignment interactions.

The key insight is that **mobility and alignment alone are not sufficient** to generate SSB. The lack of **self-propulsion** and the presence of **detailed balance** prevent the emergence of long-range order and SSB.

Thus, the SSB observed in the Vicsek model must be attributed to its **non-equilibrium nature** and the **violation of detailed balance**, which allows persistent alignment and collective motion.
