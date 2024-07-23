# TODO
`start_time`이 `2022-02-02T00:00:00`이 아니라면 함수 수정 필요

```python
def create_forcing_dataset(time_steps, resolution, start_time):
    lon = np.arange(0.0, 360.0, resolution, dtype=np.float32)
    lat = np.arange(-90.0, 90.0 + resolution/2, resolution, dtype=np.float32)

	start_datetime = pd.to_datetime(start_time) + pd.Timedelta(hours=12)
    datetime = pd.date_range(start=start_datetime, periods=time_steps, freq='6h')
    time = pd.timedelta_range(start='12h', periods=time_steps, freq='6h')

    # Create the dataset
    ds = xr.Dataset(
        coords={
            'lon': ('lon', lon),
            'lat': ('lat', lat),
            'datetime': ('datetime', datetime),
            'time': ('time', time)
        }
    )

    ds.lat.attrs['long_name'] = 'latitude'
    ds.lat.attrs['units'] = 'degrees_north'
    ds.lon.attrs['long_name'] = 'longitude'
    ds.lon.attrs['units'] = 'degrees_east'

    variables = ['toa_incident_solar_radiation',
                 'year_progress_sin',
                 'year_progress_cos',
                 'day_progress_sin',
                 'day_progress_cos']

    data_utils.add_derived_vars(ds)
    data_utils.add_tisr_var(ds)

     # `datetime` is needed by add_derived_vars but breaks autoregressive rollouts.
    ds = ds.drop_vars("datetime")
    ds = ds[list(variables)]

    # 각 변수에 'batch' 차원 추가
    for var in variables:
        # 현재 변수의 차원과 데이터 가져오기
        current_dims = ds[var].dims
        current_data = ds[var].values

        # 'batch' 차원을 추가한 새로운 데이터 배열 생성
        new_shape = (1,) + current_data.shape
        new_data = np.zeros(new_shape, dtype=current_data.dtype)
        new_data[0] = current_data

        # 새로운 차원 순서 정의 ('batch'를 첫 번째로)
        new_dims = ('batch',) + current_dims
        # 새로운 DataArray 생성 및 할당 (coordinate는 추가하지 않음)
        ds[var] = xr.DataArray(
            data=new_data,
            dims=new_dims,
            # 'batch'는 coordinate에 포함하지 않음
            coords={dim: ds[dim] for dim in current_dims}  
        )
    return ds
```

