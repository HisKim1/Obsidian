```ad-question
예측을 대부분 대기 하부를 기준으로 비교했던데, 
1. 왜 다 하부로 했을까?
2. 대기 상층부의 이벤트도 잘 잡힐까?
e.g. [[Rossby Waves]]를 잡을 수 있을까?
또 대기 상층부에 있는 이벤트가 뭐가 있지
```
- 제트기류 (Jet Stream) 예측:
    - 위치, 강도, 변동성 예측 정확도
- [[Sudden Stratospheric Warming]]:
    - #Question 얘를 예측 잘 하면 좋을 듯?!
      발생 시기, 강도, 지속 기간 예측 정확도
    - 10hPa 인근 온도 변화 
- 대류권계면 접힘 (Tropopause Folding):
    - 발생 위치, 강도, 지속 시간 예측
- [[Rossby Waves]]:
    - 파동의 진폭, 위상, 전파 속도 예측
- 대류권 상부 저기압 (Upper-level Low):
    - 발달, 이동 경로, 강도 예측
- 성층권-대류권 교환 (Stratosphere-Troposphere Exchange):
    - 교환 강도, 위치, 시기 예측
- 오존 분포:
    - 오존층 두께, 오존홀 발달 예측
- 중력파 (Gravity Waves):
    - 발생, 전파, 소멸 과정 예측
- 극 소용돌이 (Polar Vortex):
    - 강도, 안정성, 분열 시기 예측
- 권계면 (Tropopause) 높이:
    - 고도 변화, 온도 구조 예측


### Dataset의 dim., var., prop.s
어떤 dataset을 준비해야 하나

```
1. Dimension
   
---
2. Coordinates
   lon: 1440
   lat: 721
   level: 37
   time: 
   
---
3. Variables
	1. Surface (5)
	   "2m_temperature"
	   "mean_sea_level_pressure"
	   "10m_v_component_of_wind"
	   "10m_u_component_of_wind"
	   "total_precipitation_6hr"
	   
	2. Atmospheric (6)
	   "temperature"
	   "geopotential"
	   "u_component_of_wind"
	   "v_component_of_wind"
	   "vertical_velocity"
	   "specific_humidity"
	   
	3. Forcing (5)
	   "toa_incident_solar_radiation"
	   "year_progress_sin"
	   "year_progress_cos"
	   "day_progress_sin"
	   "day_progress_cos"
	   
	1. Static (2)
	   "geopotential_at_surface"
	   "land_sea_mask"	   
```
 
 ---
 ### Input Data 제작기
 
- [ ] [[Input Data 다운]]
- [x] [[eval_target 만들기]]
- [ ] [[eval_forcing 만들기]]
