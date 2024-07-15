## add_derived_vars
- 용도: 데이터셋에 연간 및 일간 진행도 특성을 추가
- 사용법:
  ```python
  dataset = xarray.Dataset(...)
  add_derived_vars(dataset)
  ```

## add_tisr_var 
- 용도: 데이터셋에 TISR(Top of Atmosphere Incident Solar Radiation) 특성을 추가, value를 [[solar_radiation.py]]에서 계산해서 추가해줌
- 사용법:
  ```python
  dataset = xarray.Dataset(...)
  add_tisr_var(dataset)
  ```

## extract_input_target_times
- 용도: 데이터셋에서 입력 기간과 목표 선행 시간에 해당하는 데이터를 추출
- 사용법:
  ```python
  dataset = xarray.Dataset(...)
  inputs, targets = extract_input_target_times(
      dataset,
      input_duration='18h',
      target_lead_times=['3d', '5d']
  )
  ```

## extract_inputs_targets_forcings
- 용도: 데이터셋에서 입력, 목표, 강제력 변수를 추출하고 처리
- 사용법:
  ```python
  dataset = xarray.Dataset(...)
  inputs, targets, forcings = extract_inputs_targets_forcings(
      dataset,
      input_variables=(...),
      target_variables=(...),
      forcing_variables=(...),
      pressure_levels=(...),
      input_duration='24h',
      target_lead_times='3d'
  )
```
