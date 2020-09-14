---
layout: article
title: Computer System Analysis and Performance Evaluation
key: sys-perf-eval-notes
tags: System PerformanceEvaluation CourseNotes
---

计算机系统分析与性能评价课程笔记

<!-- more -->

学科意义与方法论
=============

__Objects 目标__

* Performance abstraction, representation & conprehensive analysis

    e.g. 人 = 德 + 智 + 体 + ...

* Optimally designing systems / selection

* Queuing theory, Petri nets & conbination of tests and simulations


__方法选择__

* Measurements

    given system (post-prototype), given workload

* Simulation modeling

    system / environment not given

* Analytical modeling

    揭示系统内在规律，指明工作理论性贡献，但须结合实际实验数据！

    probability, stochastic process, queuing systems, queuing networks,
    Petri nets, Markov-chain, etc.

    因负载/任务随机性，多采用随机过程与概率方法。


__Why?__

* Meet intended application
* Meet efficiency & reliability requirements
* To design / build / operate systems near its optimal level of processing
    power under given requirements


__Measures 度量__

* Response time _(definition varies)_
* Waiting time, processing time

    queuing vs. serving

* Utilization
* Throughput
* Missionability 可用性

    If system remain operational for entire duration of a mission.

    * Reliability

        Probability of system performing correctly throughout a mission.

* Dependability

    Reliability over long run.

    Number of failures / day, MTTF, MTTR, long-term availability

> __Reliability vs. Dependability__
>
> Reliability
> * Useful for system where failure is catastrophic
> * Focusing on short-term mission.
>
> Dependability
> * Useful for systems where repair is possible and failure is tolerable.
> * Focusing on long-term overall bahavior.


__Technique__

* Measurements

    1. Design experiment.
    2. Gather data of performance parameters (hardware / software / hybrid).
    3. Statistical analysis to draw meaningful concolusion.

* Simulation modeling

    1. Construct system behavior model.
    2. Drive the model with appropriate abstraction of workload.
    
    Involving experiment design, data gathering & analysis.

* Analytic modeling

    1. Construct mathematical model

        Queuing, Markov-chain, Petri, etc.

    2. Solve It!

__A Systematic Approach__

1. State goals and define system
2. List system services and outcomes
3. Select performance metrics
4. List parameters that affect performance
5. Select factors to study
6. Select evaluation technique
7. Select workload
8. Design experiment
9. Analyze and interpret data

__条件概率__

* 条件概率

    $$
    P(B|A) = \frac{P(AB)}{P(A)}
    $$

* 事件独立

    $$
    P(AB) = P(A) P(B)
    $$

设 $$\Omega = E_1 + \dots + E_n$$，则

* 全概率公式

    $$
    P(A) = \sum_i{P(A|E_i)P(E_i)}
    $$

* 贝叶斯公式（后验概率公式）

    $$
    P(E_i|A) = \frac{P(A|E_i)P(E_i)}{\sum_j{P(A|E_j)P(E_j)}}
    $$

    e.g. 线路传输问题，由以往数据传输统计数据，计算收到结果的可靠性。

__离散概率分布__

* 伯努利分布（0-1分布、两点分布）
* 二项分布

    $$
    P\{X=k\} = C_n^k p_k (1-p)^{n-k}, \quad 0 \leq k \leq n
    $$

* 几何分布（伯努利试验首次成功的试验次数）

    $$
    P\{X=m\} = p (1-p)^{m-1}, \quad m = 1, 2, \dots
    $$

* __泊松分布__

    $$
    P\{X=k\} = \frac{\lambda^k}{k!} e^{-\lambda}, \quad k=0,1,\dots
    $$

    期望与方差均为 $$\lambda$$。

* 正态分布
* Γ分布

泊松分布与泊松过程
--------------

__泊松事件流（泊松过程）__

* 平稳性

    事件发生概率与考虑的微小时间段 $$\Delta t$$ 成正比，但与起起始与终止位置无关

* 稀有性

    在微小时间段发生 2 次以上事件的概率 → 0

* 无后效性

    不同时间段的事件相互独立

* 微分性

    $$P\{X(t)=n\}$$ 关于 $$t$$ 可微

__泊松事件流与泊松分布的关系__

对于泊松事件流，在长为 $$t$$ 的时间间隔内事件出现的次数 $$v(t)$$ 服从参数为 $$\lambda t$$ 的泊松分布。

__泊松过程与指数分布关系__

泊松过程中观察任务到达时间间隔 $$T_a$$，则

$$
\begin{aligned}
P\{T_a < t\} &= 1 - P\{T_a \geq t\} = 1 - e^{-\lambda t } &\text{（t内多个任务到达）}\\
E(T_a) &= \frac{1}{\lambda}
\end{aligned}
$$


随机过程
------

__随机过程__

$$\{X(t), t \in \text{状态集（参数集、索引集）}\ T\}$$

* 离散参数（$$t$$）的随机过程：随机序列
* 离散状态（$$X(t)$$）的随机过程：链

__马尔可夫过程__

无后效性的随机过程

$$
P\{X(t) \leq x | X(t_n) = x_n, \dots, X(t_1)=x_1\}
= P\{X(t) \leq x | X(t_n)=x_n\}
$$

> 泊松过程为马尔可夫过程的特例。

-----------------------------------------------------------------

Measurement
===========

__Technique__

* Types of workloads
* Performance monitoring
* Summarizing measured data
* Experimental design