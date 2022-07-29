---
title: Reinforcement Learning and Artificial Intelligence
description: 暑期课程强化学习与人工智能笔记
categories: AI
tags:
  - RL
abfrlink: 48478
index_img: /post_img/81514130_p0_master1200.jpg
banner_img: /post_img/81514130_p0_master1200.jpg
abbrlink: 48478
header: ''
---
## Introduction

Reinforcement Learning (RL) is a **scientific theory** (or hypothesis) that seeks to provide a **computational explanation** to the widely **observed phenomenon** that some complex **physical system** can adapt to the **physical environment** around it.

- scientific theory: links an observation (i.e. the subject) to some other reproducible observations (i.e. the evidence) with logic.
- computational explanation
- observed phenomenon
- physical system
- physical environment

The Rl regard the physical world as a Markov chain. Consider a physical system that interacts with a surrounding environment by exchanging mass/energy across the system boundary. The **world (system + environment)** changes over time, and is in a certain state $\mathbf{s_t}$ at each moment $t$.

Different physical theories may formulate $\mathbf{s_t}$ into different mathematical objects ($s$ can be a vector, a tensor, a function, a function of functions, etc.). But in most physical theories, the time evolution of the state follows time-invariant
(possibly stochastic) transition laws, such that $\mathbf{s_t}$ decouples the past from the future.

> Theorem (H. M. Sheffer, in Transactions of the American Mathematical Society, 1913): Every digital computer is functionally equivalent to an NAND network.

## Math Basics

### Probability Theory Basics

> 详见概率论相关的文章，这里摘录一下课上的大纲

#### Probability Space

- Sample Space, a set of all “possible worlds” under concern, each with full certainty and definiteness.
- Event Space, a set of all random events; each event may occur in a subset of the possible worlds.
- Probability function, mapping that assigns a real number to each random event to indicate its “propensity of occurrence”.

#### Joint Probability, Union Probability, Union Bound

Union Bound:

$$
\begin{array}{c}
  P[{A_1}or{A_1}or{\dotsb}{ {A_n} }]{\le}\sum_{i=1}^{n}P[A_i]
\end{array}
$$

#### Conditional Probability, Independence

The conditional probability has been in a new probability space, so much different with joint probability.And to point it, use $P_B[A]$ is better than $P[A|B]$.

To change the probability space

$$
\begin{array}{c}
  P[AB]=P[A|B]P[B]=P[B|A]P[A]
\end{array}
$$

And if we want to add a probability of C

$$
\begin{array}{c}
  P[AB|C]=P[A|BC]P[BC], or this form\\
  P_C[AB]=P_C[AB]P_C[B].\\
\end{array}
$$

#### Random Variable

If $X$ is continuous, we will (ab-)use 𝐏[𝑋 = 𝑥] to refer (instead) to the probability density of $X = x$.

If 𝑋 is continuous, we will (ab-)use Σ𝑥 (instead of ∫ d𝑥) to refer to the probabilistic integration

#### Probability Distribution

A function 𝑷 is a probability distribution function if and only if (1) 𝑃 𝒙 ≥ 𝟎 and (2) σ𝒙 𝑃(𝒙) = �

#### Multivariate Variable, Categorical Variable

- Multivariate variable (random vector), a vector of random variables.
- Categorical variable, rand. var. whose values are “labels” (rather than “numbers”)
- One-hot vectors, numerical representation for categorical variables

#### Function of Random Variable

For an ordinary, definite, and deterministic function, its output becomes a random variable if the input of the function is a random variable.

𝐏 𝑓 𝑋 = 𝑦 = σ{𝑥: 𝑓 𝑥 =𝑦} 𝐏[𝑋 = 𝑥]

#### Expectation, Conditional Expectation and Function of Random Variable's Expectation

Expectation, also called expected value, or mean value, or simply the mean, is the probability-weighted average over all possible values of a random variable.

conditional expectation is conditioned on a random event, not on a random variable.

For a function, $P[f(X)=y]=\sum_{\{x:f(x)=y\} }P[X=x]$, and $E[f(X)]=\sum_{x}P[X=x]{\cdot}f(x)$

