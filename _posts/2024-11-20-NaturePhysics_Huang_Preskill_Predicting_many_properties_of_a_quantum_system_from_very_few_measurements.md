---
layout: single
title: "Predicting many properties of a quantum system from very few measurements"
categories: ["physics read"]
tags: ["Quantum", "Quantum information"]
use_math: true
author_profile: false
sidebar: false
    # nav: "counts"
---

## Huang, Hsin-Yuan, Richard Kueng, and John Preskill. "Predicting many properties of a quantum system from very few measurements." *Nature Physics* 16.10 (2020): 1050-1057.

### Abstract

> We present an efficient method for constructing an approximate classical description of a quantum state using very few measurementsof the state. This description, called a ‘classical shadow’, can be used to predict many different properties; order $log(M)$ measurements suffice to accurately predict $M$ different functions of the state with high success probability. The number of measurements is independent of the system size and saturates information-theoretic lower bounds.



#### History of the FIeld: From Quantum State Tomography to Classical Shadows

1. **Quantum State Tomography**
   Quantum state tomography was the first framework developed to fully characterize quantum systems. It aims to reconstruct the **full density matrix $\rho$ of a quantum system** by performing a series of measurements. For a system with $n$ qubits, this requires determining $D^2 = 2^{2n}$ parameters, as the density matrix is a $D \times D$ Hermitian matrix. Despite being theoretically robust, quantum state tomography suffers from exponential resource demands:

   **Number of measurements**: It requires $O(D^2)$ copies of the quantum state, which is infeasible for large $n$.

   **Storage and computation**: Storing and processing the measurements scales exponentially with the system size, making tomography impractical for systems beyond a few qubits.
    O'Donnell, Ryan, and John Wright. "Efficient quantum tomography." *Proceedings of the forty-eighth annual ACM symposium on Theory of Computing*. 2016.

2. **Shadow Tomography**
   Scott Aaronson introduced shadow tomography to address the impracticality of full tomography. Shadow tomography focuses on **estimating the expectation values of specific measurements rather than reconstructing the entire density matrix.** For a given set of $M$ observables, it allows estimating probabilities $\text{Tr}(E_i \rho)$ for each observable $E_i$, with high accuracy, using only $O(\log^4 M)$ copies of the quantum state. Aaronson’s method demonstrated that we could exponentially reduce the number of measurements compared to full tomography, but at the cost of requiring computationally expensive global measurements and long quantum circuits.
   Aaronson, Scott. "Shadow tomography of quantum states." *Proceedings of the 50th annual ACM SIGACT symposium on theory of computing*. 2018.

   

3. **Classical Shadows**
   The **classical shadow** protocol, introduced by Huang, Kueng, and Preskill, builds on the ideas of shadow tomography but with significant improvements in efficiency and practicality. Instead of global measurements, classical shadows use **randomized measurements** to extract compact classical descriptions of quantum states. These descriptions enable the efficient prediction of many properties, such as expectation values and fidelities, from a logarithmic number of measurements in $M$. Classical shadows bridge the gap between theory and practice by ensuring:

   **Efficient measurement procedures**, such as random Pauli or Clifford operations.

   **Feasibility on near-term quantum hardware**.

   **Applicability to a broad range of tasks**, including verifying entanglement, estimating correlations, and predicting subsystem properties .



#### Intuition of Classical Shadows

The concept of **classical shadows** can be understood through simple analogies. Imagine you want to understand the shape of a 3D object, like a polyhedron, but you can only observe its 2D shadows. By shining light on the object from different angles and collecting its shadows, you gather enough information to infer many of its properties without ever seeing the full 3D structure.



#### How Classical Shadows Work

The classical shadow protocol constructs a **compressed classical representation of an unknown quantum state** that enables the prediction of many properties with high efficiency. The process involves the following steps:



1. **Randomized Measurements**

   For an unknown quantum state $\rho$, we randomly apply a unitary transformation $U$ from a fixed set (e.g., the Clifford group or Pauli operators) and measure the quantum state in the computational basis. The measurement outcomes provide a random **“snapshot”** of the quantum state.
   

2. **Inverse Transformation**
   For each measurement outcome $|\hat{b}\rangle$, we apply the inverse of the earlier unitary transformation, yielding the operator $U^\dagger |\hat{b}\rangle \langle \hat{b} | U$.

3. **Constructing the Shadow**

   Using a linear map $\mathcal{M}$, which depends on the chosen measurement ensemble, we compute the classical snapshot:

   $\hat{\rho} = \mathcal{M}^{-1}(U^\dagger |\hat{b}\rangle \langle \hat{b} | U).$

   Repeating this process $N$ times provides $N$ snapshots, forming the classical shadow:

   $\text{S}(\rho; N) = \{ \hat{\rho}_1, \hat{\rho}_2, \dots, \hat{\rho}_N \}.$
   

4. **Prediction**

   The classical shadow can be used to predict properties of $\rho$, such as expectation values of observables or entanglement fidelities. This is achieved by averaging over the snapshots:

   $\langle \mathcal{O} \rangle = \frac{1}{N} \sum_{i=1}^N \operatorname{tr}(\mathcal{O} \hat{\rho}_i)$, 

   where $\mathcal{O}$ is an observable.

