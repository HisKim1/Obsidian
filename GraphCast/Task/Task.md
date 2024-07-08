```ad-todo
예측을 대부분 대기 하부를 기준으로 비교했던데, 대기 상층부의 이벤트도 잘 잡힐까?
e.g. [[rossby wave]]를 잡을 수 있을까? / AO는 period가 너무 길다. 
또 대기 상층부에 있는 이벤트가 뭐가 있지
```

### Dataset의 dim., var., prop.s
어떤 dataset을 준비해야 하나

```ad-note
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

---
4. Properties
   resolution=0.25, 
   mesh_size=6, 
   latent_size=512, 
   gnn_msg_steps=16, 
   hidden_layers=1,
   radius_query_fraction_edge_length=0.5999912857713345,
   mesh2grid_edge_normalization_factor=0.6180338738074472
	   
```


e.g. 
```

```