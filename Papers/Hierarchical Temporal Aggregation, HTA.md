Pangu-Weather가 오차 누적으로 인한 skill 부족 해결하기 위해 사용한 방법
#### 방법
1st. develop 4 separate ML models trained to forecast at different lead times; 1, 3, 6, 24 hr
2nd. combine predictions during inference

#### 장점
1. reduction of the number of applications of the ML model for any given forecast lead time
2. the ability to provide forecasts with 1-hr granularity (세분성)

#### 단점
may lead to unphysical discontinuities in forecast evolution

