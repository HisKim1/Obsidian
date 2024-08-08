# Basic Info
- Based on [[@S. Rasp, et. al., 2024]]
- [Official Github](https://github.com/google-research/weatherbench2)

# Initiation Process
###  1. git clone
[My forked Github](https://github.com/HisKim1/his_weatherbench2)
forecast1 서버로 이사 완료
### 2. conda env. setting
[installation](https://weatherbench2.readthedocs.io/en/latest/index.html) 따라서 설치 진행해야 함.
`hiskim1_weatherbench2` conda 환경 새로 만들어서 진행하는 게 좋을 듯
-> 설치 완료 | `python setup.py install`도 같이 해줌
jax 해결 필요 없을 듯? 
﻿```shell
﻿conda remove jax
﻿conda install jax
pip install https://storage.googleapis.com/jax-releases/cuda12_plugin/jax_cuda12_plugin-0.4.23-cp311-cp311-manylinux2014_x86_64.whl
```
### 3. run [Quickstart](https://weatherbench2.readthedocs.io/en/latest/evaluation.html)
`his_weatherbench2/docs/source/evaluation.ipynb`와 동일한 파일임.
-> 잘 돌아감 2024-08-08 15:31
### 4. understand Usage & API

### 5. check important functions
