```ad-note
[[2024-08-14]] Talk w/ Prof.
```
### Objective
GraphCast가 butterfly Effect를 mimic하는 지 확인해보자
$\Rightarrow$ 만일 가능하다면 ensemble로 활용할 수 있다
### Procedure
1. [x] graphcast `test.ipynb` 수리하기 ✅ 2024-08-19
	1. 왜 내 마음대로 출력 시간대를 조정할 수 없는가? 
	   100장도 뽑았었는데 뭔갈 잘못 건드렸다!
	   
2. [x] 사용할 GC 모델 list $\rightarrow$ 학습 기간 확인 요망 ✅ 2024-08-19
	1. GC_original: 0.25$^\circ$ / 37 level / train: 1979~2017
	2. GC_operational:  0.25$^\circ$ / 37 level / train: 1979~2017 + fine-tuned: 2016~2021
	   
3. [x] input 시간대 설정 & 데이터 다운로드 ✅ 2024-08-19
	1. [[@T.Selz and G. C. Craig, 2023#Initial Conditions]]는 2021.06.26T00h을 사용함 $\rightarrow$ operational에 포함된 듯. **original 사용해야 함**.
	   $\because$ NA에 strong continental summertime convection
	2. Criteria
		1. strong continental convection period
		2. GC training에 사용되지 않은 period
		3. **그냥 똑같은 걸로 쓰기**
	3. 다운 받으러 가기
	   [[Input Data 다운]]
	4. 데이터 합성까지 완료하기
	   
4. [x] perturbation method 구현 ✅ 2024-09-05
	1. prof.'s advice
	   $$\textsf{value} \leftarrow \textsf{value} + \sigma \cdot \lambda \textsf{ Gaussian Noise} $$
	   "자세한 건 책 참조"
	2. t2m climatology STD 값을 조절하자
		1. 어떤 std를 써야 하는가
			1. 00 / 06 / 12 / 18h일 때 각 cell의 std를 해야 하지 않을까
	3. perturbation size를 잘 조절
		1. 일단 1로 뽑고 0.001로도 뽑아보자
	4. 3-variable model을 구현해서 그거랑 비슷하게 되는지 아닌지?
	   
5. [x] Perturbed Output 뽑기 ✅ 2024-09-05
	1. 변수 1개 지정
	2. 그 변수에만 다양하게 perturb 주기
	3. output 저장 (let's say "ensemble")   
	   
6. ensemble을 어떻게 비교할 것인가?
	1. 3-variables 모델과 비교해본다?
	2. 지훈에게 ECMWF ensemble 50개를 받아서 계절만 비슷하게 해서 비교해봐라 spread를 - prof. 
7. 0.5$\sigma$, 1$\sigma$, 1.5$\sigma$, 2$\sigma$까지 사용해서라도 벌어지게 해보자. 얼마나 해야 더 벌어질까 
	5$\sigma$까지 해보자
	잘 안 됨.
8. 다른 변수들에도 줘야 하지 않을까
	1. 변수 11개 std 구하기.....
9. 좀 더 지역을 낮춰서 보자 / 안 됨
10. 정리해서 교수님과 논의논의해보러 가기... 그림을 이쁘게 뽑아보자 
	1. 2021-06-21일자로 다시 다운로드
	2. perturbation 다시 주기
	3. GC 딸각 돌리기
	4. plot 조지기
		1. global mean
		2. east asia `.sel(lat=slice(25, 60), lon=slice(102.5, 150))`
	5. 이쁘게 플롯해서 저장은 해둬야 할 듯
#### Global Mean
![[2m_temperature_forecast_global mean_0.001to5_2021-06-21.png]]
#### East Asia Mean
![[2m_temperature_forecast_east asia mean_0.001to5_2021-06-21.png]]

---
```ad-note
[[2024-10-08]] Talk w/ Prof.

[[GraphCast Perturbation Canvas.canvas|GraphCast Perturbation Canvas]]
```
1. Obscured feature test로 넘어가기
	1. 랜덤 지역에만 perturbation을 주기 `add_region_perturbation`
	2. 랜덤 지역에 값을 0 혹은 $\pm$ 99999 극한값으로 줘보기
	3. 기상천외한 방법을 줘보기
2. input dataset 만들기 #WorkingOn 

## References
[1] [[@T.Selz and G. C. Craig, 2023]]
[2] [[@M. Bonavita, 2024]]
