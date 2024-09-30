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



---
# 7. Discussion

---
# 2. Background

---
# 3. Problem Formulation: capturing error accumulation

---
# 4. Defining Error accumulation

---
# 5. Regularization Strategy

---
# 6. Experiments

---
# 