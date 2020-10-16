#### 安装git-lfs

`sudo apt-get install git-lfs `

*注：apollo官方已经停用git-lfs，直接使用git即按可*

#### Prerequisites

* A machine with a 8-core processor and 16GB memory minimum
* NVIDIA Turing GPU is strongly recommended
* Ubuntu 18.04
* NVIDIA driver version 440.33.01 and above ([Web link](https://www.nvidia.com/Download/index.aspx?lang=en-us))
* Docker-CE version 19.03 and above ([Official doc](https://docs.docker.com/engine/install/ubuntu/))
* NVIDIA Container Toolkit ([Official doc](https://github.com/NVIDIA/nvidia-docker))

**注：**因为需使用NVIDIA显卡，所以还需要安装CUDA，可以加速运算

##### CUDA的安装

* 下载cuda （所有版本的cuda下载地址为：https://developer.nvidia.com/cuda-toolkit-archive）

* sudo chmod +x cuda_10.1.168_418.67_linux.run 

* sudo sh cuda_10.1.168_418.67_linux.run 

* 如果已经安装了N卡，则不选择安装N卡

* 环境设置

  ```
  # NVIDIA CUDA Toolkit
  export PATH=/usr/local/cuda-10.1/bin:$PATH
  export LD_LIBRARY_PATH=/usr/local/cuda-10.1/lib64
  
  source ~/.bashrc
  nvcc -V
  
  ```
  
* 查看cuda版本

    `cat /usr/local/cuda/version.txt` 
##### NVIDIA显卡驱动的安装

  ```
  sudo add-apt-repository ppa:graphics-drivers/ppa
  sudo apt update
  sudo ubuntu-drivers autoinstall || sudo apt install nvidia-410
  
  
  sudo apt-get update
  sudo apt-add-repository multiverse
  sudo apt-get update
  sudo apt-get install nvidia-driver-440
  ```

  

##### NVIDIA显卡驱动的卸载

     sudo apt-get remove --purge nvidia*
     sudo apt-get autoremove
##### Docker-CE安装

`https://docs.docker.com/engine/install/ubuntu/`

```c
sudo apt-get remove docker docker-engine docker.io containerd runc //卸载之前的docker
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common    
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -    //添加GPG密匙
sudo apt-key fingerprint 0EBFCD88   //通过搜索指纹的后8个字符，验证您现在是否拥有带有指纹的密钥
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io  //安装docker引擎
```

##### NVIDIA container Toolkit 安装

`https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker`

```
#添加源
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

#安装并重启docker
sudo apt update && sudo apt install -y nvidia-container-toolkit
sudo systemctl restart docker

# 在官方CUDA镜像上测试 nvidia-smi
sudo docker run --gpus all nvidia/cuda:9.0-base nvidia-smi
# 启动支持双GPU的容器
sudo docker run --gpus 2 nvidia/cuda:9.0-base nvidia-smi
# 指定GPU 1，运行容器
sudo docker run --gpus device=0 nvidia/cuda:9.0-base nvidia-smi


#安装了nvidia-container-runtime
sudo apt-get install nvidia-container-runtime
```

##### 使用apollo自带的脚本安装docker

<font color=Blue>***原因：docker源码安装后需要创建组，进而获取不使用root进入docker的权限，apollo脚本中已经做好这步了***</font> 

`bash docker/setup_host/install_docker.sh`

`bash docker/setup_host/install_nvidia_docker.sh`

![image-20200928220048981](../../.config/Typora/typora-user-images/image-20200928220048981.png)



##### 卸载docker

```
sudo apt-get purge docker-ce docker-ce-cli containerd.io
sudo rm -rf /var/lib/docker
```

#### 下载apollo源码

```
git clone https://github.com/ApolloAuto/apollo.git
```

#### 环境配置

```
cd apollo
git checkout master

echo "export APOLLO_ROOT_DIR=$(pwd)" >> ~/.bashrc  && source ~/.bashrc
```

#### 在docker中编译apollo

```
bash docker/scripts/dev_start.sh
```

#### 进入apollo容器

```
bash docker/scripts/dev_into.sh
```

#### 编译apollo

```bash
#CPU
./apollo.sh build   

#GPU
/apollo.sh build_gpu

#在编译之前，检查环境是否正确
whereis nvidia
cat /usr/local/cuda/version.txt
dpkg -l | grep libcudnn7
cat /usr/include/cudnn.h | grep CUDNN_MAJOR -A 2
```

#### 测试apollo

##### 测试CPU版本的apollo

```shell
#https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_launch_Apollo.md
#1.加载环境变量
source /apollo/scripts/apollo_base.sh

#2.启动组件
bash /apollo/scripts/bootstrap.sh

#3.登录dreamview
http://localhost:8888/

#4.下载demo record
cd docs/demo_guide/
python3 rosbag_helper.py demo_3.5.record
cyber_recorder play -f docs/demo_guide/demo_3.5.record -loop
```

##### 测试GPU版本的apollo

```bash
#可执行一个Demo检查是否成功编译GPU版本的APOLLO
./bazel-bin/modules/perception/camera/test/camera_lib_obstacle_detector_yolo_region_output_test

#或者直接运行所有测试
./apollo.sh test
```



#### 遇到问题

1. Failed to pull docker image : apolloauto/apollo:dev-x86_64-18.04-20200914_0742

   解决： sudo chmod 777 /var/run/docker.sock 
   
2. Error response from daemon: Get https://registry-1.docker.io/v2/: dial tcp: lookup registry-1.docker.io on 8.8.8.8:53: write udp 10.10.1.25:60596->8.8.8.8:53: write: operation not permitted

   解决：
   
3. N卡版本过低

   ![image-20200928200824390](../../.config/Typora/typora-user-images/image-20200928200824390.png)





