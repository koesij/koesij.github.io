---
layout: single
title: "2024 Quantum-Hackathon: Uniform Quantum Superposition State Preparation"
categories: ["projects"]
tags: ["quantum", "quantum computation"]
use_math: true
author_profile: false
sidebar: false
nav: "counts"
Typora-root-url: ../
---

​	

​	In recent years, the field of quantum computing and quantum machine learning has advanced significantly, with new challenges emerging around the generation and utilization of quantum superposition states. As these states are central to various algorithms and processes, their optimization and creation have become a growing focus for researchers. 

 **In the 2024 Quantum Hackathon, our team tackled the problem of generating arbitary uniform quantum superposition states (UQS).** While generating superposition states with uniform quantum amplitudes $\vert \psi \rangle = \frac{1}{\sqrt{N}}\sum^{N-1}_{j=0}\vert j \rangle$ can be straightforward for specific cases (such as $N=2^n$), creating such states for arbitary integer $N$ remains a challenging task. We first focused on generating quantum circuits for the cases $N=3, 5, 17, 29, 30, 31$ building upon the ideas from the  Quantum Fourier Transform (QFT) structure and incorporating other basic quantum gates. 

 From this starting point, we developed an algorithm capable of generating uniform quantum superposition (UQS) states for arbitrary integer $N$, beyond the initial cases considered. **Our algorithm requires $n=\lceil(\log_{2}N)\rceil$ qubits, with circuit depth of $O(\log_{2}N)$.  Additionally, it does not rely on quantum gates with multiple controls. Instead, it uses single-qubit gates, controlled rotation gates with a single control qubit.** This approach results in an exponential reduction in the number of CNOT gates compared to the Qiskit implementation for constructing UQS states.

 After developing the algorithm, we found out that it is equivalent to the one introduced in [1]. In this post, I will introduce the algorithm based on how we understood and developed it, rather than following the details from [1].



#### Inspiration from the Quantum Fourier Transform (QFT)



​	QFT can be intuitively understood as a way of transforming a quantum state from the computational (Z) basis to the Fourier basis. For a single qubit, this is done by applying a Hadamard gate, which creates an equal superposition of the basis states. 



$$
H\vert0\rangle=\frac{\vert 0 \rangle+\vert 1 \rangle}{\sqrt{2}},\ H\vert1\rangle=\frac{\vert 0 \rangle-\vert 1 \rangle}{\sqrt{2}}
$$



For multiple qubits, the QFT generalizes this concept by transforming computational basis state like $\vert k \rangle$ into superpositions of all basis states with specific phase factors. Mathematically, the QFT on a state $\vert k \rangle$ is expressed as:



$$
QFT\vert k \rangle=\frac{1}{\sqrt{N}}\sum^{N-1}_{j=0}e^{2\pi kj/N}\vert j \rangle
$$



Since the QFT is a unitary operation, it can be implemented as a quantum circuit. Below is an example of a QFT circuit for a 5-qubit case.



![QFT_image](/images/2024-09-29-Q-Hackathon/QFT_image.png)



In the QFT circuit, each qubit is placed into a superposition using a Hadamard gate, ensuring that the final state includes all possible qubit states with equal probability.

 This structure inspired an idea: instead of applying Hadamard gates uniformly to create equal superpositions, we explored the possibility of controlling the amplitudes of specific quantum states. **By replacing some of the Hadamard gates with rotation gates, we can fine-tune the quantum state amplitudes.** This approach allows us to construct UQS states for arbitrary values of $N = 3, 5, 7, \dots$.



#### UQS $(N=3)$



 **For instance, to create a UQS state for  $N = 3$, we can replace the Hadamard gate on the 0th qubit with a rotation gate  $R_Y(\theta)$  to adjust the amplitude distribution.** In this case, we choose  $\theta = tan^{-1}(\sqrt{2})$  so that when the 0th qubit is in state  $\vert 0 \rangle$ , the probability amplitude is  $\sqrt{\frac{1}{3}}$ , and when the 0th qubit is in state  $\vert 1 \rangle$ , the amplitude is $ \sqrt{\frac{2}{3}}$ .  Next, we apply a controlled Hadamard gate to the 1st qubit, with the 0th qubit as the control in state  $\vert 1 \rangle$ . This operation creates two additional states: $\vert10\rangle, \vert11\rangle$. Since we already have the state $\vert00\rangle$, this results in a superposition of 3 states in total.

The corresponding quantum circuit is shown below.



![M3_uqs](/images/2024-09-29-Q-Hackathon/M3_uqs.png)



Mathematically, the process can be represented as follows.



The system starts in the state:



$$
\vert 00 \rangle
$$



We apply the rotation gate  $R_Y(\arctan(\sqrt{2}))$  to the 0th qubit:



$$
R_Y(\arctan(\sqrt{2})) \vert 0 \rangle_0 = \cos(\arctan(\sqrt{2})) \vert 0 \rangle_0 + \sin(\arctan(\sqrt{2})) \vert 1 \rangle_0
$$



Simplifying:



$$
R_Y(\arctan(\sqrt{2})) \vert 0 \rangle_0 = \sqrt{\frac{1}{3}} \vert 0 \rangle_0 + \sqrt{\frac{2}{3}} \vert 1 \rangle_0
$$



Thus, the state of the system becomes:



$$
\sqrt{\frac{1}{3}} \vert 00 \rangle + \sqrt{\frac{2}{3}} \vert 10 \rangle
$$



We now apply a controlled Hadamard gate on the 1st qubit $C(H_1)$, controlled by the 0th qubit. 



$$
C(H_1) \vert 10 \rangle = \frac{1}{\sqrt{2}} (\vert 10 \rangle + \vert 11 \rangle)
$$



Thus, the state becomes:



$$
\sqrt{\frac{1}{3}} \vert 00 \rangle + \sqrt{\frac{2}{3}} \cdot \frac{1}{\sqrt{2}} (\vert 10 \rangle + \vert 11 \rangle)
$$



Simplifying, the final state of the system is:



