---
title: On some limitations of current machine learning weather prediction models
site: https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2023GL107377
summary: DLWP가 physics param 예측을 못하더라
keyword:
  - Spectral Energy
  - Physical Inconsistency
  - Error growth
status:
  - ==Done==
aliases: 
tags:
  - paper
when_published: 2024-06-24
where_published:
  - Geophysical Research Letters
---
```ad-summary
MLWP가 physics-driven characteristics such as (a)geostrophic wind, spectra, vertical velocity를 잘 못 맞추더라. 이유는 mean을 맞추는 nature of ML 때문. 다만 원하는 특성에만 optimize한다면 충분히 유용할 거다
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
$$V_{ag} = V - V_g$$
> <font color="#00e676">Ageostrophic winds in midlatitude synoptic system</font> are connected with <font color="#00e676">areas of convergence/divergence</font> which, through the continuity equation, are linked to <font color="#00e676">areas of vertical motions and active weather</font>.

$\Rightarrow$ MLWP가 NWP보다  ageostrophic을 약하게 예측 

## Rotational and Divergent Wind components
> <font color="#00e676">Divergence and vorticity fields </font>thus allow to estimate the <font color="#00e676">dynamical consistency of the forecasted wind</font>, in a manner analogous to what<font color="#00e676"> geostrophic balance </font>allows to do in terms of the <font color="#00e676">dynamical consistency of mass and wind fields.</font>

$\Rightarrow$ MLWP에서 $\frac{\text{divergence}}{\text{vorticity}}$가 현저하게 떨어짐
$\Rightarrow$ rotational component랑 vertical motions가 unphysical 

## Vertical Motions
> It is apparent that while the diagnosed $w$ is unrealistic in regions with significant topography (i.e., where isobaric surfaces end up below ground), it is a qualitatively good approximation in low lying areas and over the oceans.

$\Rightarrow$ 판구 예측으로 수식 돌려서 vertical velocity 구해보니까 40% weaker and more diffuse
\+ autoregressive 모델들에서 더 심하게 나타남

><font color="#00e676"> general noisiness and lack of realism </font>of the TC in Pangu-Weather forecast (and the other ML models, ... ) raise further questions about the ability of MLWP models to provide a <font color="#00e676">physically consistent picture of the evolution of the atmosphere</font>.
---
# Discussion and Conclusions
> These advantages appear compelling, there are some caveats.

### 1. cannot be considered general-purpose atmosphere simulators or atmospheric "digital twins."
1) From power spectra, <font color="#00e676">decreasing energy w/ increasing wavenumber</font> (higher spatially resolved scales)
2) ML weather models produce progressively <font color="#00e676">smoother forecasts</font>
   $\rightarrow$ <font color="#00e676">problems in</font> representing fundamental <font color="#00e676">dynamical balance</font> relationships
3) physical balances are not satisfied 
   $\rightarrow$ other quantities that can be <font color="#00e676">diagnosed from balance relationships</font> , ... , <font color="#00e676">are also unrealistic</font>

### 2. View as estimators of the mean of the forecast pdf is also problematic.
1) <font color="#00e676">loss of predictability </font>at medium range lead times (3-5 days) & synoptic spatial scales 
   $\because$ chaotic <font color="#00e676">growth</font> of initial and forecast <font color="#00e676">uncertainties</font>
   $\sim \not\exists$ <font color="#00e676">signature drop in energy</font> of the ECMWF EM at synoptic scales in the medium range (3-5 days) 
2) <font color="#00e676">heteroscedasticity in the distribution of forecast errors </font>with forecast lead time
   $\rightarrow$ MLWP's<font color="#00e676"> reduced forecast variability</font> at smaller spatial scales
   pf) <font color="#00e676">inability</font> of Pangu-Weather to produce <font color="#00e676">realistic error growth</font> from small-amplitude initial condition perturbation (i.e., lack of a "butterfly effect")
   
> $\therefore$ <font color="#00e676">MLWP models in ensemble prediction</font> may turn out to be <font color="#00e676">challenging</font>, at least in terms of <font color="#00e676">following the current paradigm of forecast ensembles </font>as collections of perturbed realizations of physically valid model trajectories.

### Conclusions
> Froecast models with reduced variability and which do not present the standard upscale error growth of physics-based models tend to perform better on deterministic forecast skill measures, especially at longer lead times ("double penalty" effect) and ...

general하게 쓰기는 무리가 있지만 specific aspects로 optimizing하면 쓰기 좋다

loss functions랑 training curricula 잘 골라서 different forecast ranges를 위한 ML도 가능할 듯



---
# References
[[@T.Selz and G. C. Craig, 2023]]
