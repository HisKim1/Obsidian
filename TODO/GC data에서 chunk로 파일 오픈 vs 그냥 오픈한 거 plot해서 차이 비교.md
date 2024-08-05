### Original process
1. 각 변수별 data 3개를 다운
2. 3개 파일을 1개로 concat / precip은 6hr accumulate
3. 그러고 저장
4. 그러고 각 변수별 multiprocessing으로 plot

```ad-question
#### 09:30 | 지훈이형의 의문

chunk로 열었을 때랑 그냥 했을 때 $10^{-6}$의 결과 차이가 발생한다.
multiprocessing의 영향? 기타 연산 방식의 변화로 인한 차이 발생?
```
![[Pasted image 20240805095841.png|500]]
### Test
**case 1.** @ data_concatenator
	1-1. 변수별 파일을 chunk로 열고 합치기
		file name: `testdata/ERA5_2022-01-01_all_chunk.nc`
	1-2. precipitation만 연산을 chunk로
		file name: `testdata/ERA5_2022-01-01_tp_chunk.nc`
	
**case 2.** @ data_comparison
	2-1. pressure level 싹 다 뽑아보자
	2-2. ERA5만 chunk로 open
	2-3. google만 chunk로 open
	2-4. 둘 다 chunk로 open

|        |             |            |           |
| ------ | ----------- | ---------- | --------- |
| input  | all_chunk   | tp_chunk   | none      |
| output | all\_both\_ | tp\_both\_ | none_both |
| Done?  | ✈           |            |           |