$$
\vert \psi \rangle = \sqrt{\frac{1}{3}} \vert 00 \rangle + \sqrt{\frac{1}{3}} \vert 10 \rangle + \sqrt{\frac{1}{3}} \vert 11 \rangle
$$



This represents a uniform quantum superposition over 3 states.



#### UQS $(N=5)$



 For  $N = 5$ , the same method is used, but with 3 qubits because  $2^2 < 5 < 2^3$ .  We start by applying a rotation gate  $R_Y(\theta)$  to the 0th qubit, where  $\theta = \arctan(\sqrt{\frac{4}{5-4}}) = \arctan(2)$ . This controls the probability amplitude such that when the 0th qubit is  $\vert 0 \rangle$ , the amplitude is  $\sqrt{\frac{1}{5}}$ , and when it is $\vert 1 \rangle$ , the amplitude is  $\sqrt{\frac{4}{5}}$ . When the 0th qubit is in state  $\vert 1 \rangle$ , we create a superposition over the 1st and 2nd qubits. To do this, we apply a controlled Hadamard gate to the 1st qubit, with the 0th qubit acting as the control. This ensures that the Hadamard gate is applied only when the 0th qubit is  $\vert 1 \rangle$. Similarly, we apply another controlled Hadamard gate to the 2nd qubit, again controlled by the 0th qubit in the  $\vert 1 \rangle$  state. These controlled Hadamard gates create a superposition over 4 states when the 0th qubit is in  $\vert 1 \rangle$. Thus, the final superposition state for  N = 5  is created by combining the single  $\vert 000\rangle$  state when the 0th qubit is  $\vert 0\rangle$  and 4 states $\vert 100\rangle$, $\vert 101\rangle$, $\vert 110\rangle$, $\vert 111\rangle$ when the 0th qubit is  $\vert 1\rangle$ , generated by the controlled Hadamard gates on the 1st and 2nd qubits. 

The corresponding quantum circuit is shown below.



![M5_uqs](/images/2024-09-29-Q-Hackathon/M5_uqs.png)



Mathematically, the process can be represented as follows.



The system starts in the state:



$$
\vert 000 \rangle
$$



Apply the rotation gate $R_Y(\arctan(2))$  to the 0th qubit:



$$
R_Y(\arctan(2)) \vert 0 \rangle_0 = \cos(\arctan(2)) \vert 0 \rangle_0 + \sin(\arctan(2)) \vert 1 \rangle_0
$$



Simplifying:



$$
R_Y(\arctan(2)) \vert 0 \rangle_0 = \sqrt{\frac{1}{5}} \vert 0 \rangle_0 + \sqrt{\frac{4}{5}} \vert 1 \rangle_0
$$



Thus, the state becomes:



$$
\sqrt{\frac{1}{5}} \vert 000 \rangle + \sqrt{\frac{4}{5}} \vert 100 \rangle
$$



When the 0th qubit is in state  $\vert 1 \rangle$ , we apply controlled Hadamard gates $C(H)$ to the 1st and 2nd qubits, with the 0th qubit acting as the control.

First, the controlled Hadamard gate on the 1st qubit $C(H_1)$:



$$
C(H_1) \vert 100 \rangle = \frac{1}{\sqrt{2}} (\vert 100 \rangle + \vert 110 \rangle)
$$



Then, the controlled Hadamard gate on the 2nd qubit $C(H_2)$:



$$
C(H_2) \vert 1X0 \rangle = \frac{1}{2} (\vert 100 \rangle + \vert 110 \rangle + \vert 101 \rangle + \vert 111 \rangle)
$$



Thus, the state of the system becomes:



$$
\sqrt{\frac{1}{5}} \vert 000 \rangle + \sqrt{\frac{4}{5}} \cdot \frac{1}{2} (\vert 100 \rangle + \vert 101 \rangle + \vert 110 \rangle + \vert 111 \rangle)
$$



After simplifying, the final state of the system for  N = 5  is:



$$
\vert \psi \rangle = \sqrt{\frac{1}{5}} \vert 000 \rangle + \sqrt{\frac{1}{5}} (\vert 100 \rangle + \vert 101 \rangle + \vert 110 \rangle + \vert 111 \rangle)
$$



This represents a uniform quantum superposition over 5 quantum states.



#### UQS $(N=17)$



 For  $N = 17$ , the same method used for constructing UQS states in the cases of  N = 3  and  N = 5  is applied.

The circuit for  N = 17  follows this structure, as shown below.



![M17_uqs](/images/2024-09-29-Q-Hackathon/M17_uqs.png)

Mathematically, the process can be represented as follows.



The system starts in the state:


$$
\vert 00000 \rangle
$$



We apply the rotation gate  $R_Y(\theta)$  with  $\theta = \arctan(\sqrt{\frac{16}{17-16}})=\arctan(4)$ to the 0th qubit:



$$
R_{Y}(\arctan(4)) \vert 0 \rangle_0 = \cos(\arctan(4)) \vert 0 \rangle_0 + \sin(\arctan(4)) \vert 1 \rangle_0
$$



Simplifying:


$$
R_{Y}(\arctan(4)) \vert 0 \rangle_0 = \sqrt{\frac{1}{17}} \vert 0 \rangle_0 + \sqrt{\frac{16}{17}} \vert 1 \rangle_0
$$



Thus, the state of the system becomes:


$$
\sqrt{\frac{1}{17}} \vert 00000 \rangle + \sqrt{\frac{16}{17}} \vert 10000 \rangle
$$



We now apply controlled Hadamard gates to the 1st, 2nd, 3rd, and 4th qubits, with the 0th qubit acting as the control.
Apply the controlled Hadamard gate to the 1st qubit $C(H_1)$:



$$
C(H_1) \vert 10000 \rangle = \frac{1}{\sqrt{2}} (\vert 10000 \rangle + \vert 11000 \rangle)
$$



Apply the controlled Hadamard gate to the 2nd qubit $C(H_2)$:



$$
C(H_2) \vert 1X000 \rangle = \frac{1}{2} (\vert 10000 \rangle + \vert 11000 \rangle + \vert 10100 \rangle + \vert 11100 \rangle)
$$



