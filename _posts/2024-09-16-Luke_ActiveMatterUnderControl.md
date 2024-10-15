---
layout: single
title: "Active Matter under Control: Insights from Response Theory"
categories: ["physics read"]
tags: ["classical", "out of equilibrium", "active matter"]
use_math: true
author_profile: false
sidebar: false
    # nav: "counts"
---

## Davis, Luke K., Karel Proesmans, and Étienne Fodor. "Active matter under control: Insights from response theory." *Physical Review X* 14.1 (2024): 011012.

### Abstract

>  Here, we derive and implement a versatile framework for the thermodynamic control of active matter. Combining recent develpements in stochastic thermodynamics and response theory, our approach shows how to find the optimal control for either continuous- or discrete-state active systems operating out of equilibrium.

#### Optimal Protocols: Passive vs. Active Systems 

​	Active systems are inherently nonequilibrium due to the continouous conversion of energy into work by individual particles, resulting in constant heat dissipation. This is different from passive systems, where thermodynamics efficiency improves with slower protocols. In active matter, however, there's a trade-off . **If a protocol is too fast, it dissipates more heat. If it's too slow, dissipation also grows because of sustained energy consumption. As a result, there's a natural optimal protocol duration where heat dissipation is minimized.** This paper lies in understanding the consequences of this growing dissipation and how we control active systems despite it. 

 In a **passive system**, using overdamped Langevin dynamics, the heat dissipation follows the first law of thermodynamics. The motion of particles is gonverned by the follwing equation:


$$
\dot{\boldsymbol{r}}_t=-\mu \nabla_{i}\phi(\alpha, {\boldsymbol{r}})+\sqrt{2D}\boldsymbol{\eta}_i
$$



The average heat dissipated into the thermal bath for a passive system is given by:


$$
\braket{Q}=\braket{\phi(\alpha_0)}_{s}-\braket{\phi(\alpha_1)}+\int^{t_p}_{0}dt\dot{\alpha}\braket{\partial_{\alpha} \phi}
$$



In this case, there is a balance between the system's potential energy and the work done.



 For an **active system**, small modification is introduced by adding a self-propulsion term. Each particle  $i=\{1,...,N\}$ has an independent self-propulsion velocity $\boldsymbol{v}_i$, and the motion equation becomes:


$$
\dot{\boldsymbol{r}}=-\mu\nabla_{i}\phi(\alpha, {\boldsymbol{r}})+\boldsymbol{v}_i+\sqrt{2D}\boldsymbol{\eta}_i
$$



The average heat dissipated into the thermal bath for an active system is:


$$
\braket{Q}=\braket{\phi(\alpha_0)}_{s}+\braket{\phi(\alpha_1)}+\int^{t_p}_0dt[\dot{\alpha}\braket{\partial_{\alpha}\phi}-\braket{J}]
\\=\frac{Nt_p\braket{v^2}}{\mu}+\braket{\phi(\alpha_0)}_{s}-\braket{\phi(\alpha_1)}+\int^{t_p}_0dt(\dot{\alpha}\braket{\partial_{\alpha}\phi}-\sum^{N}_{i=1}\braket{\nabla_{i} \phi\cdot\boldsymbol{v}_i})
\\
\\
J=\boldsymbol{f}_i\cdot\boldsymbol{v}_i\\
{\alpha}_0={\alpha}(t=0), {\alpha}_1={\alpha}(t=t_p)
$$


In the case of an active system, **an additional boundary term $\frac{Nt_p \braket{v^2}}{\mu}$ appears in the heat dissipation compared to the passive system.** This term is proportional to the protocol duration and depends on the specifics of the self-propulsion mechanism. It becomes more significant when the number of particles is large. **The integral term will play an important role in later discussions, as it reflects the continous contribution of the system's dynamics over time.**



#### Framework for Optimal Control

​	To address this, **a weak and slow driving assumption is made, allowing the system to remain close to its steady state while varying the control parameter $\alpha$. This assumption, while limiting generality, enables the use of systematic response theories.** With this approach, a general form for heat dissipation is derived, which consists of both a boundary term and a Lagrangian term:


