[official docs](https://graphcastgfs.readthedocs.io/en/latest/index.html#)

## 1. 37 pressure level 모델 제거
$\because$ storage restriction & **limited accuracy?**

## 2. 13 pressure level GraphCast ML fine-tuning

### Trained data
- input: NCEP's GDAS | 2021년 3월 23일 ~ 2022년 9월 1일
- ground truth: ECMWF ERA5
- validation: 2022년 9월 1일 ~ 2023년 1월 1일
- test: 2023년 1월 1일 ~ 2024년 1월 1일
### 주요 변경 사항
- 새로운 가중치로 전역 예측 생성
- GraphCastGFS v1 (구글 DeepMind 제공):
  - 12 timestep (3일)
  - ERA5 데이터만 사용
- GraphCastGFS v2:
  - 14 timestep ()
  - GDAS 및 ERA5 데이터 사용
  - v1 대비 예측 정확도 크게 향상