typically used as **distance unit** to measure how far a particular value of 𝑋 deviates from the mean 𝐄[𝑋]

#### Variance, Standard Deviation

The variance of 𝑋 is the probability-weighted average of the squared distances between possible values of 𝑋 and its mean

$$
\begin{array}{c}
  Var[X]=E[(X-E[X])^2], and conveniently\\
  Var[X]=E[X^2]=(E[X])^2
\end{array}{c}
$$

Standard deviation $\sigma(X)=\sqrt{Var[X]}$

#### Covariance and Correlation

The covariance between two random variables 𝑋 and 𝑌 measures the tendency that the values of 𝑋 and 𝑌 jointly deviate in the same way from their respective mean values.

$$

$$

Pearson correlation coefficient normalizes the deviations by dividing the standard deviations, so that we always have 0 ≤ 𝜌(𝑋, 𝑌) ≤ 1

For multivariate random variable 𝑿 = 𝑋1, 𝑋2, … ,𝑋𝑛 T, the covariance matrix of 𝑿consists of all the pairwise covariances between the elements in 𝑿

#### Entropy and Cross Entropy

The entropy of a random variable 𝑋 characterizes the inherent uncertainty of 𝑋, or equivalently, the “expected surprise” when observing a sample of 𝑋.

The uniform distribution is the maximum-entropy distribution among all probability distributions with the same support.

For two random variables 𝑋 and 𝑌 with the same support, the cross entropy of 𝒀relative to 𝑿 measures **how 𝑌’s distribution differs from 𝑋’s distribution**.

Cross entropy (or more accurately, 𝑯 𝒀 𝑿 − 𝑯(𝑿), called the KL-divergence) is usually used as a measure of the **distance between two distributions**

### Parametric Models in Statistics

#### Gaussian Model

Gaussian distribution is so widely observed that it’s been called, the normal

当样本数据 X 是一维数据（Univariate）时，高斯分布遵从下方概率密度函数（Probability Density Function）<sup>2</sup>：

$$
N(x;\mu,\sigma^2)={\frac{1}{\sigma \sqrt{2\pi} }}e^{ {-\frac{1}{2} }(\frac{x-\mu}{\sigma})^2}
$$

> A parametric model that well captures the probability distribution of not a single, but many random variables encountered in the real world.

**Gaussian distribution** has a single “peak” (called the mode of the distribution). For many random variables $Y$ in the real world, its marginal distribution $P(y)$ is **multi-modal**.

Sometimes such $P(y)$ can be decomposed into a mixture of unimodal distributions.

$$
P(y)=\sum_{x}P(x)P(y|x)
$$

where $X$ is another observable random variable.

we can fit the conditional distribution $P(y|x)$ , with a separate Gaussian function, for each $x$

$$
f(y;\mathbf{\theta})=\sum_{x}P(x)N(y;\mu_x,\sigma_x^2), \\
where {\quad}\mathbf{\theta}=({\mu_1},{\mu_2},\dotsb,{\mu_n},{\sigma_1},{\sigma_2},\dotsb,{\sigma_n})
$$

**Gaussian Mixture Model, GMM** method seeks to estimate $\mathbf{\theta}$ for the mixture distribution $f$ without observing $X$.

高斯混合模型可以看作是由 K 个单高斯模型组合而成的模型，这 K 个子模型是混合模型的隐变量（Hidden variable）。一般来说，一个混合模型可以使用任何概率分布，这里使用高斯混合模型是因为高斯分布具备很好的数学性质以及良好的计算性能<sup>2</sup>。

We can further factorize $X$ into a mixture distribution, depending on some $Z$, and so on, eventually leading to a **Probabilistic Graphical Model** (called **Bayesian Network**)

#### Gaussian Linear Model[^1]

When $X$ has infinite support, we can’t parameterize $f$ with a finite number of $\mu x$ and $\sigma x$.

In this case, we can make $\mu$ (and $\sigma$) a function of $x$, and parameterize $f$ through parameterizing the functions $\mu(x)$ and $\sigma(x)$

