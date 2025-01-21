---
layout: single
title: "Physics-informed deep learning for incompressible laminar flows"
categories: ["AI read"]
tags: ["physics informed neural network", "computational fluid dynamics"]
use_math: true
author_profile: false
sidebar: false
    # nav: "counts"

---

## Rao, Chengping, Hao Sun, and Yang Liu. "Physics-informed deep learning for incompressible laminar flows." *Theoretical and Applied Mechanics Letters* 10.3 (2020): 207-212.

### Abstract

> In this paper, we propose a mixed-variable scheme of physics-informed neural network (PINN) for fluid dynamics and apply it to simulate steady and transient laminar flows at low Reynolds numbers. A parametric study indicates that the mixed-variable scheme can improve the PINN trainability and the solution accuracy. 



This paper introduces a mixed-variable physics-informed neural network (PINN) framework to simulate incompressible laminar flows by **modifying the Navier-Stokes equations using continuum and constitutive formulations. The motivation behind this approach lies in the challenge of directly minimizing the physics-based loss functions, which involves calculating high-order derivatives, specifically second-order derivatives of the neural network outputs.** This process is computationally difficult and susceptible to errors when using automatic differentiation, as typically required in a PINN framework.



#### From Navier-Stokes to Continuum and Constitutive Formulations

In an **incompressible fluid system**, the dynamics of the fluid are governed by the Navier-Stokes equations, which follow the laws of conservation of mass and momentum. 

The **continuity equation** for incompressible flow is given by:



$$
\boldsymbol{\nabla} \cdot \boldsymbol{v} = 0
$$

The continuity equation ensures that the flow is incompressible.



The **momentum Equation** is given by:


$$
\frac{\partial \boldsymbol{v}}{\partial t} 
+ (\boldsymbol{v} \cdot \boldsymbol{\nabla}) \boldsymbol{v} 
= -\frac{1}{\rho} \boldsymbol{\nabla} p 
+ \frac{\mu}{\rho} \boldsymbol{\nabla}^2 \boldsymbol{v} 
+ \boldsymbol{g}
$$
where $\rho$ is the fluid density, $\mu$ viscosity of the fluid.

The **momentum equation** governs the **conservation of momentum** and describes how the velocity field of the fluid evolves under the influence of various forces.

 The **Cauchy stress tensor** $\boldsymbol{\sigma}$ provides a compact way to represent the internal stresses within a fluid, including both **pressure** and **viscous forces**.
$$
\boldsymbol{\sigma} = -p \mathbf{I} + \mu \left( \boldsymbol{\nabla} \boldsymbol{v} + \boldsymbol{\nabla} \boldsymbol{v}^T \right)
$$
In terms of the **Cauchy stress tensor**, the **momentum equation** for momentum conservation can be written as:
$$
\frac{\partial \boldsymbol{v}}{\partial t} +	(\boldsymbol{v} \cdot \boldsymbol{\nabla}) \boldsymbol{v}
= \frac{1}{\rho} \boldsymbol{\nabla} \cdot \boldsymbol{\sigma} + \boldsymbol{g}
$$




왜 뉴럴네트워크에서 p를 따로 뽑아주지?

p는 sigma를 trace취해서 구할 수 있는거 아닌가?


























