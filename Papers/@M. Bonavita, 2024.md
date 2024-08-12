---
title: On some limitations of current machine learning weather prediction models
site: https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2023GL107377
summary: 판구가 장기에서 geo, ageo. wind vertical struct 예측을 못하더라.
keyword: 
status:
  - WorkingOn
aliases: 
tags:
  - paper
when_published: 2024-06-24
where_published:
  - Geophysical Research Letters
---
```ad-summary
3줄 요약
```

```ad-abstract
Machine Learning (ML) is having a profound impact in the domain of Weather and Climate Prediction. A recent development in this area has been the emergence of fully data‐driven ML prediction models which routinely claim superior performance to that of traditional physics‐based models. We examine some aspects of the forecasts produced by three of the leading current ML models, <span style="background:rgba(205, 244, 105, 0.55)">Pangu‐Weather, FourCastNet and GraphCast</span>, with a focus on their fidelity and physical consistency. The main conclusion is that these <span style="background:rgba(205, 244, 105, 0.55)">ML models are not able to properly reproduce sub‐synoptic and mesoscale weather phenomena</span> and <span style="background:rgba(205, 244, 105, 0.55)">lack the fidelity and physical consistency</span> of physics‐based models and this has impacts on the interpretation of their forecasts and their perceived skill. Balancing forecast skill and physical realism will be an important consideration for future ML models.
```

# Introduction
ML-based  모델이 급격히 발전하고 있다.
w/ 예시 모델들

여기서는
> The apporach we have taken is to choose a representative sample of the current generation of MLWP model, Pangu-Weather, FourCastNet and GraphCast and analyze their forecast output from<font color="#00e676"> the point of view of physical consistency and fidelity.</font> 

---
# Data and Methods
> As noted by the Pangu-Weather developers, the <font color="#00e676">repeated application</font> of an imperfect model leads to rapid <font color="#00e676">accumulation of errors</font> and can limit its predictive skill. 

> MLWP models <font color="#00e676">oviate this probelm </font>by progressively<font color="#00e676"> increasing the forecast horizon </font>over which the ML model is trained, typically at the price of <font color="#00e676">increased smoothness</font> of the forecasted states.

Pangu는 문제 해결 위해 [[Hierarchical Temporal Aggregation, HTA]] 사용

---
# Spectral Diagnostics
MLWP의 잘 알려진 문제는 lead time따라 forecast가 "blurry"해진다는 것.

> $\because$ trained to<font color="#00e676"> optimize a weighted mean squared/absolute error</font> (L2/L1) norm of forecast errors.
> $\Rightarrow$ producing forecasts closer to the mean of the forecast pdf, tat is, <font color="#00e676">smoothing out unpredictable details</font> from the forecast

smoothing되어서 power spectra 봤을 때 높은 wavenumber쪽이 낮다 = spectral energy reduction
$\Rightarrow$ ML 모델들이 less spectrally resolved forecast를 produce
$\Rightarrow$ ML의 effective resolution = 500~700km이고 lead time 따라 감소한다
(+[[Hierarchical Temporal Aggregation, HTA]] 효과 좀 있더라)
$\Rightarrow$ synoptic은 괜찮지만, sub-synoptic & mesoscale이면 effect가 noticeable

왜 MLWP가 progressive loss of detail?
bc trained to produce forecasts that are closer to an ensemble forecast mean than to deterministic forecst

spectral 특징을 보면 예측 모델의 성능이 scale따라 달라지더라

> <font color="#00e676">The spectral characteristics</font> of the forecasts can in general affect standard <font color="#00e676">deterministic forecast skill performance</font> measures. 
> . . .
> It is apparent how the <font color="#00e676">less spectrally resolved forecasts appears to be more skillful</font> than their higher resolution version.

---
# Physical Consistency of Pangu-Weather forecasts

## Geostrophic Wind Balance
$$V_g = \frac{1}{f}\hat{k} \times \nabla_p\Phi $$
$$V_ag = V - V_g$$
> <font color="#00e676">Ageostrophic winds in midlatitude synoptic system</font> are connected with <font color="#00e676">areas of convergence/divergence</font> which, through the continuity equation, are linked to <font color="#00e676">areas of vertical motions and active weather</font>.

$\Rightarrow$ MLWP가 NWP보다  ageostrophic을 약하게 예측 

---
# Result

---
# References
