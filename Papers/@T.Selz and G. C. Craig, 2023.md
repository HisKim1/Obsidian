---
title: Can Artificial Intelligence-Based Weather Prediction Models Simulate the Butterfly Effect?
site: https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2023GL105747
summary: 판구가 butterfly effect 부족으로 앙상블 못 쓴다는 근거로 쓰인 논문
keyword: 
status:
  - NotYet
aliases: 
tags:
  - paper
when_published: 2023-10-26
where_published:
  - Geophysical Research Letters
---
```ad-summary
3줄 요약
```

```ad-abstract
We investigate error growth from small-amplitude initial condition perturbations, simulated with a recent artificial intelligence-based weather prediction model. From past simulations with standard physically-based numerical models as well as from theoretical considerations it is expected that such small-amplitude initial condition perturbations would grow very fast initially. This fast growth then sets a fixed and fundamental limit to the predictability of weather, a phenomenon known as the butterfly effect. We find however, that <span style="background:rgba(0, 230, 118, 0.55)">the AI-based model completely fails to reproduce the rapid initial growth rates and hence would incorrectly suggest an unlimited predictability of the atmosphere</span>. In contrast, if the initial perturbations are large and comparable to current uncertainties in the estimation of the initial state, the AI-based model basically agrees with physically-based simulations, although some deficits are still present.
```

# Introduction
> The<font color="#00e676"> "butterfly effect" </font>refers to a well-known and unfortunate property of the atmospheric circulation: <font color="#00e676">Tiny</font> uncertainties or errors in the initial conditions are rapidly <font color="#00e676">amplified,</font> creating a fundamental, intrinsic <font color="#00e676">predictability limit </font>for weather forecasting that <font color="#00e676">cannot be overcome.</font>

limit 존재 원인= scale interactions
: highly non-linear dynamics인 convective scale에서 latent heat release가 rapid error growth 야기

case 1) <font color="#00e676">small amplitude perturbation</font>
spatial structure 중요 X
tiny error 
$\rightarrow$ rapid growth 
$\rightarrow$ saturation of small-scale errors 
$\rightarrow$ subsequent upscale error propagation

case 2) <font color="#00e676">larger-amplitude uncertainties </font>on synoptic and planetary scales
:=up-amplitude growth
$\forall$ scale에서 exponential error growth until saturation

$\therefore$ 현재 WP의 error는 충분히 커 $\rightarrow$ case 2 dominates
만일 uncertainty가 현재의 10~20%로 줄면 case 1 발생 가능

In this paper, 
Pangu의 butterfly effect 능력 평가하겠다
ICON이라는 PDE 기반 모델과 비교하겠다
error growth를 잘 하는지 보겠다

---
# Conclusion

---
# Method

---
# Result

---
# References
