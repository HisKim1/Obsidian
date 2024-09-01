---
title: Can Artificial Intelligence-Based Weather Prediction Models Simulate the Butterfly Effect?
site: https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2023GL105747
summary: 판구가 butterfly effect 부족으로 앙상블 못 쓴다는 근거로 쓰인 논문
keyword:
  - Butterfly effect
  - Difference Kinetic Energy
  - Error growth
status:
  - ==Done==
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
# Discussion
1. MLWP의 장점: low computing cost $\rightarrow$ ensemble members 증가 가능
2. large ensemble: reduce sampling uncertainty $\rightarrow$ reliable extreme event probability forecast
그래서 가능할 것 같지만 <font color="#00e676">MLWP는 error growth가 realistic하지 않다</font>
$\because$ intrinsic predictability limit = earth's atm physical property라서 measure or observe되지 않는다

```ad-question
"Reanalyzes like ERA5 however never come close enough to the true state to enable an observation of the butterfly effect, since our current observational and assmilation system still has very significant errors."

$\rightarrow$ 논리상 필요한 문장인 건 이해하겠다만, 이러면 ERA5를 기준으로 비교하고 예측하는 모든 게 무의미하다는 뜻이 되지는 않나
```

1. Reanalysis 자체에 error가 있다
2. NN은 그 만큼의 approximated development만 배울 수 있다
   pf) 100% perturbation에서 error growth
다른 MLWP도 비슷할 거 같은데, autoregressive model은 어떨 지 궁금하긴 하다

> the essence of the butterfly effect is upscale<font color="#00e676"> propagation </font>of fast-growing <font color="#00e676">uncertainties</font> on small scales, mainly related to <font color="#00e676">convection and precipitation.</font>

low-resolution model을 해결하기 위해 stochastic convection scheme을 소개했었는데, 이걸 적용할 수도 있을 듯하다
e.g. random seed로 stochastic parameterization / stochastic infer via super-resolution method

$\therefore$ MLWP가 butterfly effect를 모사하지는 못 하지만, reliable prediction을 못 한다는 것은 아니며, reliable ensemble을 만들 수 없다는 뜻도 아니다. 다만 현재의 initial uncertainty에서 이 정도가 유의미한지 아직 모르는 것일 뿐.

---
# Experiments

### The AI-Based Model Pangu
deterministic forecasts / 13 pressure levels
5 pressure level variables (u, v, t, z, q) & 4 surface variables (u10, v10, t2m, slp)
0.25$^\circ$
1, 3, 6, 24hr를 각각 학습 $\rightarrow$ 24부터 빈 틈을 채워나가는 방식

### The PDE-Based Model ICON
<font color="#00e676">ICO</font>sahedral <font color="#00e676">N</font>on-hydrostatic model
PDE-based NWP
자세한 건 알 필요 없을 듯?

### Initial Conditions
2021.06.26 00h 기준으로 진행 
$\because$ 북미 summer convection $\uparrow \quad \Rightarrow$ error growth $\uparrow$ / 당연히 maritime & wintertime도 global diagnostics의 avg에 포함될 것

ECMWF의 ERA5 reanalysis 대신 operational analysis 사용
$\because \quad \exists$  minor & insignificant differences

initial perturbations는 ECMWF의 ensemble data assimilations (EDA)에서 찾음 @Isaksen et al., 2010

### Experiments
총 5가지 실험
모델명-해상도-perturbation scale
1. Pangu-100%
2. Pangu-0.1%
3. ICON-LR-100%
4. ICON-LR-0.1%
5. ICON-HR-0.1%
(ICON-HR-100%은 의미없다는 선행 연구가 있어서 제외)

ICON-HR이 best estimate of convective-scale error growth & butterfly effect일 것이라 예상

> The percentage factor (100% or 0.1%) indicates a rescaling of the initial condition perturbations derived from the EDA system. 

uncertainty를 주는 방법이 EDA에 있나 봄. 거기서 구한 perturbation을 100% 그대로 or 0.1%로  rescale해서 줌
$\Rightarrow$ "butterfly"-like perturbations and provide estimates of the intrinsic limit / a.k.a. "identical twin" experiments

$\therefore$ $\not \exists$ singular vectors & deterministic model $\Rightarrow$ error growth estimation에 좋다!

이외 현실적인 어려움들......

### Diagnostics
300hPa difference kinetic energy, DKE를 기준으로 비교 
(DKE$\neq$ obs - pred error)
$\because$ error growth & intrinsic predictability에 자주 쓰이더라 
$$\text{DKE} = \text{var}(u) + \text{var}(v)$$

DKE의 spectral representation $\propto$ kinetic energy (KE) spectrum of the atm

---
# Results
전반적으로 예측 결과는 비슷하다 (mean, RMSE)
KE가 대부분 중위도에 있어서 DKE도 중위도를 반영$\uparrow$ 
### Time Serise of DKE
##### case 1) 100% perturbation
Pangu, ICON growth rate가 2.2/day, 1.7/day, respectively
$\Rightarrow$ synoptic scale dynamics의 characteristics 

##### case 2) 0.01% perturbation
ICON에서는 initial growth rates $\Uparrow$; $10^{20}$/day during the first 3hr
$\Rightarrow$ fast saturation at small scales

 init uncertainty$\downarrow$
$\rightarrow$ init growth rate$\uparrow$
$\rightarrow$ DKE reduction$\downarrow$ at late times 
$\rightarrow$ predictability limited

##### case 3) Pangu
100%랑 0.1% 결과값이 just shifted vertically by 1000$^2$ 
72hr 뒤 DKE도 100%, 0.1% 각각 2.3, 3.1배

$\therefore$ const. error growth $\Rightarrow$ unlimited predictability & $\not \exists$ butterfly effect

### Spatial Structure of DKE
![[@T.Selz and G. C. Craig, 2023 2024-08-14 09.32.39.excalidraw|600]]
Pangu-100% & Pangu-0.1%는 거의 identical
$\Rightarrow$ init cond.와 무관한 structure

 amplitude가 바뀌면 structure도 바뀌어야 함. 하지만 판구는 0.1%에서 scale만 바뀌었을 뿐. 

### Spectra of DKE
global 300hPa KE & DKE의 spectra를 보았다

1. background spectrum
   perturbation amplitude에 영향 거의 X 
   $\because$ background spectrum = atm or model의 climatological feature
2. Pangu-100%
   0~24h: 500km 이하 looeses energy 
   $\Rightarrow$ lower level error가 not saturated 
   $\Rightarrow$ stagnation of error growth, even at large scales
   24h~: remains stable; no further decay
   1000km 쯤 되면 ICON이랑 비슷하다
3. ICON-LR-100%
   200km 이하 saturated $\Rightarrow$ $\not\exists$ info 4 prediction
   24h~74h: error growth $\Rightarrow$ error가 이어서 synoptic scale에서 growth 
4. ICON-LR-0.1% vs Pangu-LR-0.1%
   판구에서는 butterfly effect의 signature인 instantaneous downscale propagation of the energy peak to smaller scales가 나타나지 않음
   $\Rightarrow$ decorrelation; 
   small difference $\leftrightarrow$ large-scale advection
   원래같으면 !linear error growth in regions of moist convections때문에 error가 smaller scale로 propagate되었어야? 납득 불가
---
# References
 