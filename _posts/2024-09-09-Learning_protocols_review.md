---
layout: single
title: "Paper review: Learning protocols for the fast and efficient control of active matter"
categories: "physics read"
use_math: true
---

## Coneel Casert, Stephen Whitelam$^\dagger$

### Abstract

> Our results show that protocols identified by a flexible neural-network ansatz, which allows the optimization of multiple control parameters and the emergence of sharp features, are more efficient than protocols derived recently by constrained analytical methods.

### Active Particle in a Trap of Variable Stiffness

#### Single active Ornstein-Uhlenbeck particle

$$
\text{Equation of motion: }
\\
\dot r(t) = v(t)-\mu\alpha r(t)+\sqrt{2D}\eta(t)
\\
\\
\text{Self-propulsion velocity following Ornstein-Uhlenbeck process}: 
\\
\braket{v}=0 \text{ and } \braket{v(t)v(t')}=D_1\tau^{-1}e^{|t-t'|/\tau}
$$



$$
\text{Trajectory-averaged heat associated with varying }\alpha(t)\text{ from } \alpha_i \text{ to }\alpha_f \text{ in time } t_f:
\\
\braket{Q}=\frac{1}{2}(\alpha_ix_i-\alpha_fx_f)+\frac{1}{2}\int^{t_f}_0 dt\dot \alpha(t)x(t) \\
+\frac{D_1t_f}{\tau\mu}-\int^{t_f}_0dt\alpha(t)y(t)
\\\\
x \equiv \braket{r^2} \text{ and }y\equiv\braket{rv}
$$

The first line: passive heat (- change in energy + work done by changing the trap stiffness)

The second line: active contribution


$$
\text{The steady state values of the system's position and velocity for the final trap stiffness:}
\\
x_{ss}=\frac{1}{\alpha_f \mu}(\frac{D_1}{\gamma_f}+D) \text{ and } y_{ss}=\frac{D_1}{\gamma_f}
$$

#### Neural Network

##### Part 1

The neural network outputs $\alpha(t)$ for given input $t$ at fixed $t_f$. It is trained to minimize the order parameter.

$$
\text{order parameter: }\phi =\braket{Q}
\\
\text{optimizer: genetic algorithm}
\\
\text{experimentally-motivated constraint: }\alpha_i \le \alpha_\theta(t) \le \alpha_f
$$

The neural network **exhibited non-monotonic, rapidly-varying protocols with jump discontinuities at initial and final times**, unlike the smooth, slowly varying protocols in the theoretical framework of “Luke K. Davis et al., *Active matter under control: Insights from response theory*.”

However, when control parameters change sharply at the final moment, **the system doesn’t have enough time to physically respond**, as the simulation stops the clock at this point. In reality, if control parameters were abruptly altered, the particles would need time to react, and heat would be generated as the system adjusts to the new state. 



##### Part 2

Therefore the constraint called **State-to-State Transformation (SST)** is introduced. This constraint guarentees that the system reaches the final steady state and accounts for all the heat involved in the process, rather than only focusing on minimizing the heat up to the point of the final parameter change.

$$
\text{order parameter: }\phi =\Delta+c \text{ if }\Delta\geq\Delta_0 \text{ and } \phi = \braket{Q}\text{ otherwise}
\\
\text{optimizer: genetic algorithm}
\\
\text{experimentally-motivated constraint: }\alpha_i \le \alpha_\theta(t) \le \alpha_f\\\\

\Delta^2\equiv(x_f-x_{ss})^2+(y_f-y_{ss})^2
\\
\text{tolerance with which we wish to achieve this steady state: }\Delta_0=10^{-3}\\
c=100
$$

The modified order parameter **ensures that the Neural Network’s protocol drives the particle to the steady state corresponding to  $\alpha_f$** . Once this is achieved, the Neural Network then learns to minimize the heat among all protocols that satisfy the SST constraint.

**Result:** The protocol learned by the neural network produced significantly **less heat** compared to the protocol derived from the theoretical framework proposed by “Luke K. Davis et al.”



### Active Particle of Variable Activity in a Trap of Variable Stiffness

#### Active Brownian particle confined by a two-dimensional harmonic potential

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

Dimensionless version

$$
\frac{d\boldsymbol{r}}{dt}=\lambda \hat{e}(\theta)-\kappa\boldsymbol{r}+\sqrt{2}\boldsymbol{\xi}_r(t)\\
\frac{d\theta}{dt}=\sqrt{2}\xi_{\theta}(t)
\\
\\
\kappa\equiv\mu k/D_\theta \text{ and }\lambda\equiv u_0/\sqrt{D_\theta D_t}
$$

The **steady-state probability distribution function** $\mathcal{P}_{ss}(r, \chi)$ of the system dependes only on $r\equiv \left|\boldsymbol{r}\right|$ and $\chi \equiv \theta-\phi$, and is known exactly Kanaya Malakar, Arghya Das, Anupam Kundu, K. Vijay Kumar, and Abhishek Dhar, “Steady state of an active Brownian particle in a two-dimensional harmonic trap,” Physical Review E 101, 022610 (2020).



#### Neural Network

The control parameters are bounded as$0\leq \lambda\leq11,\ 1\leq\kappa\leq7$ for a typical experimental setup.

##### Part 1

The neural network outputs $(\lambda=a(t), \kappa(t))$ for given input $t$. **It is trained to minimize protocol time $t_f$.** The order parameters are set similarly to those in the case of the active particle discussed in part 2. 

**Result:** The protocol learned by the neural network achieved a **state-to-state transformation three times faster** compared to the protocol derived from constrained theoretical methods.

##### Part 2

The neural network outputs $(\lambda(t), \kappa(t))$ for given input $t$ at given $t_f=0.44$. **It is trained to minimize mean work.** The order parameters are set similarly to those in the case of the active particle discussed in part 2.

$$
\text{Mean work: }\braket{W}=\int^{t_f}_0dt\dot{\kappa}\braket{\frac{\partial U}{\partial \kappa}}=\frac{1}{2}\int^{t_f}_0dt\dot{\kappa}\braket{r^2}
$$

**Result:** The neural network was able to **extract net work** during the state-to-state transformation, achieving a protocol where the mean work was negative, meaning more work was extracted than input. **In comparison, the theoretical protocol was not able to reach negative net work.**



### Work Extraction from Confined, Interacting Active Particles

#### N interacting active Brownian particles placed within the two-dimensional harmonic trap



$$
\text{Equation of motion (i-th particle evolves according to the Langevin equation):}
\\
\frac{d\boldsymbol{r}_i}{dt}=\lambda\hat{e_i}(\theta)-\kappa r_i-\partial_{r_i}\sum_{j\neq i}V(r_{ij})+\sqrt{2}\boldsymbol{\xi}_r(t)
\\
\frac{d\theta_i}{dt}=\sqrt{2}\xi_\theta(t)
\\
\\
V(x)\text{ is the inter-particle potential:}
\\
V(x)=\begin{cases}4\epsilon[(\sigma/x)^{12}-(\sigma/x)^{6}]+\epsilon & (x<2^{1/6} \epsilon)
\\
0 & (\text{otherwise}) \end{cases}
\\
r_{ij}=|\boldsymbol{r_j}-\boldsymbol{r_i}|
$$

$$
\text{Mean work: }\braket{W}=\frac{N}{2}\int^{t_f}_0{dt\dot{\kappa}R^2}
\\
R^2\equiv N^{-1}\sum^{N}_{i=1}\braket{r^{2}_{i}}
$$

**No analytical solutions are known for this many-body system**, but a protocol can be learned in exactly the same way as for the single-particle problems considered previously, using a genetic algorithm to train a neural network to minimize $\phi=\braket{W}$.

#### Neural Network

The neural network outputs $(\lambda(t), \kappa(t))$ for given input $t$ at given $t_f=1.0$. **It is trained to minimize mean work.** The order parameters are set similarly to the previous cases.



**Result:** The neural network was trained with different numbers of particles $N$. The main finding of the experiment was that **the extracted work per particle is a non-monotonic function of N.** This suggests that certain particle numbers may optimize work extraction in many-body active engines, indicating that particular cycles of such engines may function more efficiently with specfic particle counts.
