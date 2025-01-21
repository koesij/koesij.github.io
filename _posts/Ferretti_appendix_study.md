Equation of motions
$$
\frac{d\boldsymbol{r}_i}{dt}=\boldsymbol{v}_i
\\
\frac{d\boldsymbol{v}_i}{dt}=-\frac{\partial \mathcal{H}}{\partial \boldsymbol{v}_i}+\boldsymbol{\xi}_i=-J\sum_{j}n_{ij}(t)(\boldsymbol{v}_i-\boldsymbol{v}_j)-g(\vert \boldsymbol{v}_i\vert-v_0)\frac{\boldsymbol{v}_i}{\vert \boldsymbol{v}_i \vert}+\boldsymbol{h}+\boldsymbol{\xi}_i
\\
\boldsymbol{F}_i=-\frac{\partial \mathcal{H}}{\partial \boldsymbol{v}_i}
\\
=-J\sum_{j}n_{ij}(t)(\boldsymbol{v}_i-\boldsymbol{v}_j)-g(\vert \boldsymbol{v}_i\vert-v_0)\frac{\boldsymbol{v}_i}{\vert \boldsymbol{v}_i \vert}+\boldsymbol{h}
$$


Onsager-Machlup action


$$
S[\boldsymbol{v}(t), \boldsymbol{r}(t)|\boldsymbol{v}(0),\boldsymbol{r}(0)]=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'(\dot{v}^{\alpha}_{i}(t')-F^{\alpha}_{i}(t'))^2
\\
=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'\bigg{[}\frac{d{v}^{\alpha}_{i}(t')}{dt'}+J\sum_{j}n_{ij}(t')({v}^{\alpha}_i-{v}^{\alpha}_j)+g(\vert \boldsymbol{v}_i\vert-v_0)\frac{{v}^{\alpha}_i}{\vert \boldsymbol{v}_i \vert}-{h}^{\alpha}\bigg{]}^2
\\
$$

