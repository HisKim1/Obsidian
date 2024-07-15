---
presenter: Micheal Ek, NCAR
session: session 1
---
# Objects
Improve land-atm interaction via improvements to the land & hydrology compoents in Earth sys models

# Land Model: provieds flux boundary cond.
- surface energy budget
  : surface albedo & emissivity?에 영향
- surface water budget
  : terrestrial surface change한다

# Noah-MP Land Model
Canopy / snow / soil / groundwater / ... 등 다양한 process 어쩌잔거지

# WRF -Hydro Community Model
SOTA land surface physics 적용

# Noah-MP + WRF-Hydro in NOAA global model
NOAA에서 진행하는 첫번째 ??? proj.!

# Local Land-Atm. Interaction and Coupling
model에 잘 반영하려면 좋은 system이 있어야 하는데, 많은 proc가 서로 interact하고 있다
![[20240715_143252.jpg]]

# Land-Atmosphere Interaction: Terrestrial Leg

# Land-Atmosphere Interaction: Atmospheric Leg
dry soil / strong inversion -> shallow ABL, no clouds
dry soil

| soil | inversion | Atm Boundary layer | cloud |
| ---- | --------- | ------------------ | ----- |
| dry  | strong    | shallow            | no    |
| dry  | weak      |                    | yes   |
| wet  | ?         | ??                 |       |
# Summary
ESM은 복잡하다 w/ many proc & interactions
ESM을 위해서는 적절한 proc가 필요
ESM에서 land-atm interaction을 적절히 표현하기 위해서는 land & hydrological process의 적절한 respresentation이 필요하다??
# References
Land-Atmosephere Interactions: The LoCo Perspective, Joseph A., etc.