## GAEA-net-Determined-AI-set-up
This is a guide for instaling GAEA-net on Determined AI server.
# Step 1: Launch Cuda9.2-CuDNN7 instance (2GPU)
```
bind_mounts:
- container_path: /nas2 #path name in container
host_path: /mnt/nfs/synology
debug: false
description: My_Container # Name of container
entrypoint: null
environment:
add_capabilities: null
drop_capabilities: null
environment_variables: {}
force_pull_image: false
image:
cpu: >-
determinedai/environments:py-3.8-pytorch-1.9-lightning-1.3-tf-2.4-
cpu-9f0cb26
cuda: >-
iskra3138/cuda9:9.2-base-gpu-825e8ee
rocm: determinedai/environments:rocm-4.2-pytorch-1.9-tf-2.5-rocm-
9f0cb26
pod_spec: null
ports: null
registry_auth:
password: 22429dae-cc82-4bdf-81e7-5c35252ac1ca
username: afnanahmad
idle_timeout: null
notebook_idle_type: kernels_or_terminals
resources:
agent_label: ''
devices: null
resource_pool: default
slots: 2 # num of GPUs that you want
weight: 1
work_dir: /nas2 # default path on container
```
```
```
```
```
```
```
```
```