$$
S[\boldsymbol{v}^{\dagger}(t), \boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)]
=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'\{-\frac{d{v}^{\alpha}_{i}(t-t')}{dt'}+F^{\alpha}_{i}(t-t')\}^2
\\
=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'\bigg{[}-\frac{d{v}^{\alpha}_{i}(t-t')}{dt'}+J\sum_{j}n_{ij}(t-t')\{-{v}^{\alpha}_i(t-t')+{v}^{\alpha}_j(t-t')\}
\\
+g\{{\vert -\boldsymbol{v}_i(t-t')\vert-v_0}\}\frac{-{v}^{\alpha}_i(t-t')}{\vert -\boldsymbol{v}_i(t-t') \vert}-{h}^{\alpha}(t-t')\bigg{]}^2
\\
\\
\text{Let's apply change of variables}
\\
\tau=t-t' \rightarrow d\tau=-dt'
\\
S[\boldsymbol{v}^{\dagger}(t), \boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)] = \frac{1}{4T} \sum_{i, \alpha} \int_0^t d\tau \left[ -\frac{d v_i^{\alpha}(\tau)}{d\tau} + J \sum_{j} n_{ij}(\tau) \{ v^{\alpha}_i(\tau) - v^{\alpha}_j(\tau) \} 
+ g \{ \vert \boldsymbol{v}_i(\tau) \vert - v_0 \} \frac{v^{\alpha}_i(\tau)}{\vert \boldsymbol{v}_i(\tau) \vert} + {h}^{\alpha}(\tau) \right]^2
$$

$$
S[\boldsymbol{v}^{\dagger}(t), \boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)]-S[\boldsymbol{v}(t), \boldsymbol{r}(t)|\boldsymbol{v}(0),\boldsymbol{r}(0)]
\\
=\frac{1}{4T} \sum_{i, \alpha} \int_0^t dt' \bigg{[} -\frac{d v_i^{\alpha}(t')}{dt'} + J \sum_{j} n_{ij} (v^{\alpha}_i - v^{\alpha}_j) + g(\vert \boldsymbol{v}_i \vert - v_0) \frac{v^{\alpha}_i}{\vert \boldsymbol{v}_i \vert} + {h}^{\alpha} \bigg{]}^2
\\
-\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'\bigg{[}\frac{d{v}^{\alpha}_{i}(t')}{dt'}+J\sum_{j}n_{ij}({v}^{\alpha}_i-{v}^{\alpha}_j)+g(\vert \boldsymbol{v}_i\vert-v_0)\frac{{v}^{\alpha}_i}{\vert \boldsymbol{v}_i \vert}-{h}^{\alpha}\bigg{]}^2
\\
\\
=\frac{1}{4T}\sum_{i, \alpha} \int_0^t {dt'} \bigg{[}-2\frac{d{v}^{\alpha}_{i}(t')}{dt'}\bigg{(}J \sum_{j} n_{ij} (v^{\alpha}_i - v^{\alpha}_j) + g(\vert \boldsymbol{v}_i \vert - v_0) \frac{v^{\alpha}_i}{\vert \boldsymbol{v}_i \vert} + {h}^{\alpha}\bigg{)} 
\\
+\bigg{(}J \sum_{j} n_{ij} (v^{\alpha}_i - v^{\alpha}_j) + g(\vert \boldsymbol{v}_i \vert - v_0) \frac{v^{\alpha}_i}{\vert \boldsymbol{v}_i \vert} + {h}^{\alpha}\bigg{)}^2
\\
- 2\frac{d{v}^{\alpha}_{i}(t')}{dt'}\bigg{(}J \sum_{j} n_{ij} (v^{\alpha}_i - v^{\alpha}_j) + g(\vert \boldsymbol{v}_i \vert - v_0) \frac{v^{\alpha}_i}{\vert \boldsymbol{v}_i \vert} - {h}^{\alpha}\bigg{)} 
\\
- \bigg{(}J \sum_{j} n_{ij} (v^{\alpha}_i - v^{\alpha}_j) + g(\vert \boldsymbol{v}_i \vert - v_0) \frac{v^{\alpha}_i}{\vert \boldsymbol{v}_i \vert} - {h}^{\alpha}\bigg{)}^2   \bigg{]}
\\
\\
=\frac{1}{4T}\sum_{i, \alpha} \int_0^t {dt'}\bigg{[}- 4\frac{d{v}^{\alpha}_{i}(t')}{dt'} \bigg{(}J \sum_{j} n_{ij} (v^{\alpha}_i - v^{\alpha}_j) + g(\vert \boldsymbol{v}_i \vert - v_0) \frac{v^{\alpha}_i}{\vert \boldsymbol{v}_i \vert}\bigg{)}+2h^{\alpha}\bigg{(}J \sum_{j} n_{ij} (v^{\alpha}_i - v^{\alpha}_j) + g(\vert \boldsymbol{v}_i \vert - v_0) \frac{v^{\alpha}_i}{\vert \boldsymbol{v}_i \vert} \bigg{)}      \bigg{]}
\\
=\frac{1}{4T}\sum_{i, \alpha} \int_0^t {dt'}\bigg{[}\bigg{(}4\frac{d{v}^{\alpha}_{i}(t')}{dt'}-2h\bigg{)} \bigg{(}-J \sum_{j} n_{ij} (v^{\alpha}_i - v^{\alpha}_j) - g(\vert \boldsymbol{v}_i \vert - v_0) \frac{v^{\alpha}_i}{\vert \boldsymbol{v}_i \vert}\bigg{)}     \bigg{]}
$$


Following APPENDIX C
$$
S[\boldsymbol{v}(t), \boldsymbol{r}(t)|\boldsymbol{v}(0),\boldsymbol{r}(0)]=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'(\dot{v}^{\alpha}_{i}(t')-F^{\alpha}_{i}(t'))^2
\\
=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'\{\dot{v}^{\alpha}_{i}(t')+J\sum_{j}n_{ij}(t')(\boldsymbol{v}_i-\boldsymbol{v}_j)+g(\vert \boldsymbol{v}_i\vert-v_0)\frac{\boldsymbol{v}_i}{\vert \boldsymbol{v}_i \vert}-\boldsymbol{h}\}^2
\\
$$

$$
S[\boldsymbol{v}^{\dagger}(t), \boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)]
=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'\{-\frac{d{v}^{\alpha}_{i}(t-t')}{dt'}+F^{\alpha}_{i}(t-t')\}^2
\\
=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'\{-\frac{d{v}^{\alpha}_{i}(t-t')}{dt'}+F^{\alpha}_{i}(t-t')\}^2
\\
\text{From here, let's define a new variable,}
\\
\tau=t-t', \ d\tau=-dt' \text{ or } dt'= -d\tau
\\
S[\boldsymbol{v}^{\dagger}(t), \boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)]
=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}d\tau\{\frac{d{v}^{\alpha}_{i}(\tau)}{d\tau}+F^{\alpha}_{i}(\tau)\}^2
\\
$$




