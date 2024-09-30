---
title: Defining error accumulation in ML atmospheric simulators
site: https://arxiv.org/abs/2405.14714
summary: 딥러닝 대기 모델에서 에러는 무엇인가
keyword: 
status:
  - WorkingOn
aliases: 
tags:
  - paper
when_published: 2024-05-23
where_published:
  - arXiv
---
```ad-summary
3줄 요약
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
## Capturing explosive forms
= (ENS mean이 indefinitely grow할 때) + (ENS mean이 stable할 때)
$$X_{k, t+1} = X_{k,t} + Z_{k,t} \quad (Z_{k,t} \sim N(0,1) )$$
**Metric 1) RMSE**: bad
$\because$ generative model의 mean은 truth에 붙어서 각각이 explode한 걸 잡아내지 못 함

**Metric 2) spread/skill**: better
시간에 따라 증가 $\to$ reflecting the diverging trajectories

**Metric 3) own metric**: evident

## Capturing non-explosive forms
**Metric 1) RMSE**: low


**Metric 2) spread/skill**: better
시간에 따라 증가 $\to$ reflecting the diverging trajectories

**Metric 3) own metric**: evident

## Not capturing errors due to STIC

## Not capturing errors due to unobserved variables

## Existing metrics lack a reference point for highlighting error accumulation

---
# 4. Defining Error accumulation

---
# 5. Regularization Strategy

---
# 6. Experiments

---
# 