$$
\boldsymbol{\nabla} \cdot \mathbf{v} = 0
\\
\frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \boldsymbol{\nabla}) \mathbf{v} = -\frac{1}{\rho} \boldsymbol{\nabla} p + \frac{\mu}{\rho} \boldsymbol{\nabla}^2 \mathbf{v} + \mathbf{g}
\\
\frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \boldsymbol{\nabla}) \mathbf{v} = \frac{1}{\rho} \boldsymbol{\nabla} \cdot \boldsymbol{\sigma} + \mathbf{g}
\\
\mu \boldsymbol{\nabla}^2 \mathbf{v}
\\
\boldsymbol{\nabla} \cdot \boldsymbol{\sigma} = -\boldsymbol{\nabla} p + \mu \boldsymbol{\nabla} \cdot \left( \boldsymbol{\nabla} \mathbf{v} + \boldsymbol{\nabla} \mathbf{v}^T \right)
\\
\boldsymbol{\sigma} = -p \mathbf{I} + \mu \left( \boldsymbol{\nabla} \mathbf{v} + \boldsymbol{\nabla} \mathbf{v}^T \right)
\\
\boldsymbol{\nabla} \mathbf{v} + \boldsymbol{\nabla} \mathbf{v}^T
\\
\boldsymbol{\nabla} \mathbf{v} =
\begin{pmatrix}
\frac{\partial v_1}{\partial x_1} & \frac{\partial v_1}{\partial x_2} & \frac{\partial v_1}{\partial x_3} \\
\frac{\partial v_2}{\partial x_1} & \frac{\partial v_2}{\partial x_2} & \frac{\partial v_2}{\partial x_3} \\
\frac{\partial v_3}{\partial x_1} & \frac{\partial v_3}{\partial x_2} & \frac{\partial v_3}{\partial x_3}
\end{pmatrix}
\\
\boldsymbol{\nabla} \mathbf{v}^T =
\begin{pmatrix}
\frac{\partial v_1}{\partial x_1} & \frac{\partial v_2}{\partial x_1} & \frac{\partial v_3}{\partial x_1} \\
\frac{\partial v_1}{\partial x_2} & \frac{\partial v_2}{\partial x_2} & \frac{\partial v_3}{\partial x_2} \\
\frac{\partial v_1}{\partial x_3} & \frac{\partial v_2}{\partial x_3} & \frac{\partial v_3}{\partial x_3}
\end{pmatrix}
\\
\boldsymbol{\sigma} = -p \mathbf{I} + \mu (\boldsymbol{\nabla} \mathbf{v} + \boldsymbol{\nabla} \mathbf{v}^T)
\\
\boldsymbol{\nabla} \mathbf{v} + \boldsymbol{\nabla} \mathbf{v}^T =
\begin{pmatrix}
2 \frac{\partial v_1}{\partial x_1} & \frac{\partial v_1}{\partial x_2} + \frac{\partial v_2}{\partial x_1} & \frac{\partial v_1}{\partial x_3} + \frac{\partial v_3}{\partial x_1} \\
\frac{\partial v_2}{\partial x_1} + \frac{\partial v_1}{\partial x_2} & 2 \frac{\partial v_2}{\partial x_2} & \frac{\partial v_2}{\partial x_3} + \frac{\partial v_3}{\partial x_2} \\
\frac{\partial v_3}{\partial x_1} + \frac{\partial v_1}{\partial x_3} & \frac{\partial v_3}{\partial x_2} + \frac{\partial v_2}{\partial x_3} & 2 \frac{\partial v_3}{\partial x_3}
\end{pmatrix}
\\
\boldsymbol{\sigma} =
\begin{pmatrix}

		-p + 2 \mu \frac{\partial v_1}{\partial x_1} & \mu \left( \frac{\partial v_1}{\partial x_2} + \frac{\partial v_2}{\partial x_1} \right) & \mu \left( \frac{\partial v_1}{\partial x_3} + \frac{\partial v_3}{\partial x_1} \right) \\
\mu \left( \frac{\partial v_2}{\partial x_1} + \frac{\partial v_1}{\partial x_2} \right) & - p + 2 \mu \frac{\partial v_2}{\partial x_2} & \mu \left( \frac{\partial v_2}{\partial x_3} + \frac{\partial v_3}{\partial x_2} \right) \\
\mu \left( \frac{\partial v_3}{\partial x_1} + \frac{\partial v_1}{\partial x_3} \right) & \mu \left( \frac{\partial v_3}{\partial x_2} + \frac{\partial v_2}{\partial x_3} \right) & - p + 2 \mu \frac{\partial v_3}{\partial x_3}
\end{pmatrix}
\\
\boldsymbol{\nabla} \cdot \boldsymbol{\sigma} =
\begin{pmatrix}
\frac{\partial \sigma_{11}}{\partial x_1} + \frac{\partial \sigma_{12}}{\partial x_2} + \frac{\partial \sigma_{13}}{\partial x_3} \\
\frac{\partial \sigma_{21}}{\partial x_1} + \frac{\partial \sigma_{22}}{\partial x_2} + \frac{\partial \sigma_{23}}{\partial x_3} \\
\frac{\partial \sigma_{31}}{\partial x_1} + \frac{\partial \sigma_{32}}{\partial x_2} + \frac{\partial \sigma_{33}}{\partial x_3}
\end{pmatrix}
$$
The **Navier-Stokes equation** for an incompressible Newtonian fluid (from the paper) is:
$$
\frac{\partial \boldsymbol{v}}{\partial t} + (\boldsymbol{v} \cdot \boldsymbol{\nabla}) \boldsymbol{v} = \frac{1}{\rho} \boldsymbol{\nabla} \cdot \boldsymbol{\sigma} + \boldsymbol{g}
$$
The **Cauchy stress tensor** for a Newtonian fluid is given by:
$$
\boldsymbol{\sigma} = -p \boldsymbol{I} + \mu (\boldsymbol{\nabla} \boldsymbol{v} + \boldsymbol{\nabla} \boldsymbol{v}^T)
$$

$$
\boldsymbol{\nabla} \cdot \boldsymbol{\sigma} = \boldsymbol{\nabla} \cdot \left( -p \mathbf{I} + \mu (\boldsymbol{\nabla} \mathbf{v} + \boldsymbol{\nabla} \mathbf{v}^T) \right)
\\
= -\boldsymbol{\nabla} p + \mu \boldsymbol{\nabla} \cdot (\boldsymbol{\nabla} \mathbf{v} + \boldsymbol{\nabla} \mathbf{v}^T)
\\
\boldsymbol{\nabla} \cdot \mathbf{v} = 0
$$