Apply the controlled Hadamard gate to the 3rd qubit $C(H_3)$:



$$
C(H_3) \vert 1XX00 \rangle = \frac{1}{2\sqrt{2}} (\vert 10000 \rangle + \vert 11000 \rangle + \vert 10100 \rangle + \vert 11100 \rangle + \vert 10010 \rangle + \vert 11010 \rangle + \vert 10110 \rangle + \vert 11110 \rangle)
$$



Apply the controlled Hadamard gate to the 4th qubit $C(H_4)$:



$$
C(H_4) \vert 1XXX0 \rangle = \frac{1}{4} (\vert 10000 \rangle + \vert 11000 \rangle + \vert 10100 \rangle + \vert 11100 \rangle + \vert 10010 \rangle + \vert 11010 \rangle + \vert 10110 \rangle
\\
+ \vert 11110 \rangle + \vert 10001 \rangle + \vert 11001 \rangle + \vert 10101 \rangle + \vert 11101 \rangle + \vert 10011 \rangle + \vert 11011 \rangle + \vert 10111 \rangle + \vert 11111 \rangle)
$$



Simplifying, the final state of the system is:


$$
\vert \psi \rangle = \sqrt{\frac{1}{17}} \vert 00000 \rangle + \sqrt{\frac{1}{17}} \sum_{i=1}^{16} \vert 1XXXX \rangle
$$



This represents a uniform quantum superposition over 17 quantum states.



#### Binary Representation of $N$



​	**The circuits we have studied so far can be understood as constructing a UQS state by expressing  $N$  in its binary form and applying controlled Hadamard gates based on the binary digits (bits).** For instance, in the case of  $N = 3$ , its binary representation is $ 11_2$ , meaning  $N = 2 + 1$ .  Therefore, we applied a controlled Hadamard gate to the 1st qubit to create 2 superposition states. For  $N = 5$ , the binary form is  $101_2$ , meaning  $N = 4 + 1$ . We applied controlled Hadamard gates to both the 1st and 2nd qubits to create 4 superposition states. Similarly, for  $N = 17$ , its binary form is  $10001_2$ , meaning  $N = 16 + 1$ . We applied controlled Hadamard gates accordingly.

This method generalizes to any integer  $N$ since any integer can be expressed in binary form. For example,  $N = 29$  is represented as  $11101_2 = 16 + 8 + 4 + 1$ ,  $N = 30$  as  $11110_2 = 16 + 8 + 4 + 2$ , and  $N = 31$  as  $11111_2 = 16 + 8 + 4 + 2 + 1$ . In the following sections, we will explore these cases in detail, as we did for  $N = 3, 5, 17$, and introduce a python code that can generate a UQS state for any integer  $N$, using its binary representation to guide the construction.



#### UQS $(N=29)$ 



 For  $N = 29$ , we can express it as  $N = 16 + 8 + 4 + 1$ . Similar to the previous cases, we start by assigning a probability amplitude of  $\sqrt{\frac{16}{29}}$  when the 0th qubit is  $\vert 1\rangle$ , allowing us to create a superposition over 16 states. To achieve this, the rotation gate $R_Y(\theta)$ on the 0th qubit must have a rotation angle  $\theta = \arctan(\sqrt{\frac{16}{29 - 16}}) = \arctan(\sqrt{\frac{16}{13}})$ . Once this rotation is applied, we use controlled Hadamard gates to ensure that when the 0th qubit is  $\vert 1\rangle$ , the next 4 qubits are placed into an equal superposition.

 **Next, we handle the remaining terms  8 ,  4 , and  1  in the binary representation of  $N$ . We apply a controlled rotation  gate $C(R_Y(\theta))$ to the 1st qubit to preserve the superposition we created earlier when the 0th qubit is  $\vert 1\rangle$ .** Now, to assign a probability amplitude of  $\sqrt{\frac{8}{29}}$  when the 0th qubit is  $\vert 0\rangle$  and the 1st qubit is  $\vert1\rangle$ , ensuring equal superposition over 8 states, the controlled rotation  gate’s angle should be  $\theta = \arctan(\sqrt{\frac{8}{13 - 8}})$ . Afterward, we apply a controlled Hadamard gate to superposition the next 3 qubits, while ensuring the 0th qubit and 1st qubit remains  $\vert 0\rangle$ and  $\vert 1 \rangle$ respectively.

 Similarly, for the 2nd qubit, we apply a controlled rotation gate $C(R_Y(\theta))$ with an angle $\theta = \arctan(\sqrt{\frac{4}{5 - 4}})$ , followed by controlled Hadamard gates to ensure that the 0th and 1st qubits remain  $\vert 00\rangle$, while the 2nd qubit is set to  $\vert 1\rangle$ , allowing the remaining qubits to superposition.

Since, we did not mess with the  $\vert 00000\rangle$  state created during the first rotation gate $R_Y(\theta)$, we now have a uniform superposition of 29 quantum states.

The circuit for  $N = 29$  follows this structure, as shown below.



![M29_uqs](/images/2024-09-29-Q-Hackathon/M29_uqs.png)

Mathematically, the process can be represented as follows.



The system starts in the state:


$$
\vert 00000 \rangle
$$



We apply the rotation gate $R_Y(\theta)$ with $\theta = \arctan(\sqrt{\frac{16}{29 - 16}}) = \arctan(\sqrt{\frac{16}{13}})$  to the 0th qubit:



$$
R_Y(\arctan(\sqrt{\frac{16}{13}})) \vert 0 \rangle_0 = \cos(\arctan(\sqrt{\frac{16}{29}})) \vert 0 \rangle_0 + \sin(\arctan(\sqrt{\frac{13}{29}})) \vert 1 \rangle_0
$$



Simplifying:


$$
R_Y(\arctan(2)) \vert 0 \rangle_0 = \sqrt{\frac{13}{29}} \vert 0 \rangle_0 + \sqrt{\frac{16}{29}} \vert 1 \rangle_0
$$



Thus, the state of the system becomes:


