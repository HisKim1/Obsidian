---
title: Neural general circulation models for weather and climate
site: https://www.nature.com/articles/s41586-024-07744-y#Sec2
summary: NeuralGCM=NN + NWP / 날씨부터 기후까지 / 첫 hybrid 모델
keyword:
  - NeuralGCM
status:
  - ==Done==
aliases: 
tags:
  - paper
when_published: 2024-07-22
where_published:
  - Nature
---
```ad-summary
GCM의 2부분 중에서 physics를 NN으로 대체했더니 !blur한 예측을 하더라. 
당연히 연산 cost 줄었다.
앞으로 나아가야 할 방향성을 실현한 모델이지 않을까.
```

```ad-abstract
General circulation models (GCMs) are the foundation of weather and climate prediction. GCMs are physics-based simulators that combine a numerical solver for large-scale dynamics with tuned representations for small-scale processes such as cloud formation. Recently, machine-learning models trained on reanalysis data have achieved comparable or better skill than GCMs for deterministic weather forecasting. However, these models have not demonstrated improved ensemble forecasts, or shown sufficient stability for long-term weather and climate simulations. Here we present a ==GCM that combines a differentiable solver for atmospheric dynamics with machine-learning components== and show that it can generate forecasts of deterministic weather, ensemble weather and climate on par with the best machine-learning and physics-based methods. NeuralGCM is competitive with machine-learning models for ==one- to ten-day forecasts==, and with the European Centre for Medium-Range Weather Forecasts ensemble prediction for one- to fifteen-day forecasts. With prescribed sea surface temperature, NeuralGCM can ==accurately track climate metrics for multiple decades, and climate forecasts with 140-kilometre resolution show emergent phenomena== such as realistic frequency and trajectories of tropical cyclones. For both weather and climate, our approach offers orders of magnitude computational savings over conventional GCMs, although our model does not extrapolate to substantially different future climates. Our results show that end-to-end deep learning is compatible with tasks performed by conventional GCMs and can enhance the large-scale physical simulations that are essential for understanding and predicting the Earth system.
```

# Introduction
## data-driven model의 문제점
1. they do not produce calibrated uncertainty estimates, which is essential for useful weather forecasts.
2. MSE for averaging over uncertainty, producing unrealistically blurry predictions when optimized for multi-day forecasts
3. misrepresent derived (diagnostic) variables such as geostrophic wind
4. the lack of coupling between machine-learning components and the governing equations during training potentially causes serious problems, such as instability and climate drift [[@N. Brenowiz, C. Bretherton, 2019]]


---
# Neural GCMs
![[Pasted image 20240802130028.png]]
differentiable dynamical core + learned physics module
- dynamical core: large-scale fluid motion & thermodynamics 
- learned physics: predicts the effect of unresolved processes

For weather
- ECMWF-HRES: best-in-class conventional physics-based
- GraphCast & Pangu: ML-based
For climate
- global cloud-resolving model
- Atmospheric Model Intercomparison Project, AMIP
---
# Medium-range Weather forecasting
성능 비교에는 [[@S. Rasp, et. al., 2024|WeatherBench2]] 썼다

## Model Accuracy
<font color="#00e676">Deterministic models</font> that produce a single weather forecast for given initial conditions can be <font color="#00e676">compared effectively using RMSE skill</font> at short lead times.

Ensembles are essential for <font color="#00e676">capturing intrinsic uncertainty</font> of weather forecasts, especially at longer lead times.
## Case Study
An important characteristic of forecasts is <font color="#00e676">their resemblance to realistic weather patterns</font>.

<font color="#00e676">Blurrier forecasts</font> correspond to <font color="#00e676">physically inconsistent</font> atmospheric conditions and misrepresent extreme weather.

## Spectra
We can <font color="#00e676">quantify the blurriness</font> of different forecast models <font color="#00e676">via their power spectra</font>.

## Water budget

## Geostrophic Wind Balance
A recent study highlighted that Pangu <font color="#00e676">misrepresents the vertical structure</font> of the geostrophic and noted a deterioration at longer lead times. [[@M. Bonavita, 2024]]
Similarly, we observe that GraphCast shows an error that worsens with lead time.
## Generalizing to Unseen Data

---
# Result

---
# References
[[@M. Bonavita, 2024]]