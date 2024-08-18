```ad-note
[[2024-08-14]] Talk w/ Prof.
```
### Objective
GraphCast가 butterfly Effect를 mimic하는 지 확인해보자
$\Rightarrow$ 만일 가능하다면 ensemble로 활용할 수 있다
### Procedure
1. [ ] graphcast `test.ipynb` 수리하기
	1. 왜 내 마음대로 출력 시간대를 조정할 수 없는가? 
	   100장도 뽑았었는데 뭔갈 잘못 건드렸다!
	   
2. [ ] 사용할 GC 모델 list $\rightarrow$ 학습 기간 확인 요망
	1. GC_original: 0.25$^\circ$ / 37 level / train: 1979~2017
	2. GC_operational:  0.25$^\circ$ / 37 level / train: 1979~2017 + fine-tuned: 2016~2021
	   
3. [ ] input 시간대 설정 & 데이터 다운로드
	1. [[@T.Selz and G. C. Craig, 2023#Initial Conditions]]는 2021.06.26을 사용함 $\rightarrow$ operational에 포함된 듯. original 사용해야 함.
	   $\because$ NA에 strong continental summertime convection
	2. Criteria
		1. strong continental convection period
		2. GC training에 사용되지 않은 period
		   
4. [ ] perturbation method 구현
	1. prof.'s advice
	   $$\textsf{value} \leftarrow \textsf{value} + \sigma \cdot \lambda \textsf{ Gaussian Noise} $$
	   "자세한 건 책 참조"
	   
5. [ ] Perturbed Output 뽑기
	1. 변수 1개 지정
	2. 그 변수에만 다양하게 perturb 주기
	3. output 저장 (let's say "ensemble")
	   
6. ensemble을 어떻게 비교할 것인가?
	1. 추후 논의 예정

## References
[1] [[@T.Selz and G. C. Craig, 2023]]
[2] [[@M. Bonavita, 2024]]
