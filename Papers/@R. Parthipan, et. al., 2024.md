---
title: Defining error accumulation in ML atmospheric simulators
site: https://arxiv.org/abs/2405.14714
summary: 딥러닝 대기 모델에서 에러는 무엇인가 정의함. 학습에 쓰면 개선도 됨.
keyword:
  - KL divergence
  - error accumulation
status:
  - ==Done==
aliases: 
tags:
  - paper
when_published: 2024-05-23
where_published:
  - arXiv
---
```ad-summary
내가 만든 metric 쓰면 잘 된다! 이걸로 학습시켜도 잘 된다! 
```

```ad-abstract
Machine learning (ML) has recently shown significant promise in modelling atmospheric systems, such as the weather. Many of these ML models are autoregressive, and error accumulation in their forecasts is a key problem. However, there is no clear definition of what `error accumulation' actually entails. In this paper,<span style="background:rgba(0, 230, 118, 0.55)"> we propose a definition and an associated metric to measure it</span>. Our definition distinguishes between errors which are due to model deficiencies, which we may hope to fix, and those due to the intrinsic properties of atmospheric systems (chaos, unobserved variables), which are not fixable. We illustrate the usefulness of this definition by proposing a simple regularization loss penalty inspired by it. This approach shows performance improvements (according to RMSE and spread/skill) in a selection of atmospheric systems, including the real-world weather prediction task.
```

# 1. Introduction
Error accumulation은 잘 알려진 modelling dynamical systems problem
하지만 그게 정확히 뭔지 def.가 없어...
$\to$ 일반적으로 RMSE, skill/spread, [[continuous ranked probability score, CRPS|CRPS]] 적당히 섞어 평가하더라.

우리는 Error를 2가지로 나누어 평가한다
1. ML model deficiencies로 인한 
   $\to$ we hope to fix
2. Intrinsic properties of atmospheric systems로 인한 (chaotic & unobserved variables)
   $\to$ not hope to remedy
   
> Our metric assess this by <font color="#00e676">evaluating model performance</font> against <font color="#00e676">a reference model </font>that is immune to errors from iterative rollouts. 

---
# 7. Discussion

---
# 2. background
## Defining error accumulation in dynamical systems
> ~ all mention error accumulation, typically describing it informally as <font color="#00e676">a progressive increase in forecast errors with each iteration of an autoregressive forecast.</font>

다른 방식으로는 'stability criterion'도 있다

## Addressing error accumulation
exposure bias
:= autoregressive model의 past state 사용 시점과 simulation에서 model-generated state 사용하는 시점의 mismatch
$\to$ language하는 사람들이 해결하려고 도전; Scheduled Sampling
$\to$ MLWP에 adapted

Note) "For models based on techniques such as diffusion, it is not clear how rollout training would be used."

poor performance는 lack of model generalization이고, rollout training은 form of regularization through data augmentation이다. 
e.g. Gaussian noise 더한 / high-resolution을 truth로 잡고 ML을 돌려 / etc...

---
# 3. Problem Formulation: capturing error accumulation
CTS: continuous forecasting model
## Capturing explosive forms
= (ENS mean이 indefinitely grow할 때) + (ENS mean이 stable할 때)
$$X_{k, t+1} = X_{k,t} + Z_{k,t} \quad (Z_{k,t} \sim N(0,1) )$$
**Metric 1) RMSE**: bad
$\because$ generative model의 mean은 truth에 붙어서 각각이 explode한 걸 잡아내지 못 함

**Metric 2) spread/skill**: better
시간에 따라 증가 $\to$ reflecting the diverging trajectories

**Metric 3) own metric**: evident

## Capturing non-explosive forms
CTS는 했는데 generative model은 못 했다? $\to$ $\because$ model deficiency
**Metric 1) RMSE**: low
값이 너무 작아서 못 잡았다? (왜 작다고 판단했는지는...)

**Metric 2) spread/skill**: better
1보다 작은 값 $\to$ spread가 덜 되었거나 skill이 너무 잘 되었거나.

**Metric 3) own metric**: evident

## Not capturing errors due to STIC
STIC: Sensitivity To Initial Conditions
STIC가 model state가 widely diverge할 수 있는 limit을 걸어 
$\to$ "stabilize around climatological  distributions w/o accurately predicting the specific future evolution"
$\to$ not correctable하니 metric에선 제외
## Not capturing errors due to unobserved variables
> ~ finer resolution forecats typically yield better results compared to coarser ones. Thus, <font color="#00e676">error reduction is an expected outcome of higher-resolution data</font>, indicating a natural skill limit imposed by the data resolution rather than the ML model itself.

## Existing metrics lack a reference point for highlighting error accumulation
여러 metrics를 합쳐서 fixable error accumulation을 assess하려고 하지만, 합친다고 잘 잡히지 않더라. 
그래서 clear reference model이 필요하다. 
근데 그 reference model, 주로 ECMWF's ENS & HRES는 ML한테 따잇 당했다. 
highlight performance gap 못할 거다

---
# 4. Defining Error accumulation

*Definition*: error accumulation $\delta(t)$ over a period of time $T$
$$\displaystyle \delta(t) = \mathbb{E}_{x_{1:c}\sim \text{data}}\text{KL}(p_{\text{gen}}(x_{t+c}\vert x_{1:c}\vert\vert p_{\text{truth}}(x_{t+c}\vert x_{1:c})))$$
$x$: possible sequences drawn from the data distribution
$x_{1:c}$: context data / e.g. initial conditions
$p_{\text{gen}}$: assessed generative model
$p_{\text{truth}}$: truth model (but inaccessible) $\rightsquigarrow$ $p_{\text{cts}}$: continuous forecasting model로 교체하면
####  $$\displaystyle \delta(t) \approx \mathbb{E}_{x_{1:c}\sim \text{data}}\text{KL}(p_{\text{gen}}(x_{t+c}\vert x_{1:c}\vert\vert p_{\text{cts}}(x_{t+c}\vert x_{1:c})))$$

note) [[Kullback-Leibler (KL) divergence|KL divergence]]

![[Pasted image 20241001111116.png]]
초반부에서 iterative rollout error에 의해 저하된 potential predictability를 끌어낼 수 있고, time-step 200 넘어가면 chaos에 의한 거라서 negligible한 impact이다.

## Calculating the metric in practice
1. sample data from $p_\text{pen}(x_{t+c}\vert x_{1:c}))$
   $\because \not\exists$  explicit conditional marginal density function in autoregressive models
2. approximate the densities of $x_{t+c}\vert x_{1:c}$ by fitting normal distribution
3. apply the explicit form of KL divergence for normal distributions

## Illustrative examples
[[#Capturing explosive forms]], [[#Capturing non-explosive forms]], [[#Not capturing errors due to STIC]] 각각 원하는 대로 잘 되었다.

---
# 5. Regularization Strategy
## Classic maximum likelihood objective
$$\begin{align}
\arg\max_{\theta} \bigg( & \mathbb{E}_{x_{1:n}\sim p_{\text{truth}}} \log p_{\text{gen},\theta}(x_{c+1}, ..., x_{c+n}|x_{1:c}) \\
& - \frac{\lambda}{n}\sum_{t=1}^n \mathbb{E}_{x_{1:c}\sim p_{\text{truth}}} 
\text{KL}\left(p_{\text{gen},\theta}(x_{t+c}|x_{1:c}) \| p_{\text{cts}}(x_{t+c}|x_{1:c})\right)\bigg)
\end{align}$$
## Practical implementation
$$\begin{align}
\arg\max_{\theta} \bigg( & \mathbb{E}_{x_{1:n}\sim p_{\text{truth}}} \log p_{\text{gen},\theta}(x_{c+1}, ..., x_{c+n}|x_{1:c}) \\
& - \frac{\lambda}{n}\sum_{t=1}^n \mathbb{E}_{x_{1:c},x_{t+c-1}\sim p_{\text{truth}}} 
\text{KL}\left(p_{\text{gen},\theta}(x_{t+c}|x_{t+c-1}) \| p_{\text{cts}}(x_{t+c}|x_{1:c})\right)\bigg)
\end{align}$$
에서 각 input data를 random-walk noise (Gaussian)을 더하고 
$p_{\text{gen, } \theta}(x_{t+c} \vert x_{t+c-1})$ & $p_{\text{cts, } \theta}(x_{t+c} \vert x_{1:c})$ $\sim$ Normal

## Future directions
1. rollout + noise 대신에 replay buffer 사용
2. KL 계산에 normal 사용 대신 adversarial training 사용
---
# 6. Experiments
뭘로 하던간에 Generative model + noise + penalty한 게 좋더라

---
# 