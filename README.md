# GAEA-net-Determined-AI-set-up
This is a guide for instaling GAEA-net on Determined AI server.
## Step 1: Launch Cuda9.2-CuDNN7 instance (2GPU)
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
## Step 2: Install git, vim, wget, etc.
```
$ apt update
$ apt install -y git vim wget zip unzip
```
## Step 3: Install Anaconda
```
$ wget https://repo.anaconda.com/archive/Anaconda3-2021.11-Linux-x86_64.
sh
$ sh ./Anaconda3-2021.11-Linux-x86_64.sh
```
## Step 4: Create new conda environment
```
$ source ~/.bashrc
$ conda create -n {env_name} python=3.6
$ conda activate {env_name}
```
## Step 5: Install tensorflow 1.12.0
```
conda install tensorflow-gpu=1.12.0
```
## Step 6: Install pdal 1.7
Install pdal as a conda environment ( https://anaconda.org/conda-forge/pdal )
```
conda install -c conda-forge/label/cf202003 pdal=1.7
```
## Step 7: Install laspy and sklearn
```
pip install laspy==1.7 sklearn
```
## Step 8: Clone source code
### what I changed on the source code
I’ve changed shell scripts in the tf_ops refering to the links below.

https://www.codeleading.com/article/90214640128/

https://github.com/charlesq34/pointnet2/issues/48#issuecomment-404482115

I’ve changed the gpu numbers in train_multi_gpu_deep.py and train_multi_gpu.py
```
os.environ["CUDA_VISIBLE_DEVICES"] = "0,1"
```
```
$ git clone https://github.com/iskra3138/GADH_Net_EA.git
```
## Step 9: Compile and install pointnet2 & PointSIFT tensorflow utilities
```
$ cd ./GADH_Net_EA/tf_ops/3d_interpolation
$ sh ./tf_interpolate_compile_py3.sh
$ cd ../grouping
$ sh ./tf_grouping_compile_py3.sh
$ cd ../sampling
$ sh ./tf_sampling_compile_py3.sh
$ cd ../pointSIFT_op
$ sh ./tf_pointSIFT_compile_py3.sh
```
# Run GAEA-net from Docker Image
This is a guide for launching GADH_Net_EA image on DeterminedAI Server.
Everything in scratch version is pre-installed.
This image is ausmlab/gadh_net_ea:determinedai
## Step 1: Launch Instance
This is a sample config of using 2GPUs
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
ausmlab/gadh_net_ea:determinedai
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
## Step 2: Activate environment where what we need is installed
```
$ conda activate gadh
$ cd /nas2/zhen/pointnet2
$ sh train.sh
```
```
```
```
```
```
```
