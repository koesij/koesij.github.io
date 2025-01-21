#### Introduction 

My research objective is leveraging AI to understand and control quantum systems. This objective stems from my ongoing research with Prof. Kunwoo Kim and Prof. Jaedong Noh, where we focus on developing reinforcement learning-based control protocols for active matter and understanding these AI-generated protocols through the lens of non-equilibrium statistical mechanics. During this project, I found myself frequently asking, *Can we apply these methods to quantum systems?* This curiosity has driven my desire to explore how reinforcement learning can extend to quantum control problems and to further deepen our understanding of quantum systems with the help of AI.

#### Research Experience

**Optimal Control Protocols for Active Matter:** My research with Professor Kunwoo Kim and Jaedong Noh revolves around developing reinforcement learning-based control protocols to steer active matter systems efficiently. The initial motivation for this project came from the paper[1]. This study explores how neural networks can be employed to control fluctuating nano systems, optimizing processes such as work extraction and entropy absorption. A particularly fascinating finding was that by providing global measurements as inputs to the neural network at each control step, the system's entropy production could be driven to negative values. This phenomenon is akin to harnessing energy from thermal fluctuations through measurement information, reminiscent of the concepts found in information engines.

 Inspired by these insights, we sought  to apply similar ideas to active matter systems. Our goal became steering active matter from an initial state to a target state while simultaneously harnessing energy from the system itself. For example, this approach could be visualized as redirecting a flock of birds to avoid entering a restricted airspace, using minimal external energy, or guiding them using their own kinetic energy.

During the project, we encountered challenges in calculating the Entropy Production Rate (EPR) when applying external fields to the Hamiltonian flocking model. Theoretical expectations suggested that the EPR would increase when a field was applied due to the increased irreversibility. However, our simulations showed no such change, even with the applied field. This led us to carefully review our approach, where we confirmed that the phase transition and steady-state EPR were consistent with the numerical and analytical results presented in a foundational paper[2] analyzing the Hamiltonian flocking model at steady state. With this confirmation, our focus then shifted to re-examining the mathematical framework used in the presence of external fields.

 Re-examining the derivations, we realized that our calculations had incorrectly treated the field term, failing to account for the nuances of the Stratonovich prescription in time-reversal transformations. Recognizing this, I derived a revised formulation that properly incorporated the field’s influence under time reversal. This corrected the inconsistency, and I implemented the updated equations into our numerical simulations. As a result, the simulations aligned with our expectations, showing that the EPR indeed increased with the application of an external field. This experience taught me the importance of precise mathematical reasoning in complex systems and deepened my understanding of the interplay between theoretical and computational approaches in non-equilibrium systems.

Another key challenge was integrating the CUDA C++ simulations with the PyTorch-based neural network to create a feedback control system. For each control step, I ran the numerical simulation using CUDA C++ for a given time duration, then transferred the resulting data to PyTorch, making it accessible for the neural network. The neural network processed this data and output control parameters—such as adjustments to the external field and temperature—which were then applied back to the simulation. This iterative process allowed the simulation and the neural network to interact continuously, forming a real-time feedback loop. By effectively combining the strengths of CUDA C++ for high-performance simulations and PyTorch for neural network training, I enabled a seamless integration of numerical and AI methodologies.



**Q-Hackathon:** In the 2024 Quantum Hackathon, I led the implementation of quantum circuits using the PennyLane library, focusing on generating arbitrary uniform quantum superposition (UQS) states. This challenge involved designing circuits for cases where $N$ is not a power of two, a non-trivial task due to the need to balance quantum state amplitudes precisely. 

Our initial approach was inspired by the Quantum Fourier Transform (QFT), which guided the construction of a quantum circuit algorithm capable of generating UQS states for arbitrary $N$ . However, this method relied heavily on multi-controlled qubits, leading to an exponential growth in the number of CNOT gates when decomposing these multi-controlled operations for real quantum hardware. Recognizing the impracticality of this approach for Noisy Intermediate-Scale Quantum (NISQ) devices, we refined the algorithm to minimize the need for multi-controlled gates, resulting in a significant reduction in CNOT gate usage.

The optimized algorithm utilized $n = \lceil \log_{2} N \rceil$ qubits with a circuit depth of $O(\log_{2} N)$ , making it more efficient for implementation on available quantum hardware. As the main coder, I developed the quantum circuits and ran them on IBM’s quantum computers, allowing us to evaluate the practical impact of quantum noise. This hands-on experience highlighted the importance of error mitigation techniques, as we observed substantial deviations in outcomes when no such corrections were applied.

Beyond coding, I also contributed insights that helped shape our algorithm’s final design, leading to an efficient solution that minimized gate usage while maintaining accuracy. These improvements were key to our team securing 2nd place in the competition out 24 teams. This experience reinforced my understanding of the practical challenges in quantum computing, from algorithmic design to hardware execution, and deepened my passion for optimizing quantum hardware to tackle complex computational tasks—closely aligning with my broader research goals in AI and quantum systems.





**Solving Navier-Stokes with PINNs and Quantum Circuits:**





**2024 IonQ Mentoring Program:**