$$
\sqrt{\frac{13}{29}} \vert 00000 \rangle + \sqrt{\frac{16}{29}} \vert 10000 \rangle
$$



We now apply controlled Hadamard gates to the 1st, 2nd, 3rd, and 4th qubits, with the 0th qubit acting as the control. When the 0th qubit is  $\vert 1\rangle$ , the controlled Hadamard gates create the superposition over 16 states.



Apply the controlled Hadamard gate to the 1st qubit $C(H_1)$:



$$
C(H_1) \vert 10000 \rangle = \frac{1}{\sqrt{2}} (\vert 10000 \rangle + \vert 11000 \rangle)
$$



Apply the controlled Hadamard gate to the 2nd qubit $C(H_2)$:



$$
C(H_2) \vert 1X000 \rangle = \frac{1}{2} (\vert 10000 \rangle + \vert 11000 \rangle + \vert 10100 \rangle + \vert 11100 \rangle)
$$



Apply the controlled Hadamard gate to the 3rd qubit $C(H_3)$:



$$
C(H_3) \vert 1XX00 \rangle = \frac{1}{2\sqrt{2}} (\vert 10000 \rangle + \vert 11000 \rangle + \vert 10100 \rangle + \vert 11100 \rangle + \vert 10010 \rangle + \vert 11010 \rangle + \vert 10110 \rangle + \vert 11110 \rangle)
$$



Apply the controlled Hadamard gate to the 4th qubit $C(H_4)$:



$$
C(H_4) \vert 1XXX0 \rangle = \frac{1}{4} (\vert 10000 \rangle + \vert 11000 \rangle + \vert 10100 \rangle + \vert 11100 \rangle + \vert 10010 \rangle + \vert 11010 \rangle + \vert 10110 \rangle
\\+ \vert 11110 \rangle + \vert 10001 \rangle + \vert 11001 \rangle + \vert 10101 \rangle + \vert 11101 \rangle + \vert 10011 \rangle + \vert 11011 \rangle + \vert 10111 \rangle + \vert 11111 \rangle)
$$



Thus, the state becomes:


$$
\sqrt{\frac{13}{29}} \vert 00000 \rangle + \sqrt{\frac{16}{29}} \cdot \frac{1}{\sqrt{16}} \sum_{i=0}^{15} \vert 1XXXX \rangle
$$



Simplifying:


$$
\sqrt{\frac{13}{29}} \vert 00000 \rangle + \sqrt{\frac{1}{29}} \sum_{i=1}^{16} \vert 1XXXX \rangle
$$



Next, we handle the remaining terms (8, 4, and 1) in the binary representation of  $N = 29$.


 For the 1st qubit we apply a controlled rotation gate $C(R_Y(\theta))$ with $\theta = \arctan(\sqrt{\frac{8}{13 - 8}})=\arctan(\sqrt{\frac{8}{5}})$ , ensuring that when the 0th qubit is  $\vert 0\rangle$: 



$$
C(R_Y(\arctan(\sqrt{\frac{8}{5}}))) \vert 00000 \rangle = \sqrt{\frac{5}{13}} \vert 00000 \rangle + \sqrt{\frac{8}{13}} \vert 01000 \rangle
$$



From this point onward, the remaining process follows the same method as described above. We continue applying controlled Hadamard gates to create superpositions over the remaining states, just as we did for the earlier qubits. This process is straightforward and can be easily followed.

The final state of the system after completing the process is:



$$
\vert \psi \rangle = \sqrt{\frac{1}{29}} \vert 00000 \rangle + \sqrt{\frac{1}{29}} \sum_{i=1}^{16} \vert 1XXXX \rangle+\sqrt{\frac{1}{29}} \sum_{i=1}^{8} \vert 01XXX \rangle +\sqrt{\frac{1}{29}} \sum_{i=1}^{4} \vert 001XX \rangle
$$



This represents a uniform quantum superposition over 29 quantum states.



#### UQS $(N=30, 31)$



 For the cases of  $N = 30$  and  $N = 31$ , the same method we’ve discussed so far is followed to construct the UQS states. The process involves using controlled rotation gates to adjust the probability amplitudes and applying controlled Hadamard gates to create superpositions over the corresponding quantum states, just as we did for previous values of  $N$.

Here is the UQS circuit for  $N = 30$:

 ![M30_uqs](/images/2024-09-29-Q-Hackathon/M30_uqs.png)



UQS circuit for  $N = 31$:



![M31_uqs](/images/2024-09-29-Q-Hackathon/M31_uqs.png)

#### UQS Circuit Construction for Arbitary Integer N in Code



The following code constructs UQS circuit for any arbitrary integer $N$, as we have discussed previously.
(This implementation is written using the Pennylane[2] library.)



Import Module

```python
import pennylane as qml
from pennylane import numpy as np
import matplotlib.pyplot as plt
```



Calculating Powers of $2$ for $M$

```python
def powers_of_2(M):
    powers = []
    bit_position = 0
    while M > 0:
        if M & 1:
            powers.append(bit_position)
        M = M >> 1
        bit_position += 1
        
    return list(reversed(powers))
```



Calculating the $\theta$ Values for $R_Y$ gates
```python
def RY_thetas(M):
    powers = powers_of_2(M)
    
    thetas = []
    current_sum = 0
    
    for p in (powers):
        if p == powers[-1]:
            break
        
        theta = 2*np.arctan(np.sqrt(2**p / (M - current_sum - 2**p)))
        
        thetas.append(theta)
        current_sum += 2**p
        
    return thetas, powers
```



Constructing the UQS Circuit

