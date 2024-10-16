---
author: Christopher Bretherton
---

### Weather vs Climate
Weather랑 Climate가 어떻게 다른가. 

### Physics-based model의 단점
1. systematic error
2. computational cost
	1. 1 simulated year/day requires 20MW electrical power
	     -> 굳이 모든 걸 할 필요는 없는데
3. spread in climate sensitivity

### ML models of weather and climate
##### two main approach
1. Hybrid ML
2. Full model emulation, FME
     전체 모델을 replace

##### Expectation
1. Hybrid가 systematic bias를 줄일 수 있길
2. FME가 더 빠르게 예측할 수 있길
3. training 사용 범위에는 잘 들어오겠다만 extreme에는 잘 못해

### Hybrid SOTA: Neural GCM
[[@D. Kochkov, et al., 2024]]

### The machine learning revolution in weather forecasting
2018년 즈음부터 계속 신상 모델이 떴고, 지금 GraphCast가 제일 좋다더라...
죄다 ERA5를 training data로 사용했고, 그걸 재생산하는 거
허벌나게 빠르다

### Diverse ML architectures used for atmospheric modeling
ML 안에서 2가지 방법으로 진행됨
1. Horizontal exchange
     Fluid dynamics처럼
2. Gird-column porcessing

Fuxi가 single GPU로 된다고? #Question 

### Adapting a weather emulator to climate modeling
reanalysis가 most reliable since 1980

ocean이 중요하다, climate에. 어떻게 model에 넣을 것인가?
놓침

### ACE
seasonal cycle of ocean temp.를 잘 하려고 했다

내꺼는 extreme rainfall까지 잘 되었다...

### Conclusion