Gaussian Linear Models (or Linear Gaussian Models) are parametric models that seek to fit the **conditional probabilities** $P[Y=y|X=x]$, where both $X$ and $Y$ are observablerandom variables, with a Gaussian function with linear mean:

$$
f(y|x;a,b,\sigma)=N(y;ax+b,\sigma)={\frac{1}{\sigma{\sqrt{2\pi} }} }e^{ {-\frac{1}{2} }{(\frac{y-(ax+b)}{\sigma})}^2}
$$

With separately learned distribution $P(x)$, the Gaussian Linear function $f(y|x;a,b,\sigma)$can model more complex marginal distribution of $Y$ (than a single Gaussian function can), $P[Y=y]=\sigma_x{P(x)f(y|x;a,b,\sigma)}$.

Often, we just care about the conditional probability for its own sake (e.g. in policy learning), $P[Y=y|X=x]=f(y|x;a,b,\sigma)$.

#### Maximum Likelihood Estimation, MLE

对于单高斯模型，我们可以用最大似然法估算参数 $\mathbf{\theta}$的值[^2]

$$
\prod^{n}_{i=1}{\mathbf{P_{\theta} }}[{Y_i}={y_i}|{X_i}={x_i}]=\prod^{n}_{i=1}f({x_i,y_i;\mathbf{\theta} })
$$

The MLE principle proposes to choose the parameter vector $\mathbf{\theta}$ that maximizes the function, which is equivalent to minimize the **negative-log-likelihood (NLL) function**:

$$
-\log{\prod^{n}_{i=1}f({x_i,y_i;\mathbf{\theta} })}=-{\sum_i}\log f({x_i,y_i;a,b,\sigma})={\frac{1}{2\sigma^2} }{({\sum_i}(a{x_i}+b-{y_i})^2)}+n\log{\sigma{\sqrt{2\pi} }}
$$

#### Gaussian Linear Model with Multivariate

Multivariate Gaussian Linear Model is a parametric model that seeks to fit the conditional distribution $Y=y|\mathbf{X}=\mathbf{x}$, where $\mathbf{X}$ is an observable **multivariate random variable**, such that

$$
f(y|\mathbf{x};\mathbf{w},\sigma)=N(y;{\mathbf{w}\cdot\mathbf{x} },\sigma)={\frac{1}{\sigma{\sqrt{2\pi} }} }e^{ {-\frac{1}{2} }{(\frac{y-{\mathbf{w}\cdot\mathbf{x} }}{\sigma})}^2}
$$

#### Gasussian Linear Regression and Mean Squared Error, MSE

The Gaussian linear function can be alternatively viewed as a parametric model for a “perturbed mapping” from a vector variable 𝒙 to a scalar variable 𝑦, where the perturbation is a Gaussian noise $\epsilon ~ N(0,\sigma^2)$

Given observations and the parameter vector as the linear coefficients, can be equivalently chosen based on the **Mean Squared Error (MSE) principle**, without the explicit probabilistic interpretation

$$
{L_{MSE} }={\frac{1}{n} }\sum_i{(\mathbf{w\cdot x}-{y_i})^2}
$$

#### Logistic Regression

深度学习的实践说明，线性回归总是存在他的局限性。

Generalized linear model in the form of

$$
g(\mathbb{}{x};\mathbb{w})=\phi(\mathbf{w}\cdot \mathbf{x}), {\quad}\phi(s)=\frac{1}{1+e^{-s} }
$$

or other function with the similar S-shape curve

#### Deep Logistic Networks

## Elements in Reinforcement Learning

**RL is a Cross-disciplinary nature.**

