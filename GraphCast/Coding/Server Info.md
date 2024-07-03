### OS version
```
(hiskim1_3.11) [root@forecast1 graphcast]# cat /proc/version
Linux version 4.18.0-348.el8.x86_64 (mockbuild@kbuilder.bsys.centos.org) (gcc version 8.5.0 20210514 (Red Hat 8.5.0-3) (GCC)) #1 SMP Tue Oct 19 15:14:17 UTC 2021
```

### OS type
```
(hiskim1_3.11) [root@forecast1 graphcast]# rpm -qa | grep release
centos-linux-release-8.5-1.2111.el8.noarch
epel-release-8-19.el8.noarch
```
### GPU
```
(hiskim1_3.11) [root@forecast1 graphcast]# nvidia-smi
Tue Jul  2 17:11:46 2024       
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