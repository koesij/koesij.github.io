---
layout: single
title: "Learning protocols for the fast and efficient control of active matter"
categories: ["physics read"]
tags: ["classical", "active matter control"]
use_math: true
author_profile: false
sidebar: false
    # nav: "counts"
---

## Casert, Corneel, and Stephen Whitelam. "Learning protocols for the fast and efficient control of active matter." *arXiv preprint arXiv:2402.18823* (2024).

### Abstract

> Our results show that protocols identified by a flexible neural-network ansatz, which allows the optimization of multiple control parameters and the emergence of sharp features, are more efficient than protocols derived recently by constrained analytical methods.

### Active Particle in a Trap of Variable Stiffness

#### Single active Ornstein-Uhlenbeck particle

​	The system being considered is an **active Ornstein-Uhlenbeck particle**, whose motion follows the equation:


$$
\dot r(t) = v(t)-\mu\alpha r(t)+\sqrt{2D}\eta(t)
$$





The **self-propulsion velocity** of the particle is governed by the Ornstein-Uhlenbeck process, where:


$$
\braket{v}=0 \text{ and } \braket{v(t)v(t')}=D_1\tau^{-1}e^{\vert t-t'\vert /\tau}
$$


The trajectory-averaged heat is calculated as the trap stiffness varies from $\alpha_i$ to $\alpha_f$, with both active and passive contributions considered:


$$
\braket{Q}=\frac{1}{2}(\alpha_ix_i-\alpha_fx_f)+\frac{1}{2}\int^{t_f}_0 dt\dot \alpha(t)x(t) \\
+\frac{D_1t_f}{\tau\mu}-\int^{t_f}_0dt\alpha(t)y(t)
\\\\
x \equiv \braket{r^2} \text{ and }y\equiv\braket{rv}
$$



The **first line of the heat dissipation formula represents passive heat**, which includes:

1. The change in energy due to the difference between $\alpha_i$ and $\alpha_f$.
2. The work done by adjusting the trap stiffness, captured by the integral over $\dot{\alpha}(t)$.

The **second line of the formula corresponds to the active contribution**, which arises from the particle’s self-propulsion. This includes:

1. The active energy dissipation over time, scaled by the self-propulsion velocity $D_1$.
2.  Coupling term $\alpha(t) y(t)$.



The steady-state values for the particle’s position and velocity, corresponding to the final trap stiffness $\alpha_f$, are:



$$
x_{ss}=\frac{1}{\alpha_f \mu}(\frac{D_1}{\gamma_f}+D) \text{ and } y_{ss}=\frac{D_1}{\gamma_f}
$$



#### Neural Network

##### Part 1

​	The neural network is trained to output $\alpha(t)$ for a fixed time $t_f$, with the goal of minimizing the order parameter $(\phi = \braket{Q})$ using a genetic algorithm. The control parameter $\alpha_{\theta}(t)$ is constrained to stay within the limits set by the initial and final trap stiffness:

$$
\text{Constraint: }\alpha_i \le \alpha_\theta(t) \le \alpha_f
$$

The neural network produced **non-monotonic, rapidly varying protocols with discontinuities**, unlike the smooth protocols derived from theoretical framework, “Luke K. Davis et al., *Active matter under control: Insights from response theory*.”

However, when control parameters change sharply at the final moment, **the system doesn’t have enough time to physically respond**, as the simulation stops the clock at this point. In reality, if control parameters were abruptly altered, the particles would need time to react, and heat would be generated as the system adjusts to the new state. 



##### Part 2

​	To ensure the system reaches the final steady state and accounts for all the heat involved in the process, a constraint called **State-to-State Transformation (SST)** is introduced. This constraint ensures the focus is not just on minimizing the heat up to the final parameter change, but also on driving the system to its steady state.


$$
\text{order parameter: }\phi =\Delta+c \text{ if }\Delta\geq\Delta_0 \text{ and } \phi = \braket{Q}\text{ otherwise}
\\
c=100\text{ is a penalty constant.}
$$



Here, $\Delta$ measures how close the system is to its steady state at the end of the process:


$$
\Delta^2=(x_f-x_{ss})^2+(y_f-y_{ss})^2
$$
 

with $x_{ss}$ and $y_{ss}$ being the steady-state values of position and velocity, respectively. The tolerance for achieving the steady state is set to $\Delta_0 = 10^{-3}$.

The modified order parameter **ensures that the Neural Network’s protocol drives the particle to the steady state corresponding to  $\alpha_f$** . Once this is achieved, the Neural Network then learns to minimize the heat among all protocols that satisfy the SST constraint.

**Result:** The protocol learned by the neural network produced significantly **less heat** compared to the protocol derived from the theoretical framework proposed by “Luke K. Davis et al.”



### Active Particle of Variable Activity in a Trap of Variable Stiffness

#### Active Brownian particle confined by a two-dimensional harmonic potential

The motion of an **active Brownian particle** in a two-dimensional harmonic potential is described by the following equations:


$$
\text{equation of motion:}
\\
\frac{d \boldsymbol{\rho}}{d\tau}=u_0\hat{e}(\theta)-\mu k \boldsymbol{\rho}+\sqrt{2D_t}\boldsymbol{\xi}_r(\tau),
\\
\frac{d\theta}{d\tau}=\sqrt{2D_\theta}\xi_\theta(\tau)
\\
\\
\text{position vector: }\boldsymbol{\rho}=(\rho cos\phi, \rho sin\phi)
\\
\text{direction: }\hat{e}(\theta)=(cos\theta, sin\theta)
$$



The equations can be rewritten in a **dimensionless form** as:


$$
\frac{d\boldsymbol{r}}{dt}=\lambda \hat{e}(\theta)-\kappa\boldsymbol{r}+\sqrt{2}\boldsymbol{\xi}_r(t)\\
\frac{d\theta}{dt}=\sqrt{2}\xi_{\theta}(t)
\\
\\
\kappa\equiv\mu k/D_\theta \text{ and }\lambda\equiv u_0/\sqrt{D_\theta D_t}
$$



The **steady-state probability distribution function** $\mathcal{P}_{ss}(r, \chi)$ of the system dependes only on $r \equiv \vert \boldsymbol{r} \vert$ and $\chi \equiv \theta-\phi$, and is known exactly Kanaya Malakar, Arghya Das, Anupam Kundu, K. Vijay Kumar, and Abhishek Dhar, “Steady state of an active Brownian particle in a two-dimensional harmonic trap,” Physical Review E 101, 022610 (2020).



#### Neural Network

 For this experiment, the control parameters are bounded within the ranges $0 \leq \lambda \leq 11$ and $1 \leq \kappa \leq 7$, which represent typical experimental conditions.

##### Part 1

The neural network outputs $(\lambda = a(t), \kappa(t))$ based on the input time $t$. **It is trained to minimize the protocol time $t_f$**, with order parameters similar to those used in the case of the active particle, ensuring the SST.

**Result:** The protocol learned by the neural network achieved a **SST three times faster** than the protocol derived from  theoretical methods.

##### Part 2

In this setup, the neural network outputs $(\lambda(t), \kappa(t))$ for the given time input t and a fixed protocol time t_f = 0.44. **The goal here is to minimize the mean work.** Again, the order parameters are set similarly to the active particle, ensuring the SST.

The mean work is calculated as:


$$
\braket{W}=\int^{t_f}_0dt\dot{\kappa}\braket{\frac{\partial U}{\partial \kappa}}=\frac{1}{2}\int^{t_f}_0dt\dot{\kappa}\braket{r^2}
$$



**Result:** The neural network was able to **extract net work** during the state-to-state transformation, achieving a protocol where the mean work was negative, meaning more work was extracted than input. **In contrast, the theoretical protocol was not able to reach negative net work.**



### Work Extraction from Confined, Interacting Active Particles

#### N interacting active Brownian particles placed within the two-dimensional harmonic trap

The motion of N interacting active Brownian particles within a two-dimensional harmonic trap is described by the following equations:


$$
\text{(i-th particle evolves according to the Langevin equation)}
\\
\frac{d\boldsymbol{r}_i}{dt}=\lambda\hat{e_i}(\theta)-\kappa r_i-\partial_{r_i}\sum_{j\neq i}V(r_{ij})+\sqrt{2}\boldsymbol{\xi}_r(t)
\\
\frac{d\theta_i}{dt}=\sqrt{2}\xi_\theta(t)
\\
$$



$V(x)$ is the inter-particle potential:


$$
V(x)=\begin{cases}4\epsilon[(\sigma/x)^{12}-(\sigma/x)^{6}]+\epsilon & (x<2^{1/6} \epsilon)
\\
0 & (\text{otherwise}) \end{cases}
$$


where $r_{ij}=\vert \boldsymbol{r_j}-\boldsymbol{r_i} \vert$  is the distance between particles $i $ and $j$.



The **mean work** done on the system is given by:


$$
\braket{W}=\frac{N}{2}\int^{t_f}_0{dt\dot{\kappa}R^2}
$$



where $R^2$ is the average squared distance:


$$
R^2\equiv N^{-1}\sum^{N}_{i=1}\braket{r^{2}_{i}}
$$


**No analytical solutions are known for this many-body system**, but a protocol can be learned in exactly the same way as for the single-particle problems considered previously, using a genetic algorithm to train a neural network to minimize $\phi=\braket{W}$.



#### Neural Network

The neural network outputs $(\lambda(t), \kappa(t))$ for given input $t$ at given $t_f=1.0$. **It is trained to minimize mean work.** The order parameters are set similarly to the previous cases.



**Result:** The neural network was trained with different numbers of particles $N$. The main finding of the experiment was that **the extracted work per particle is a non-monotonic function of N.** This suggests that certain particle numbers may optimize work extraction in many-body active engines, indicating that particular cycles of such engines may function more efficiently with specific particle counts.
