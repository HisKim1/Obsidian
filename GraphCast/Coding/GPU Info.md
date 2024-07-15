```
(hiskim1_3.11) [root@forecast1 hiskim1]# nvidia-smi
Wed Jul  3 14:20:14 2024
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 510.108.03   Driver Version: 510.108.03   CUDA Version: 11.6     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla V100-PCIE...  Off  | 00000000:3B:00.0 Off |                    0 |
| N/A   48C    P0    28W / 250W |      4MiB / 32768MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  Tesla V100-PCIE...  Off  | 00000000:D9:00.0 Off |                    0 |
| N/A   46C    P0    28W / 250W |      4MiB / 32768MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      7945      G   /usr/libexec/Xorg                   4MiB |
|    1   N/A  N/A      7945      G   /usr/libexec/Xorg                   4MiB |
+-----------------------------------------------------------------------------+
```

```
(hiskim1_3.11) [root@forecast1 hiskim1]# nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2021 NVIDIA Corporation
Built on Fri_Dec_17_18:16:03_PST_2021
Cuda compilation tools, release 11.6, V11.6.55
Build cuda_11.6.r11.6/compiler.30794723_0
```

```
(hiskim1_3.11) [root@forecast1 hiskim1]# uname -a
Linux forecast1 4.18.0-348.el8.x86_64 #1 SMP Tue Oct 19 15:14:17 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
```

```
(hiskim1_3.11) [root@forecast1 hiskim1]# conda list | grep -E "cuda|cudnn|jax"
cuda-python               11.8.3          py311h2c6edaf_2    conda-forge
cuda-version              11.6                 hca96458_3    conda-forge
cudatoolkit               11.6.2              hfc3e2af_13    conda-forge
jax                       0.4.30                   pypi_0    pypi
jaxlib                    0.4.30                   pypi_0    pypi
```

#Question 
### [jax 라이브러리](https://storage.googleapis.com/jax-releases/jax_cuda_releases.html)가 GPU 인식을 못 한다.
##### + jax version이 계속 변한다
used conda environment
1. hiskim1_3.11
2. hiskim2_3.11
```
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep -E "cuda|cudnn|jax"
cuda-version              11.8                 h70ddcb2_3    conda-forge
cudatoolkit               11.8.0              h4ba93d1_13    conda-forge
cudnn                     8.9.7.29             hbc23b4c_3    conda-forge
jax                       0.4.10                   pypi_0    pypi
jaxlib                    0.4.30                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep -E "cuda|cudnn|jax"
cuda-version              11.8                 h70ddcb2_3    conda-forge
cudatoolkit               11.8.0              h4ba93d1_13    conda-forge
cudnn                     8.9.7.29             hbc23b4c_3    conda-forge
jax                       0.4.10                   pypi_0    pypi
jaxlib                    0.4.10                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep -E "cuda|cudnn|jax"
cuda-version              11.8                 h70ddcb2_3    conda-forge
cudatoolkit               11.8.0              h4ba93d1_13    conda-forge
cudnn                     8.9.7.29             hbc23b4c_3    conda-forge
jax                       0.4.10                   pypi_0    pypi
jaxlib                    0.4.30                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep -E "cuda|cudnn|jax"
cuda-version              11.8                 h70ddcb2_3    conda-forge
cudatoolkit               11.8.0              h4ba93d1_13    conda-forge
cudnn                     8.9.7.29             hbc23b4c_3    conda-forge
jax                       0.4.10                   pypi_0    pypi
jaxlib                    0.4.30                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep -E "cuda|cudnn|jax"
cuda-version              11.8                 h70ddcb2_3    conda-forge
cudatoolkit               11.8.0              h4ba93d1_13    conda-forge
cudnn                     8.9.7.29             hbc23b4c_3    conda-forge
jax                       0.4.10                   pypi_0    pypi
jaxlib                    0.4.30                   pypi_0    pypi
```

```
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep jax
jax                       0.4.30                   pypi_0    pypi
jaxlib                    0.4.30                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep jax
jax                       0.4.30                   pypi_0    pypi
jaxlib                    0.4.30                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep jax
jax                       0.4.10                   pypi_0    pypi
jaxlib                    0.4.10                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep jax
jax                       0.4.10                   pypi_0    pypi
jaxlib                    0.4.10                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep jax
jax                       0.4.30                   pypi_0    pypi
jaxlib                    0.4.10                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep jax
jax                       0.4.30                   pypi_0    pypi
jaxlib                    0.4.10                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep jax
jax                       0.4.10                   pypi_0    pypi
jaxlib                    0.4.10                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep jax
jax                       0.4.10                   pypi_0    pypi
jaxlib                    0.4.10                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep jax
jax                       0.4.30                   pypi_0    pypi
jaxlib                    0.4.30                   pypi_0    pypi
(hiskim2_3.11) [hiskim1@forecast1 ~]$ conda list | grep jax
jax                       0.4.30                   pypi_0    pypi
jaxlib                    0.4.30                   pypi_0    pypi
```

**/home/hiskim1/jaxtest.py**
```python
import jax

print(jax.devices())
```

**output**
```
(hiskim1_3.11) [hiskim1@forecast1 ~]$ python jaxtest.py
An NVIDIA GPU may be present on this machine, but a CUDA-enabled jaxlib is not installed. Falling back to cpu.
[CpuDevice(id=0)]
```

**해결 방안**
1. ~~jax 버전 조절
   [설치가능한 jax](https://storage.googleapis.com/jax-releases/jax_cuda_releases.html)
   우리가 갖고 있는 cuda 11.6에 cudnn 8.9랑 딱 맞는 jax가 없긴 함
   안 됨.~~
   
2. ~~cudnn 버전 조절~~

3. CUDA version 업그레이드 10일 오전 10시 예정
   #WorkingOn 