```python
def uqs(M):
    thetas, powers = RY_thetas(M)
    n_qubits = powers[0] + 1
    
    @qml.qnode(qml.device('default.qubit', wires=n_qubits))
    def circuit():
        
        for ry_target in range(len(thetas)):
            ry_control = list(range(ry_target))
            
            if ry_control:
                qml.ctrl(qml.RY, control=ry_control, control_values=[0] * len(ry_control))(thetas[ry_target], wires=ry_target)
            else:
                qml.RY(thetas[ry_target], wires=ry_target)
                
            
            for h_target in range(ry_target + 1, ry_target + 1 + powers[ry_target]):
                h_control = list(range(ry_target + 1))
                if h_control:
                    h_control_val = [0] * len(h_control)
                    h_control_val[-1] = 1
                    qml.ctrl(qml.Hadamard, control=h_control, control_values=h_control_val)(wires=h_target)
                        
        
        if powers[-1] != 0:
            for p in range(powers[-1]):
                qml.ctrl(qml.Hadamard, control=list(range(len(thetas))), control_values=[0] * len(thetas))(wires=len(thetas)+p)
                
        return qml.state()
    
    return circuit
```



Creating and Plotting the UQS Circuit for $N = 31$

```python
M =  #My birthday is the 23th of July
thetas, powers = RY_thetas(M)
print(thetas)
print(powers)

uqs_circuit = uqs(M)
drawer = qml.draw(uqs_circuit)
qml.draw_mpl(uqs_circuit)()
```

 [1.6030599884631436, 1.637512475205122, 1.714143895700262, 1.9106332362490186] 

[4, 3, 2, 1, 0] 



![M31_uqs](/images/2024-09-29-Q-Hackathon/M31_uqs.png)



Executing the Circuit and Plotting the Measurement Results

```python
probability_amplitudes = uqs_circuit()
probabilities = np.abs(probability_amplitudes) ** 2

num_qubits = len(probabilities).bit_length() - 1

plt.bar(range(len(probabilities)), probabilities)
plt.xlabel('States')
plt.ylabel('Probabilities')
plt.title('Measurement results')

plt.xticks(range(len(probabilities)), [f'{i:0{num_qubits}b}' for i in range(len(probabilities))], rotation=90)

nonzero_probabilities = np.count_nonzero(probabilities > 0)
plt.text(0.65, 1.1, f'Nonzero probabilities: {nonzero_probabilities}', transform=plt.gca().transAxes)

plt.show()
```



![M31_measure](/images/2024-09-29-Q-Hackathon/M31_measure-7243670.png)



#### Burden of Multi-Qubit Control



​	In the construction of UQS states, particularly for larger values of $N$, such as $N = 29, 30, 31$, the use of multi-qubit controlled gates is introduced. **These multi-control gates are typically decomposed into simpler two-qubit gates, such as Echoed Cross-Resonance (ECR) gates, during transpilation.** The ECR gate, like the CNOT gate, is a two-qubit gate used to create entanglement between qubits in superconducting quantum processors. **For example, in the case of the UQS circuit for $N = 31$, after being transpiled by Qiskit's[3] transpiler for IBM-Kyto, the circuit resulted in 643 ECR gates.** While these gates are necessary for implementing multi-qubit control, their use significantly increases the circuit’s depth and adds noise. This can place a heavy load on NISQ hardware, making it challenging to achieve reliable results.

 **Therefore, an efficient algorithm that minimizes or avoids the use of multi-qubit controlled gates is essential for improving performance on NISQ computers.**



#### UQS Preparation Without Multi-Qubit Control



​	In our previous method, we used multi-controlled qubits to preserve the probability amplitudes of the constructed states. For example, in the case of  $N = 29$ , part 1 of the figure below shows that four controlled Hadamard gates create 16 superposition states when the 0th qubit is  $\vert 1 \rangle$ . To avoid disturbing these states, the three controlled Hadamard gates in part 2 are controlled not only by the 1st qubit but also by the 0th qubit. A similar approach is applied to the Hadamard gates in part 3. **As  $N$  increases, this method requires an increasing number of multi-controlled qubits.**



![M29_part](/images/2024-09-29-Q-Hackathon/M29_part.png)



 **To overcome this limitation, our team developed an algorithm that eliminates the need for quantum gates with multiple controls. It uses single-qubit gates and controlled rotation gates with only a single control qubit.**

 The development of this algorithm began with the question: **Can we utilize the quantum states prepared in earlier steps to generate the additional states required for UQS preparation?** This idea arose because, instead of preserving the previously constructed states, we hypothesized that we might be able to avoid the need for multi-controlled qubits by utilizing those states. **To explore this, we considered reversing the process used in the previous method.**

 In the previous method, states corresponding to the largest powers of 2 in the binary representation of  $N$  were constructed first. For example, in the case of $N = 29 = 16 + 8 + 4 + 1$ , the states representing 16 were created first, followed by the states for 8, 4 and 1. **To take advantage of the states already prepared, our new approach begins by constructing states corresponding to the smallest powers of 2 first, then gradually building up to the larger powers of 2.** To understand this idea and see how the implementation works in practice, let's dive deeper into this approach by examining specific cases.



#### UQS w/o Multi-Qubit Control $(N=7)$



 The figure below shows the quantum circuit that generates the UQS states for $N=7$ using our new algorithm. First, we apply a rotation gate to the 1st qubit to initialize the superposition of two states. The rotation angle, $\theta$, is set to $arctan(\sqrt{\frac{7-2^0}{2^0}})=\arctan(\sqrt{6})$, since the $\vert 000 \rangle$ state corresponds to $2^0$ in the binary representation of 7. Next, we apply a controlled Hadamard gate to the 0th qubit, controlled by the 1st qubit when it is in the $\vert 1 \rangle$ state. At this point, we have the superposition of the $2^0$ and $2^1$ quantum states. Afterward, we introduce the 2nd qubit into the superposition by applying a controlled rotation gate when the 1st qubit is in the  $\vert 1 \rangle$  state. Since we need to generate  $2^2$  states from the existing  $2^1$  states, the rotation angle  $\theta$  is calculated as  $arctan(\frac{7 - 2^1 - 2^0}{2^1})$ . Finally, we apply another controlled Hadamard gate to the 1st qubit to superpose the $2^2$  state, combining it with the previously created quantum states. As a result, we end up with a superposition of the  $N=7=2^0 + 2^1 + 2^2$  quantum states.



![M7_eff](/images/2024-09-29-Q-Hackathon/M7_eff.png)

Mathematically, the process can be represented as follows.