$$
\text{heat dissipation:}\\
\braket{Q}=B(\alpha_0, \alpha_1,\dot{\alpha}_0, \dot{\alpha}_1 
)+\int^{t_p}_{0}dt\mathcal{L}(\dot{\alpha}, \alpha)
\\\\
\text{boundary term}:
\\
B=\braket{\phi_0}_s-\braket{\phi_1}_s+\dot{\alpha}_0\sum(\alpha_0)-\dot\alpha_1(\Phi+\sum)(\alpha_1)+\int^{\alpha_1}_{\alpha_0}d\alpha\Lambda(\alpha)
\\
\text{Lagrangian term:}
\\
\mathcal{L}(\dot{\alpha},\alpha)=\dot{\alpha}^2(\Psi-\sum')(\alpha)-V(\alpha),\ \sum'=d\sum/d\alpha
$$



The functions $\{V, \Phi, \sum, \Lambda, \Phi\}$ are given by:


$$
V=-\braket{J}_s, \ \Phi=\int^{\infty}_{0}dtR_{1}(\phi;t,0)t,
\\
\sum=\frac{1}{2}\int^{\infty}_{0}dtR_{1}(J;t,0)t^2,
\\
\Lambda=\braket{\partial_{\alpha}\phi}_s+\int^{\infty}_{0}dtR_{1}(J;t,0)t,
\\
\Psi=\int^{\infty}_{0}dtR_{1}(\partial_\alpha\phi;t,0)t+\frac{1}{2}\int^{\infty}_{0}\int^{\infty}_{0}dtdt'R_{2}(J;t',t'-t,0)tt'
$$



**The Lagrangian is the key quantity in minimize heat dissipation.** The Lagrangian has a familiar structure to physicists, resembling kinetic and potential energy terms. By applying the calculus of variations and solving the Euler-Lagrange equations, the system can be optimized. 

In this setup, the Lagrangian depends on $\dot{\boldsymbol{\alpha}}$ and $\boldsymbol{\alpha}$. Since the Lagrangian is homogeneous -meaning it doesn't explicitly depend on time - a constant of motion, which is the Hamiltonian, can be extracted. **This allows for the calculation of the protocol speed and the first integral of motion, both of which are crucial for determining the optimal protocols.**


$$
E(t_p)=\frac{\dot\alpha^2}{2}(\Psi-\sum')(\alpha)+V(\alpha)
$$



The optimal protocol speed is given by:


$$
\dot{\alpha}=\pm\sqrt{\frac{E-V(\alpha)}{(\Psi-\sum')(\alpha)}}
$$



The protocol duration $t_p$ can be computed using:


$$
t_p=\Bigg|\int^{\alpha_1}_{\alpha_0}da\sqrt{\frac{(\Psi-\sum')(\alpha)}{E-V(\alpha)}}\Bigg|
$$



These functions $\{V, \Phi, \sum, \Lambda, \Phi\}$ represent terms in the heat dissipation formula and are influenced by the system’s linear and second-order responses. **To fully capture the system's behavior, it is important to account for non-linear effects that arise from second-order responses.**

 **If the self-propulsion terms are eliminated, the system simplifies and aligns with passive control frameworks already known in the literature.** Once $\{V, \Phi, \sum, \Lambda, \Phi\}$ are understood, the optimal control protocols can be derived.



####  Response Functions: From Correlations to Equations of Motion

**Note:** I'm still exploring the formalism of response functions and how they relate to correlation functions and equations of motion. Since I'm new to this topic, I'll need more time to fully understand it. Therefore, based on my current understanding, I'll leave an overview and key concepts of how response functions are used to predict the system's behavior analytically.



​	To explore heat dissipation in active systems, the paper employs **response theory**, which explains how systems react to small external perturbations. Rather than calculating the system's response to each perturbation directly, the paper uses **correlation functions** to predict the system's behavior, offering analytically tractable approach.

 The **response functions** are derived from **correlation functions**, which measure the relationships between fluctuations in different observables over time. The main idea is that the system's spontaneous fluctuations (natural variations without external control) encode the same information needed to predict its response to perturbations. This connection is rooted in the **fluctuation-dissipation theorem**, which links these fluctuations to the system's response to small changes.

 For systems far from equilibrium, such as active matter, the paper extends these ideas using **fluctuation-response relations**. These relations apply to both passive and active systems, allowing the response function to be expressed in terms of **connected correlation functions**, which account for interactions between different parts of the system. By calculating these correlations, the system’s response can be predicted without experimental perturbation.

 The paper uses the **path integral approach** to compute the response functions, describing the system’s evolution through an **action** that captures its entire trajectory. By taking functional derivatives of this action with respect to the control parameter perturbation, the response functions are derived in terms of the system’s dynamics. By expressing the response functions as path integrals, the correlation functions can be directly related to the system’s **equations of motion**. 



#### Application to Active and Many-Body Systems

​	One of the key results of applying this framework to active and many-body systems is that, **unlike passive control, protocols in active systems do not collapse onto a single master curve.** For more detailed insights, including visual representations and specific cases, it’s best to refer directly to the figures and discussions presented in the paper.
