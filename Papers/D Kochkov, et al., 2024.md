---
title: Neural general circulation models for weather and climate
site: https://www.nature.com/articles/s41586-024-07744-y#Sec2
summary: 
keyword: 
status:
  - WorkingOn
aliases: 
tags:
  - paper
when_published: 2024-07-22
where_published:
  - nature
---
```ad-summary
3줄 요약
```

```ad-abstract
General circulation models (GCMs) are the foundation of weather and climate prediction. GCMs are physics-based simulators that combine a numerical solver for large-scale dynamics with tuned representations for small-scale processes such as cloud formation. Recently, machine-learning models trained on reanalysis data have achieved comparable or better skill than GCMs for deterministic weather forecasting. However, these models have not demonstrated improved ensemble forecasts, or shown sufficient stability for long-term weather and climate simulations. Here we present a ==GCM that combines a differentiable solver for atmospheric dynamics with machine-learning components== and show that it can generate forecasts of deterministic weather, ensemble weather and climate on par with the best machine-learning and physics-based methods. NeuralGCM is competitive with machine-learning models for ==one- to ten-day forecasts==, and with the European Centre for Medium-Range Weather Forecasts ensemble prediction for one- to fifteen-day forecasts. With prescribed sea surface temperature, NeuralGCM can ==accurately track climate metrics for multiple decades, and climate forecasts with 140-kilometre resolution show emergent phenomena== such as realistic frequency and trajectories of tropical cyclones. For both weather and climate, our approach offers orders of magnitude computational savings over conventional GCMs, although our model does not extrapolate to substantially different future climates. Our results show that end-to-end deep learning is compatible with tasks performed by conventional GCMs and can enhance the large-scale physical simulations that are essential for understanding and predicting the Earth system.
```

# Introduction
## data-driven model의 문제점
1. they do not produce calibrated uncertainty estimates, which is essential for useful weather forecasts.
2. MSE for averaging over uncertainty, producing unrealistically blurry predictions when optimized for multi-day forecasts
3. misrepresent derived (diagnostic) variables such as geostrophic wind
4. the lack of coupling between machine-learning components and the governing equations during training potentially causes serious problems, such as instability and climate drift [[N. Brenowiz and C. Bretherton, 2019]]


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


---
# Result

---
# References