![image-20220705010806726](https://tva1.sinaimg.cn/large/e6c9d24ely1h3ve5vqbuoj20xa0u0q5v.jpg)

### Origin of RL

Reinforcement: The observation that under some conditions, some stimulus has the effect that it can increase the likelihood of the action preceding it, with a reproducible pattern.

Behavioral psychology research not only gave birth to the name of RL, but more importantly, provides abundant experimental data for the RL theory to explain.

### The Policy

Policy is changing during learning.

When a system learns, the mapping rule between its inputs (=observations) and outputs (=actions) must be changing.

![image-20220705011701586](https://tva1.sinaimg.cn/large/e6c9d24ely1h3vef3efh3j20na0b03yy.jpg)

The mapping rule is called **a decision policy function**, or just **policy** for short.

- Deterministic policy: $\mathbf{a_t}=\pi(\mathbf{x_t})$
- Stochastic policy: $P[{A_t}=\mathbf{a_t}|{X_t}=\mathbf{x_t}]=\pi(\mathbf{x_t},\mathbf{a_t})$,so that ${A_t}~\pi({x_t},\cdot)$

#### Parameterization

For any system to learn anything, its policy $\pi$ must be able to change flexibly

With a parameter $\theta$, we get

- Deterministic policy: $\mathbf{a_t}=\pi(\mathbf{x_t},\theta)$
- Stochastic policy: $P[{A_t}=\mathbf{a_t}|{X_t}=\mathbf{x_t}]=\pi(\mathbf{x_t},\mathbf{a_t},\theta)$

To change the model $\pi$, we only need to change its parameter $\theta$.

For flexible learning, we want the model to cover a large enough set of possible policy functions. For example, a linear model is impossible to learn effectively if the optimal policy is $a=x^2$.

#### Trial and Error

Trial and Error is family of optimization methods that can optimize an objective function $J$ without explicit knowledge (e.g. the closed form) about $J$.

The trial-and-error process results in a trace of policies with improving performance

### Related models(preview)

About parameterization:

- Regression models in statistics
- Parameterization in biological neuronal networks
- Artificial neural networks
- From Genotype to Biological Fitness

About trial and error:

- Evolution as a special form of trial-and-error learning
- Evolutionary algorithms in AI
- Policy Gradient Method, Stochastic Gradient Descent (SGD)
- Bandit Algorithms, Upper Confidence Bound (UCB) Algorithm
- Q-Learning
- Monte-Carlo Tree Search
- Correspondence in Cognitive Neuroscience
- Deep Reinforcement Learning

## Biological Neural Nwtwork

Brain consists of two types of cells: glial cells and neurons.

![image-20220706152706244](https://tva1.sinaimg.cn/large/e6c9d24ely1h3x8m229o2j218e0u0gr7.jpg)

![image-20220706152905711](https://tva1.sinaimg.cn/large/e6c9d24ely1h3x8nz6x74j21aa0fktbd.jpg)

### Integrate-and-fire Model

**Action potential** in pre-synaptic neuron induces **response current** in post-synaptic neuron.Resoonse current decays over time.

$$
{I_{response}({\Delta t})}={\frac{w_i}{\tau_s} }e^{-{\Delta t}/{\tau_s} }
$$

> Response currents from all synapses integrate through the dendrite of the post-synaptic neuron, accumulating potential imbalance in the membrane of the cell, until **reaching a threshold** at which point a post-synaptic action potential is released (which resets the membrane potential)

Firing-rate model is a statistical model of biological neural networks, which assumes that functionality of a biological neural network mostly depends on **frequency patterns of the action potentials** flowing in the network, whose precise timing patterns do not matter.

The firing rate of a neuron is a **function of time $t$** which gives the **frequency density of action potentials** that the neuron would probabilistically release at each time point $t$.

$$
{x(t)}=\lim_{ {\Delta t}\rightarrow 0}\mathbf{E}[\frac{ {spikes{\ }in}[t-{\Delta t},t]}{\Delta t}]
$$

Firing-rate $x_i(\cdot)$ of pre-synaptic neuron $i$ induces a response current $I_i(\cdot)$ at post synaptic neuron. Response currents from all synapses integrate into a total synaptic current $I(\cdot)$ which induces the firing-rate $y(\cdot)$ of the post-synaptic neuron.

Step by step,

1. Response current induced by a single action potential: ${I_{response}(\Delta t)}={\frac{w_i}{\tau_s} }e^{-{\Delta t}/{\tau_s} }$
2. Response current induced by all spikes of synapse $i$: ${I_i(t)}={\int_{-\infty}^{t} }{I_{response}(t-\tau){s_i(\tau)d\tau} }$
3. Total synaptic current induced by all spikes of all synapses: $I(t)=\sum_i{T_i(t)}$

Finally, firing rates $\mathbf{x}$ of all the pre-synaptic neurons collectively induce total synaptic current $I$ at the post-synaptic neuron:

$$
{\tau_s}{\frac{\mathrm{d}I}{\mathrm{d}t} }=-I\,+\,\mathbf{w}\cdot\mathbf{x}
$$

Total synaptic current $I$ determines the firing rate $y$ of the post-synaptic neuron

$$
{\tau_r}{\frac{\mathrm{d}y}{\mathrm{d}t} }=-y+\phi(I)
$$

where $\phi(\cdot)$ is called the **activation function** of the (post-synaptic) neuron.

### Activity-independent Synaptic Plasticity and Hebbian Rule

**Plasticity** is the ability of a solid material to undergo permanent deformation, a persistent change of shape in response to applied forces.

Changes of a synapse’s strength $w$ that persist for tens of minutes or longer are generally called long-term potentiation (LTP) and long-term depression (LTD). Activity-dependent long-term synaptic plasticity is widely believed to be the biological foundation underlying the phenomenon of learning and memory.

The **Hebbian theory** is the best-known model for activity-dependent long-term synaptic plasticity. The **Hebbian rule** states that synapses change in proportion to the covariance between activities of the pre- and post-synaptic neurons.

赫布理论（英語：Hebbian theory）是一个神经科学理论，解释了在学习的过程中脑中的神经元所发生的变化。赫布理论描述了突触可塑性的基本原理，即突触前神经元向突触后神经元的持续重复的刺激，可以导致突触传递效能的增加。这一理论由唐纳德·赫布于1949年提出，又被称为赫布定律（Hebb's rule）、赫布假说（Hebb's postulate）、细胞结集理论（cell assembly theory）等[^3]。

“当神经元 A 的一个轴突和神经元 B 很近，足以 对它产生影响，并且持续地、重复地参与了对神经元 B 的兴奋，那么在这两个神 经元或其中之一会发生某种生长过程或新陈代谢变化，以致神经元 A 作为能使 神经元B兴奋的细胞之一，它的效能加强了．”这个机制称为赫布理论（Hebbian Theory）或赫布规则（Hebbian Rule，或 Hebb’s Rule）．如果两个神经元总是相 关联地受到刺激，它们之间的突触强度增加．这样的学习方法被称为赫布型学习 （Hebbian learning）．Hebb认为人脑有两种记忆：长期记忆和短期记忆．短期记 忆持续时间不超过一分钟．如果一个经验重复足够的次数，此经验就可储存在长 期记忆中．短期记忆转化为长期记忆的过程就称为凝固作用．人脑中的海马区为 大脑结构凝固作用的核心区域[^4]

- Let real number $w$ denote the **strength of an excitatory synapse**, $x(t)$ and $y(t)$ the pre- and post-synaptic firing rates at time $t$,

$$
{\tau_w}{\frac{\mathrm{d}w}{\mathrm{d}t} }=x(t){\,}y(t)
$$

- Let **random variable** $X$ and $Y$ be the pre- and post-synaptic firing rates at a random time $\tau$ in a time window $[t-{\Delta t},t]$,

$$
{\tau_w}{\frac{\mathrm{d}w}{\mathrm{d}t} }=\mathbf{E}[XY]-{\mathbf{E}[X]}{\mathbf{E}[Y]}
$$

## Artificial Neural Networks, ANN

> ANN在统计领域由于难以证明，近几年虽然在动力系统、抽象代数的方向上有研究，但可解释性还是比较差；生物科学方面，过于复杂的脑神经系统仍然难以模仿，不过话说回来，全脑模拟也确实是一个研究方向；最后，AI领域曾在早期被提出，但由于过于庞大被搁置了数十年

Parameterization in AI:

- Neural-network models
- Tabular models
- Non-differentiable models

### Multi-Layer Perceptron, MLP

![image-20220707142039567](https://tva1.sinaimg.cn/large/e6c9d24ely1h3ycb4jbvej20si0jcn08.jpg)

Each hidden-layer and ouput-layer node $i$ repoesents a sub-mode $g(\mathbf{x};\mathbf{w_i},b_i)=\phi({\mathbf{w_i}\cdot{\mathbf{x} }+{b_i} })$. If define $\mathbf{\bar{x} }=(\mathbf{x},1)^T,{\;}\bar{\mathbf{w_i} }=(\mathbf{w_i},{b_i})$

### Activitation Functions

- Sigmoid, it can seperate when the **input is too large**:
$$
\sigma(x)=\frac{1}{1+e^{-x} }
$$

- tanh: $\tanh(x)$
- ReLU: $max(0,x)$
- Leaky
- ReLU
- Maxout
- ELU

一个MLP模型的需要的参数是非常多的，以一个输入$\mathbb{R}^5$，有两个$\mathbb{R}^7$隐藏层并输出$\mathbb{R}^4$的网络来讲，他需要的参数是

$$
n=[(N_{input}+1)\cdot{N_{next} }]+[(N_{hidden1}+1)\cdot{N_{next} }]+[(N_{hidden2}+1)\cdot{N_{output} }]=170
$$

A **decision policy** determines the probability that an “intelligent” system would output a particular “action” in a time step conditioned on aparticular “state” of the system.

A policy function 𝜋 is a conditional probability distribution. As a probability distribution, any policy function has to satisfy the following constraints

![image-20220707144028629](https://tva1.sinaimg.cn/large/e6c9d24ely1h3ycvp1fuaj20wu0fuad9.jpg)

For a discrete output, define **softmax function** and add it to the output layer

$$
\sigma:\mathbb{R}^K{\rightarrow}[0,1]^K,{\;}where{\;}\sigma_i(z)={\frac{e^{z_i} }{\sum_{j=1}^K}{e^{z_j} }},{\,} for{\,} i=1,\dotsb,K
$$

> 由于指数的增长速率很大，这个函数可以“柔软”的放大输出之间的差异，并共同成为一个概率分布函数。</br>
> Softmax function是为了将输出转换为一个条件概率，而不是获得一个最大值。

Then $\pi(\mathbf{s},\mathbf{a};\mathbf{\theta})=\sigma(f_{MLP}(\mathbf{s};\mathbf{\theta}))\cdot\mathbf{a}$

其中$\mathbf{a}$是一组one-hot vector。

![image-20220707144606874](https://tva1.sinaimg.cn/large/e6c9d24ely1h3yd81y6lyj21400fgq6i.jpg)

### Example: Locomotion Control

### Domain-specific NN architecture

#### Convolutional Network

![image-20220707153056204](https://tva1.sinaimg.cn/large/e6c9d24ely1h3yec7ew8rj214u0q6tc2.jpg)

#### Transformer Network

![image-20220707154021201](https://tva1.sinaimg.cn/large/e6c9d24ely1h3yem057wej21z60magpd.jpg)

#### Graph Network

![image-20220707154326848](https://tva1.sinaimg.cn/large/e6c9d24ely1h3yep7une0j210g0jmwfq.jpg)

## Tabular Model and Non-differential Model

A tabular model is a parametric model that covers the entire policy space.

## Biological Evolution

## HomeWorkds

### homework-1.a

## References

[^1]: [机器学习——线性高斯模型](https://www.cnblogs.com/young978/p/15813842.html)
[^2]: [高斯混合模型（GMM） - 戴文亮的文章 - 知乎](https://zhuanlan.zhihu.com/p/30483076)
[^3]: [赫布理论 - 维基百科](https://zh.m.wikipedia.org/zh/赫布理论)
[^4]: [机器学习简介](https://blog.csdn.net/qq_40808154/article/details/115407544)
