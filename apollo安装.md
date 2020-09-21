#### 安装git-lfs

`sudo apt-get install git-lfs `

apollo官方已经停用git-lfs，直接使用git即按可

#### Prerequisites

* A machine with a 8-core processor and 16GB memory minimum
* NVIDIA Turing GPU is strongly recommended
* Ubuntu 18.04
* NVIDIA driver version 440.33.01 and above ([Web link](https://www.nvidia.com/Download/index.aspx?lang=en-us))
* Docker-CE version 19.03 and above ([Official doc](https://docs.docker.com/engine/install/ubuntu/))
* NVIDIA Container Toolkit ([Official doc](https://github.com/NVIDIA/nvidia-docker))

**注：**因为需使用NVIDIA显卡，所以还需要安装CUDA，可以加速运算

##### CUDA的安装

##### NVIDIA显卡驱动的安装

* ```
  sudo add-apt-repository ppa:graphics-drivers/ppa
  sudo apt update
  sudo ubuntu-drivers autoinstall || sudo apt install nvidia-410
  ```

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





