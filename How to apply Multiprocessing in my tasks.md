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
4) 시간대별 계산 결과 plot
```

---
# Multiprocessing

```ad-question
우리 *forecast1* 서버에는 CPU가 40개나 있는데, 왜 나는 CPU를 1개밖에 쓰고 있지 못할까....
40개를 다 쓸 수만 있다면 작업을 더 빨리 끝낼 수 있지 않을까?

$\Rightarrow$ Multiprocessing으로 서버를 Exploit하자 😎
```

## Definition
여러 [[#Process]]를 서로 다른 core^[core = CPU = processor]에서 <font color="#00e676">동시에 실행</font>하여 parallelism 구현하는 방법
하나의 작업을 분할하여 처리 $\Rightarrow$ resource sharing^[각 process가 실제로 필요한 memory 용량만 차지] $\uparrow$,  scalability^[CPU 40개인 *forecast1*에서 돌리다가 CPU 8개인 내 labtop에서 돌려도 상관 없음. environment에 맞춰 잘 돌아감] $\uparrow$

## Method
접근 방식: 각 <font color="#00e676">CPU에 함수와 parameter를 할당</font>하여 연산한다! 

![[Excalidraw/Drawing 2024-08-09 10.20.33.excalidraw.md|700]]
(coding demo에서 연습해볼 예정)
#### 1)  `from multiprocessing import Pool` 
각 함수를 사용 가능한 CPU `Pool`에 할당하기 위한 모듈

#### 2) `from functools import partial`
함수에게 전달하는 parameter (`arg_list`)가 부분적으로 다를 때

#### 3) `xarray.open_dataset(file_path, chunks = [          ])`
큰 dataset을 잘게 쪼개서 처리 $\Rightarrow$ 자동으로 multiprocessing, lazy evaluation^[불필요한 연산을 하지 않기 위해 계산 결과값이 실제로 필요할 때까지 계산을 미루는 기법]

---
# ⚠ Caution
## case 1 | Memory 사용량을 계산해야 한다!
**Question )**
Suppose that weather1 server has <font color="#00e676">16GB memory</font>, <font color="#00e676">16 multi-processor</font>.
I execute `with multiprocessing.Pool() as Pool` for multiprocessing a function `cal_correlation` which requires <font color="#00e676">at least 2GB memory</font>. What will happen?

**Answer )**
`Pool` module은 16 `cal_correlation`을 생성해 각 CPU에 할당하고 각 `cal_correlation`에게 2GB + $\alpha$ 를 할당하려고 함. 
하지만 required = (2GB + $\alpha$) $\times 16$ >>> 16GB
$\Rightarrow$ 그 어느 `cal_correlation`도 실행에 필요한 최소한의 memory 용량, 2GB,를 할당받지 못 함
$\Rightarrow$ 2GB 이상 할당될 때까지 무한 대기
$\Rightarrow$ **☠ Deadlock 돌입, execution time $\rightarrow \infty$  ☠ 

**Solution )**
1. `with multiprocessing.Pool(processes = 8) as Pool`
   동시에 실행할 프로세스의 수 = 사용할 core의 수를 8개로 고정
2. 각 `cal_correlation` 에 넘어가는 parameters의 사이즈를 조절해 실행에 필요한 최소 memory size를 줄인다

**Moral )**
서버는 나만 쓰는 게 아니다! 남들이 얼마나 CPU, memory를 점유하고 있는지 확인 후 실행해야 함.
memory 용량이 300GB라고 해서 memory를 100% 사용하려 하면 안 된다! ^[컴퓨터에는 수십만개의 background process가 돌아가고 있고 그 process를 위한 memory 공간이 있어야 컴퓨터가 정상적으로 돌아간다. 하다 못해 `ls`, `cd` 같은 linux 명령어도 다 프로세스로 처리되므로 multiprocessing한다고 memory 용량을 다 채워버리면 아무런 조치를 취할 수 없을 것이다...]

## case 2 | Exception occured while executing ...


## case 3 | Overhead < Benefit ?
### Overhead
any combination of <font color="#00e676">excess or indirect</font> computation time, memory, bandwidth, or other resources that are required to perform a specific task^[Wikepidia]

