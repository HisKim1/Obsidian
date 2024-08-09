---
presenter: Hisu Kim
keyword:
  - Multiprocessing
  - Process
  - Pool
  - Dask
summary: CPU를 효율적으로 착취하는 방법 w/ python
---
# Background^[Operating System Concepts, 10th Ed. feat. by Silberschatz et al.]

```ad-question
우리 *forecast1* 서버에는 CPU가 40개나 있는데, 왜 나는 CPU를 1개밖에 쓰고 있지 못할까....
40개를 다 쓸 수만 있다면 작업을 더 빨리 끝낼 수 있지 않을까?
```

## Process
### Definition
a program in execution load into memory 
$\rightarrow$ `.ipynb` 커널 실행시 process 1개라고 봐도 무방함 (엄밀한 설명은 아님)

### Type
1. I/O-bound process
   <font color="#00e676">I/O (Input/output)</font>하는 데에 시간을 더 많이 쓰는 프로세스
   = 연산에 필요한 파일을 불러오거나 계산이 완료된 파일을 저장하는 데 시간 소요 $\uparrow$ 
   $\rightarrow$ CPU 사용 시간 $\simeq$ 5% / process state = waiting
```ad-example
1) 대용량 기상 데이터 파일 읽기/쓰기 = disk I/O
2) 원격 기상 데이터베이스 쿼리 = network I/O
3) 이미지 저장 = disk I/O
```
2. CPU-bound process
   <font color="#00e676">CPU 연산</font>에 시간을 더 많이 쓰는 프로세스
   $\rightarrow$ CPU 사용 시간 $\simeq$ 90% / process state = running
```ad-example
1) 복잡한 대기 순환 모델 실행
2) 대규모 기후 데이터에 대한 통계값 연산
3) 다양한 초기 조건에 대한 앙상블 기상 예측
```

## Multiprocessing
### Definition
여러 [[#Process]]를 서로 다른 core^[core = CPU]에서 동시에 실행하여 parallelism 구현하는 방법
하나의 작업을 분할하여 처리 $\Rightarrow$ resource sharing^[각 process가 실제로 필요한 memory 용량만 차지] $\uparrow$,  scalability^[CPU 40개인 *forecast1*에서 돌리다가 CPU 8개인 내 labtop에서 돌려도 상관 없음. environment에 맞춰 잘 돌아감] $\uparrow$

### Method
coding demo에서 연습해볼 예정
#### 1)  `form multiprocessing import Pool` 


#### 2) `from functools import partial`

#### 3) `xarray.open_dataset(file_path, chunks = [          ])`
