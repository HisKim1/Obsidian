# 방법
1. 최소한으로만 받아서 돌아가게만 해보는 걸로 우선
2. 다운 받은 2개 파일을 하나로 합쳐 -> done
   precipitation accumulate가 어떻게 되었는지 확인해서 넣어야 함.
   accumulate_precip_dataset함수 작동 
3. 시간을 00z 06z 12z 18z만 선택해서 새로 만들어
4. 넣으면 돌아가야 됨!

[single layer 딸깍딸깍](https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-single-levels?tab=form)
1. Popular
	1. 10m u-component of wind
	2. 10m v-component of wind
	3. mean sea level pressure
	4. 2m temperature
	5. total precipitation -> 얘만 hourly로 다운
4. radiation and heat
	1. (TOA incident solar radiation) 필요 없을 수도?
5. other
	1. geopotential
	2. land-sea mask

[multi layer 딸깍딸깍](https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-pressure-levels?tab=form)
1. variables
	1. geopotential
	2. specific humidity
	3. temperature
	4. U-component of wind
	5. V-component of wind
	6. vertical velocity

# 필요한 features
- [x] geopotential_at_surface => single level에서 geopotential이 맞나? ㅇㅇ
- [x] 2m_temperature
- [x] geopotential
- [x] mean_sea_level_pressure
- [x] land_sea_mask
- [x] toa_incident_solar_radiation => 있긴 있는데 같은건가?
      이거 만들어주는 함수가 따로 있다. ![[data_utils.py#add_tisr_var]]

- [x] total_precipitation_6hr => 직접 합쳐야 함
      
- [x] 10m_v_component_of_wind
- [x] 10m_u_component_of_wind
- [x] temperature
- [x] u_component_of_wind
- [x] v_component_of_wind
- [x] vertical_velocity
- [x] specific_humidity

# e.g.
\
All Examples:   {'lon': 1440, 'lat': 721, 'level': 37, 'time': 14, 'batch': 1}

----------------------------------------------
Train Inputs:   {'batch': 1, 'time': 2, 'lat': 721, 'lon': 1440, 'level': 37}
Train Targets:  {'batch': 1, 'time': 10, 'lat': 721, 'lon': 1440, 'level': 37}
Train Forcings: {'batch': 1, 'time': 10, 'lat': 721, 'lon': 1440}

----------------------------------------------
Eval Inputs:    {'batch': 1, 'time': 2, 'lat': 721, 'lon': 1440, 'level': 37} var: 18개
Eval Targets:   {'batch': 1, 'time': 5, 'lat': 721, 'lon': 1440, 'level': 37} var: 11개
Eval Forcings:  {'batch': 1, 'time': 5, 'lat': 721, 'lon': 1440} var: 5개

18-11-5 = 2; static {'geopotential_at_surface', 'land_sea_mask'}



Data variables:
 - [x] u10      (time, latitude, longitude) float64 199MB ...
 - [x] v10      (time, latitude, longitude) float64 199MB ...
 - [x] t2m      (time, latitude, longitude) float64 199MB ...
 - [x] lsm      (time, latitude, longitude) float64 199MB ...
 - [x] msl      (time, latitude, longitude) float64 199MB ...
 - [x] tisr     (time, latitude, longitude) float64 199MB ...
 - [x] tp       (time, latitude, longitude) float64 199MB ... -> 합성 필요
 - [x] z        (time, level, latitude, longitude) float64 7GB ...
 - [x] q        (time, level, latitude, longitude) float64 7GB ...
 - [x] t        (time, level, latitude, longitude) float64 7GB ...
 - [x] u        (time, level, latitude, longitude) float64 7GB ...
 - [x] v        (time, level, latitude, longitude) float64 7GB ...
 - [x] w        (time, level, latitude, longitude) float64 7GB ...

Data variables:
 - [x] geopotential_at_surface       (lat, lon) float32 4MB ... -> 그냥 geopotential을 이름 바꿔서 넣어줫음
 - [x] land_sea_mask                 (lat, lon) float32 4MB ...
 - [x] 2m_temperature                (batch, time, lat, lon) float32 58MB ...
 - [x] mean_sea_level_pressure       (batch, time, lat, lon) float32 58MB ...
 - [x] 10m_v_component_of_wind       (batch, time, lat, lon) float32 58MB ...
 - [x] 10m_u_component_of_wind       (batch, time, lat, lon) float32 58MB ...
 - [x] total_precipitation_6hr       (batch, time, lat, lon) float32 58MB ...
 - [x] toa_incident_solar_radiation  (batch, time, lat, lon) float32 58MB ...
 - [x] temperature                   (batch, time, level, lat, lon) float32 2GB ...
 - [x] geopotential                  (batch, time, level, lat, lon) float32 2GB ...
 - [x] u_component_of_wind           (batch, time, level, lat, lon) float32 2GB ...
 - [x] v_component_of_wind           (batch, time, level, lat, lon) float32 2GB ...
 - [x] vertical_velocity             (batch, time, level, lat, lon) float32 2GB ...
 - [x] specific_humidity             (batch, time, level, lat, lon) float32 2GB ...