Entropy production


$$
\log{\frac{P[\boldsymbol{v}(t),\boldsymbol{r}(t)]}{P[\boldsymbol{v}^{\dagger}(t),\boldsymbol{r}^{\dagger}(t)]}}=\log{\frac{P[\boldsymbol{v}(t),\boldsymbol{r}(t)|\boldsymbol{v}(0),\boldsymbol{r}(0)]P_{0}(\boldsymbol{v}(0),\boldsymbol{r}(0))}{P[\boldsymbol{v}^{\dagger}(t),\boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)]P_{0}(\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0))}}
\\
=\log{\frac{P[\boldsymbol{v}(t),\boldsymbol{r}(t)|\boldsymbol{v}(0),\boldsymbol{r}(0)]}{P[\boldsymbol{v}^{\dagger}(t),\boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)]}}+\log{\frac{P_{0}(\boldsymbol{v}(0),\boldsymbol{r}(0))}{P_{0}(\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0))}}
$$



$$
=S[\boldsymbol{v}^{\dagger}(t), \boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)]-S[\boldsymbol{v}(t), \boldsymbol{r}(t)|\boldsymbol{v}(0),\boldsymbol{r}(0)]+\log{\frac{P_{0}(\boldsymbol{v}(0),\boldsymbol{r}(0))}{P_{0}(\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0))}}
$$

$$
S[\boldsymbol{v}^{\dagger}(t), \boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)]-S[\boldsymbol{v}(t), \boldsymbol{r}(t)|\boldsymbol{v}(0),\boldsymbol{r}(0)]=\frac{1}{4T}\sum_{i}\sum_{\alpha}\int^{t}_{0}dt\bigg{[}\bigg{(}\frac{dv_{i}^{\alpha}}{dt}+F^{\alpha}_{i}{}\bigg{)}^2-\bigg{(}\frac{dv_{i}^{\alpha}}{dt}-F^{\alpha}_{i}{}\bigg{)}^2\bigg{]}
\\
=\frac{1}{T}\sum_{i}\sum_{\alpha}\int^{t}_{0}dt\frac{dv^{\alpha}_{i}}{dt}\circ F^{\alpha}_{i}
$$

$$
\bigg{[}\bigg{(}\frac{dv_{i}^{\alpha}}{dt}+F^{\alpha}_{i}{}\bigg{)}^2-\bigg{(}\frac{dv_{i}^{\alpha}}{dt}-F^{\alpha}_{i}{}\bigg{)}^2\bigg{]}

=\bigg{(}2\frac{dv^{\alpha}_{i}}{dt}F^{\alpha}_{i}\bigg{)}
$$






Peusdo Hamiltonian
$$
\mathcal{H}=\frac{J}{2}\sum_{ij}n_{ij}(\boldsymbol{v}_i-\boldsymbol{v}_j)^2+\frac{g}{2}\sum_{i}(\vert\boldsymbol{v}_i\vert-v_0)^2-\sum_{i}\boldsymbol{h}_i\cdot\boldsymbol{v}_i
$$


