```python
def create_target_dataset(time_steps, resolution, pressure_levels):
    # Define coordinates
    lon = np.arange(0.0, 360.0, resolution, dtype=np.float32)
    lat = np.arange(-90.0, 90.0 + resolution/2, resolution, dtype=np.float32)
    if pressure_levels == 37:
        level = [   1,    2,    3,    5,    7,   10,   20,   30,   50,   70,  100,  125, 150,  175,  200,  225,  250,  300,  350,  400,  450,  500,  550,  600, 650,  700,  750,  775,  800,  825,  850,  875,  900,  925,  950,  975, 1000]
    elif pressure_levels == 13:
        level = [50, 100, 150, 200, 250, 300, 400, 500, 600, 700, 850, 925, 1000]
    else:
        raise ValueError("Unsupported number of pressure levels. Choose either 37 or 13.")

    level = np.array(level, dtype=np.int64)
    
    # 시작 시간부터 time_steps 개의 6시간 간격 타임델타 생성
    time = pd.timedelta_range(start='6h', periods=time_steps, freq='6h')

    # timedelta64[ns]로 명시적 변환
    # time = time.astype('timedelta64[ns]')/

    # Create the dataset
    ds = xr.Dataset(
        coords={
            'lon': ('lon', lon),
            'lat': ('lat', lat),
            'level': ('level', level.astype(np.int32)),
            'time': ('time', time),
        }
    )

    ds.lat.attrs['long_name'] = 'latitude'
    ds.lat.attrs['units'] = 'degrees_north'
  
    ds.lon.attrs['long_name'] = 'longitude'
    ds.lon.attrs['units'] = 'degrees_east'

    # Add data variables filled with NaN
    surface_vars = ['2m_temperature', 'mean_sea_level_pressure', '10m_v_component_of_wind',
                    '10m_u_component_of_wind', 'total_precipitation_6hr']
    level_vars = ['temperature', 'geopotential', 'u_component_of_wind',
                  'v_component_of_wind', 'vertical_velocity', 'specific_humidity']

    for var in surface_vars:
        ds[var] = xr.DataArray(
            data=np.full((1, time_steps, len(lat), len(lon)), np.nan, dtype=np.float32),
            dims=['batch', 'time', 'lat', 'lon']
        )
    
    for var in level_vars:
        ds[var] = xr.DataArray(
            data=np.full((1, time_steps, len(level), len(lat), len(lon)), np.nan, dtype=np.float32),
            dims=['batch', 'time', 'level', 'lat', 'lon'],
        )
    ds = ds.transpose("batch", "time", "lat", "lon", ...)

    return ds
```