The system starts in the state:

$$
\vert 000 \rangle
$$

We apply the rotation gate  $R_Y(\theta)$  with  $\theta = \arctan\left(\sqrt{\frac{7 - 2^0}{2^0}}\right)  = \arctan(\sqrt{6})$  to the 1st qubit:


$$
R_Y(\arctan(\sqrt{6})) \vert 0 \rangle_1 = \cos(\arctan(\sqrt{6})) \vert 0 \rangle_1 + \sin(\arctan(\sqrt{6})) \vert 1 \rangle_1
$$



Simplifying:


$$
R_Y(\arctan(\sqrt{6})) \vert 0 \rangle_1 = \sqrt{\frac{1}{7}} \vert 0 \rangle_1 + \sqrt{\frac{6}{7}} \vert 1 \rangle_1
$$



Thus, the state of the system becomes:


$$
\sqrt{\frac{1}{7}} \vert 000 \rangle + \sqrt{\frac{6}{7}} \vert 010 \rangle
$$



Next, we apply a controlled Hadamard gate to the 0th qubit, controlled by the 1st qubit when it is in the  $\vert 1 \rangle$  state:


$$
C(H_0) \vert 010 \rangle = \frac{1}{\sqrt{2}} (\vert 010 \rangle + \vert 110 \rangle)
$$



At this point, the state of the system becomes:


$$
\sqrt{\frac{1}{7}} \vert 000 \rangle + \sqrt{\frac{6}{7}} \cdot \frac{1}{\sqrt{2}} (\vert 010 \rangle + \vert 110 \rangle)
$$



Simplifying:


$$
\sqrt{\frac{1}{7}} \vert 000 \rangle + \sqrt{\frac{3}{7}} (\vert 010 \rangle + \vert 110 \rangle)
$$



Now, we apply a controlled rotation gate  $C(R_Y(\theta))$  to the 2nd qubit, controlled by the 1st qubit. Since we need to generate  $2^2$  states from  $2^1$  states, the rotation angle  $\theta$  is calculated as:


$$
\theta = \arctan\left(\sqrt{\frac{7 - 2^1 - 2^0}{2^1}}\right) = \arctan\left(\sqrt{\frac{7 - 3}{2}}\right) = \arctan(\sqrt{2})
$$



Thus, the controlled rotation gate creates the following transformation:


$$
C(R_Y(\arctan(\sqrt{2}))) (\vert 010 \rangle+\vert 110 \rangle) = \sqrt{\frac{1}{3}} (\vert 010 \rangle + \vert 110 \rangle) + \sqrt{\frac{2}{3}} (\vert 011 \rangle + \vert 111 \rangle)
$$



Finally, we apply another controlled Hadamard gate to the 1st qubit, creating the superposition over  $2^2$  states:


$$
C(H_1) \vert \psi \rangle = \sqrt{\frac{1}{7}} \vert 000 \rangle + \sqrt{\frac{3}{7}}\cdot \frac{1}{\sqrt{3}} (\vert 100 \rangle + \vert 110 \rangle) + \sqrt{\frac{3}{7}}\cdot\sqrt{\frac{2}{3}}\cdot\sqrt{\frac{1}{2}} (\vert 001 \rangle + \vert 011 \rangle + \vert 101 \rangle + \vert 111 \rangle)
$$



Thus, the final state of the system is:


$$
\vert \psi \rangle = \sqrt{\frac{1}{7}} \vert 000 \rangle + \sqrt{\frac{1}{7}} (\vert 100 \rangle + \vert 110 \rangle) + \sqrt{\frac{1}{7}} (\vert 001 \rangle + \vert 011 \rangle + \vert 101 \rangle + \vert 111 \rangle)
$$



This represents a uniform quantum superposition over  $2^0 + 2^1 + 2^2$  quantum states for  $N = 7$.



#### UQS w/o Multi-Qubit Control $(N=22)$



 The figure below shows the quantum circuit that generates the UQS states for  $N = 22$  using our new algorithm. First, note that 22 is an even number. For even values of  $N$ , we express  $N$  as $2^n$ and an odd number. In this case,  22 = $2^1 \times 11$ . The strategy is to first construct the UQS for the odd component and then extend it by adding a Hadamard gate to an additional qubit, multiplying the number of states by  $2^n$ . This ensures that the quantum states are uniformly superposed over the desired number of states.



UQS circuit for  $N = 22$:

![M22_eff](/images/2024-09-29-Q-Hackathon/M22_eff.png)

 Next, we need to construct the quantum states for  $N = 11$ . The binary representation of 11 is  $2^3 + 2^1 + 2^0$ . Most of the process is similar to the one used for  $N = 7$ . However, the key difference is that in the final step, a controlled Pauli-X gate is applied. This adjustment is necessary because instead of generating  $2^2$  states, we want achieve  $2^4$  states using the quantum states constructed in the previous steps. To illustrate this more clearly, I will represent the process mathematically for the case of  $N = 11$  and then extend it to  $N = 22$.



UQS circuit for  $N = 11$:



![M11_eff](/images/2024-09-29-Q-Hackathon/M11_eff.png)



The system starts in the state ($N=11$):


$$
\vert 0000 \rangle
$$


We apply a rotation gate  $R_Y(\theta)$  with  $\theta=\arctan\left(\sqrt{\frac{11 - 2^0}{2^0}}\right)  = \arctan(\sqrt{10})$  to the 1st qubit:


$$
R_Y(\arctan(\sqrt{10})) \vert 0 \rangle_1 = \cos(\arctan(\sqrt{10}) \vert 0 \rangle_1 + \sin(\arctan(\sqrt{10}) \vert 1 \rangle_1
$$


Simplifying:


$$
\sqrt{\frac{1}{11}} \vert 0 \rangle_1 + \sqrt{\frac{10}{11}} \vert 1 \rangle_1
$$


Next, we apply a controlled Hadamard gate to the 0th qubit, controlled by the 1st qubit when it is in the  $\vert 1 \rangle$  state:


$$
C(H_0) \vert 0100 \rangle = \frac{1}{\sqrt{2}} (\vert 0100 \rangle + \vert 1100 \rangle)
$$


The state of the system now becomes:


$$
\sqrt{\frac{1}{11}} \vert 0000 \rangle + \sqrt{\frac{10}{11}} \cdot \frac{1}{\sqrt{2}} (\vert 0100 \rangle + \vert 1100 \rangle)
$$


Now, we apply a controlled rotation gate  $C(R_Y(\theta))$  to the 2nd qubit, controlled by the 1st qubit. Since we need to generate  $2^3$  states from the existing  $2^1$  states, the rotation angle  $\theta$  is calculated as:


$$
\theta = \arctan\left(\sqrt{\frac{11 - 2^1 - 2^0}{2^1}}\right) = \arctan\left(\sqrt{\frac{11 - 3}{2}}\right) = \arctan(\sqrt{4}) = \arctan(2)
$$


Thus, the controlled rotation gate creates the following transformation:


$$
C(R_Y)(\arctan(2))) (\vert 0100 \rangle + \vert 1100 \rangle) = \sqrt{\frac{1}{5}} (\vert 0100 \rangle + \vert 1100 \rangle) + \sqrt{\frac{4}{5}} (\vert 0110 \rangle + \vert 1110 \rangle)
$$


The state now becomes:


$$
\sqrt{\frac{1}{11}} \vert 0000 \rangle + \sqrt{\frac{10}{11}} \cdot\sqrt{\frac{1}{2}}\cdot \sqrt{\frac{1}{5}} (\vert 0100 \rangle + \vert 1100 \rangle) + \sqrt{\frac{10}{11}} \cdot \sqrt{\frac{1}{2}}\cdot\sqrt{\frac{4}{5}} (\vert 0110 \rangle + \vert 1110 \rangle)
$$


Simplifying:


$$
\sqrt{\frac{1}{11}} \vert 0000 \rangle + \sqrt{\frac{1}{11}} (\vert 0100 \rangle+\vert 1100 \rangle)+ \sqrt{\frac{4}{11}} (\vert 0110 \rangle+\vert 1110 \rangle)
$$


Now, we apply a controlled Hadamard gate to the 1nd qubit, controlled by the 2rd qubit when it is in the  $\vert 1 \rangle$  state:


$$
C(H_1) \vert X110 \rangle = \frac{1}{\sqrt{2}} (\vert X010 \rangle-\vert X110 \rangle)
$$


The state now becomes:


$$
\sqrt{\frac{1}{11}} \vert 0000 \rangle + \sqrt{\frac{1}{11}} (\vert 0100 \rangle+\vert 1100 \rangle)+ \sqrt{\frac{2}{11}} (\vert 0010 \rangle-\vert 0110 \rangle+\vert 1010 \rangle-\vert 1110 \rangle)
$$




Finally, we apply a controlled Pauli-X gate to the 3rd qubit, controlled by the 2nd qubit in the  $\vert 1 \rangle$  state:


$$
C(X_3) \vert XX10 \rangle = \vert XX1(1 \oplus 0) \rangle
$$


Applying it to the current state:


$$
\sqrt{\frac{1}{11}} \vert 0000 \rangle + \sqrt{\frac{1}{11}} (\vert 0100 \rangle+\vert 1100 \rangle)+ \sqrt{\frac{2}{11}} (\vert 0011 \rangle-\vert 0111 \rangle+\vert 1011 \rangle-\vert 1111 \rangle)
$$


Now, we apply a controlled Hadamard gate to the 2nd qubit, controlled by the 3rd qubit when it is in the  $\vert 1 \rangle$  state:


$$
C(H_2) (\vert X011 \rangle-\vert X111 \rangle) = \sqrt\frac{1}{2}\vert XXX1 \rangle
$$


This results in the final state:


$$
\vert \psi \rangle = \sqrt{\frac{1}{11}} \vert 0000 \rangle + \sqrt{\frac{1}{11}} (\vert 0100 \rangle+\vert 1100 \rangle) + 
\\
\sqrt{\frac{1}{11}} (\vert 0001\rangle+\vert 0011 \rangle+\vert 0101 \rangle+\vert 0111 \rangle+\vert 1001\rangle+\vert 1011 \rangle+\vert 1101 \rangle+\vert 1111 \rangle)
$$


This represents a uniform quantum superposition over  $2^0 + 2^1 + 2^3$  quantum states for  $N = 11$.



The only difference for  N = 22  is the inclusion of an additional qubit with a Hadamard gate applied to it. This modification ensures that the quantum superposition now uniformly covers all 22 states.



#### UQS Circuit w/o Multi-Qubit Control for Arbitary Integer $N$ in Code



The following code constructs UQS circuit w/o Multi-Qubit Control for any arbitrary integer $N$.
(This implementation is written using the Pennylane [2] library.)

Import Module

```python
import pennylane as qml
from pennylane import numpy as np
import matplotlib.pyplot as plt
```



Calculating Powers of $2$ for $M$

```python
def powers_of_2(M):
    powers = []
    bit_position = 0
    while M > 0:
        if M & 1:
            powers.append(bit_position)
        M = M >> 1
        bit_position += 1
        
    return list(reversed(powers))
```



Calculating the $\theta$ Values for $R_Y$ gates

```python
def RY_eff_thetas(M):
    powers = powers_of_2(M)
    
    thetas = []
    current_sum = M
    
    for p in reversed(powers):
        if p == powers[0]:
            break
        current_sum -= 2**p
        print(current_sum)
        
        ratio = current_sum / (2**p)
        
        theta = 2*np.arctan(np.sqrt(ratio))
        thetas.append(theta)
        
    return thetas, powers
```



Constructing the UQS Circuit

```python
def uqs_efficient(M):
    
    counts = 0
    while M % 2 == 0:
        M //= 2
        counts += 1

    thetas, powers = RY_eff_thetas(M)
    
    if powers:
        n_qubits = powers[0] + 1 + counts
    else:
        n_qubits = counts
        
    @qml.qnode(qml.device('default.qubit', wires=n_qubits))
    def circuit():
    
        def A_gate(i, theta):
            qml.RY(theta, wires=i+1)
            qml.ctrl(qml.Hadamard, control=i+1, control_values=1)(wires=i)
    
        def B_gate(i, theta):
            qml.ctrl(qml.RY, control=i, control_values=1)(theta, wires=i+1)
            qml.ctrl(qml.Hadamard, control=i+1, control_values=1)(wires=i)
        
        def S_gate(i):
            qml.ctrl(qml.PauliX, control=i, control_values=1)(wires=i+1)
            qml.ctrl(qml.Hadamard, control=i+1, control_values=1)(wires=i)
        
        for i in range(counts):
            qml.Hadamard(wires=i)
            
        if M == 1:
            return qml.state()

        else:
            A_gate(counts, thetas[0])
            
            k = 1
            
            for j in range(1, powers[0]):
                if j in powers:
                    B_gate(counts + j, thetas[k])
                    k += 1

                else:
                    S_gate(counts+j)

            return qml.state()

    return circuit
```



Creating and Plotting the UQS Circuit for $N = 26$

```python
M = 26
uqs_eff_circuit = uqs_efficient(M)
drawer = qml.draw(uqs_eff_circuit)
print(drawer())
qml.draw_mpl(uqs_eff_circuit)()
```



![M26_eff](/images/2024-09-29-Q-Hackathon/M26_eff.png)



Executing the Circuit and Plotting the Measurement Results

```python
probability_amplitudes = uqs_eff_circuit()
probabilities = np.abs(probability_amplitudes) ** 2

num_qubits = len(probabilities).bit_length() - 1

plt.bar(range(len(probabilities)), probabilities, color='gray')
plt.xlabel('States')
plt.ylabel('Probabilities')
plt.title('Measurement results')

plt.xticks(range(len(probabilities)), [f'{i:0{num_qubits}b}' for i in range(len(probabilities))], rotation=90)

nonzero_probabilities = np.count_nonzero(probabilities > 0.0)
plt.text(0.65, 1.1, f'Nonzero probabilities: {nonzero_probabilities}', transform=plt.gca().transAxes)

plt.show()
```



![M26_measure](/images/2024-09-29-Q-Hackathon/M26_measure.png)



#### Complexity Explanation of UQS circuit w/o Multi-Qubit Control



**Number of Qubits:** $n=\lceil \log_2{N} \rceil$

The number of qubits required for creating a UQS state for an integer  $N$  is determined by the binary representation of  $N$ . If  $N$  is represented in binary form as:

$$
N = b_{n-1}b_{n-2}\ldots b_1 b_0,
$$

**where  $b_i$  are the binary digits (either 0 or 1) and  $n = \lceil \log_2(N) \rceil$ , then the number of qubits needed is exactly  $n$ .** Each qubit corresponds to one digit in the binary representation, ensuring that we can represent  $2^n$  unique states. This means that the total number of qubits required scales logarithmically with  $N$ .

For example, for  $N = 22$ , the binary representation is  $10110_2$ , which has 5 bits. Therefore, we need 5 qubits to encode all the states up to  $N = 22$ . More generally, if  $N$  has  $n$  binary digits, the number of qubits required is  $O(\log_2 N)$ .



**Circuit Depth:** $O(\log_2N)$

The circuit depth is determined by the number of operations (gates) required to create the uniform superposition. This is also influenced by the binary representation of  $N$ .

**Each step of the circuit construction involves adding a new set of superposition states based on the binary digits set to 1 in  $N $. For each power of 2 represented by  $b_i = 1$ , a controlled rotation gate and a controlled Hadamard gate are applied, both of which are single-controlled gates. For the powers of 2 where  $b_i = 0$ , a CNOT gate followed by a controlled Hadamard gate with a single control qubit is used to skip over the absent states and continue constructing the superposition.** The implementation of this process can be seen in the code above.

**Therefore, in either case, each binary digit  $b_i$  requires exactly 2 single-controlled gates, as you can see from the code that constructs the UQS circuit without multi-qubit control. Thus, the circuit depth for  $n = \lceil \log_2(N) \rceil$ digits in the binary representation is proportional to  $O(\log_2 N)$ .**



#### About 2024 Q-Hackathon



​	In the 2024 Q-Hackathon, participants were presented with various topics to tackle, including quantum error correction, quantum encoding (which we chose), quantum information, classical shadows, quantum machine learning, and quantum circuit transpilation, among others. The event was supported by mentors who are active researchers from National Labs in Korea, professors from various universities, and industry experts from IBM Quantum, Samsung, IONQ, PASCAL.

 The hackathon was held over three days and nights. Thanks to the support from IBM and IONQ, we were able to run our circuits on real quantum hardware and gained valuable experience in mitigating errors and analyzing the error rates and characteristics of different quantum devices.

 The event featured 24 teams (consisting of 101 graduate and undergraduate students) from diverse universities. We were honored to win 2nd place in the competition and were awarded at the '2024 Quantum Korea'. It was a great honor, and I truly enjoyed every moment from brainstorming solutions to collaborating with my teammates.

 I would like to express a huge thanks to the mentors and everyone who organized and participated in the event. I'm also grateful to Professor Kunwoo Kim for his lectures on 'Quantum Information and Quantum Computation'. The knowledge from those lectures, covering topics like quantum algorithms and quantum entanglement, played a significant role in helping our team tackle the problems.

 This event was a major milestone for me and I'm excited to continue my journey in exploring the world of quantum computing. 



You can see us receiving the award in [4]. For a detailed overview of the 2024 Q-Hackathon, you can watch [5].





[1] "Shukla, Alok, and Prakash Vedula. "An efficient quantum algorithm for preparation of uniform quantum superposition states." *Quantum Information Processing* 23.2 (2024): 38."

[2] https://pennylane.ai/

[3] https://www.ibm.com/quantum/qiskit

[4] https://www.lecturernews.com/news/articleView.html?idxno=155271

[5] https://youtu.be/R1HYkRDAkeY?si=8M4mDqCuUFAzbh6l