equation of motions
$$
\frac{d\boldsymbol{r}_i}{dt}=\boldsymbol{v}_i
\\
\frac{d\boldsymbol{v}_i}{dt}=-\frac{\partial \mathcal{H}}{\partial \boldsymbol{v}_i}+\boldsymbol{\xi}_i=-J\sum_{j}n_{ij}(t)(\boldsymbol{v}_i-\boldsymbol{v}_j)-g(\vert \boldsymbol{v}_i\vert-v_0)\frac{\boldsymbol{v}_i}{\vert \boldsymbol{v}_i \vert}+\boldsymbol{h}+\boldsymbol{\xi}_i
\\
\boldsymbol{F}_i=-\frac{\partial \mathcal{H}}{\partial \boldsymbol{v}_i}
\\
$$


Calculus
$$
\boldsymbol{v} = (v_1, v_2, \dots, v_n)
\\
|\boldsymbol{v}| = \sqrt{v_1^2 + v_2^2 + \dots + v_n^2} = \sqrt{\boldsymbol{v} \cdot \boldsymbol{v}}
\\
\frac{\partial |\boldsymbol{v}|}{\partial \boldsymbol{v}} = \frac{\partial}{\partial \boldsymbol{v}} \sqrt{\boldsymbol{v} \cdot \boldsymbol{v}}
\\
\frac{\partial |\boldsymbol{v}|}{\partial \boldsymbol{v}} = \frac{1}{2} \frac{1}{\sqrt{\boldsymbol{v} \cdot \boldsymbol{v}}} \cdot \frac{\partial}{\partial \boldsymbol{v}} (\boldsymbol{v} \cdot \boldsymbol{v})
\\
\frac{\partial}{\partial \boldsymbol{v}} (\boldsymbol{v} \cdot \boldsymbol{v}) = 2\boldsymbol{v}
\\
\frac{\partial |\boldsymbol{v}|}{\partial \boldsymbol{v}} = \frac{1}{2 |\boldsymbol{v}|} \cdot 2\boldsymbol{v} = \frac{\boldsymbol{v}}{|\boldsymbol{v}|}
$$

$$
\frac{\partial (\boldsymbol{h} \cdot \boldsymbol{v})}{\partial \boldsymbol{v}}
\\
\boldsymbol{h} \cdot \boldsymbol{v} = \sum_{i} h_i v_i
\\
\frac{\partial (\boldsymbol{h} \cdot \boldsymbol{v})}{\partial \boldsymbol{v}} = \frac{\partial}{\partial \boldsymbol{v}} \sum_{i} h_i v_i
\\
\frac{\partial (\boldsymbol{h} \cdot \boldsymbol{v})}{\partial \boldsymbol{v}} = \sum_{i} h_i \frac{\partial v_i}{\partial \boldsymbol{v}} = \sum_{i} h_i \boldsymbol{e}_i
\\
\frac{\partial (\boldsymbol{h} \cdot \boldsymbol{v})}{\partial \boldsymbol{v}} = \boldsymbol{h}
$$

$$
S[\boldsymbol{v}^{\dagger}(t), \boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)]
=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'\{-\frac{d{v}^{\alpha}_{i}(t-t')}{dt'}+F^{\alpha}_{i}(t-t')\}^2
\\
=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}dt'\{-\frac{d{v}^{\alpha}_{i}(t-t')}{dt'}+F^{\alpha}_{i}(t-t')\}^2
\\
\text{From here, let's define a new variable,}
\\
\tau=t-t', \ d\tau=-dt' \text{ or } dt'= -d\tau
\\
S[\boldsymbol{v}^{\dagger}(t), \boldsymbol{r}^{\dagger}(t)|\boldsymbol{v}^{\dagger}(0),\boldsymbol{r}^{\dagger}(0)]
=\frac{1}{4T}\sum_{i, \alpha}\int^{t}_{0}d\tau\{\frac{d{v}^{\alpha}_{i}(\tau)}{d\tau}+F^{\alpha}_{i}(\tau)\}^2
\\
$$
