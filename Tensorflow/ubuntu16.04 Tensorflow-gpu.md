
## Install tensorflow-gpu (ubuntu16.04)

> 설치 환경  
> Anaconda 가상환경 생성  
> CUDA 설치  
> cuDNN 설치  
> tensorflow-gpu 설치  


### 설치 환경  
이 문서는 아래와 같은 환경 기준입니다.
  
|  |  |  
|--|--|  
| OS | ubuntu16.04 |  
| GPU | NVIDIA Geforce GTX 1060 |  
| envs | Anaconda |  


** Initial checks **  
GPU device

    lspci | grep -i nvidia  

Linux version  

    uname -m && cat /etc/*release | head -n0  

GCC  

    gcc --version  

### Anaconda 가상환경 생성  


###  CUDA 설치  
[여기](https://developer.nvidia.com/cuda-10.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=debnetwork)서 10.0 download  

![
](https://lh3.googleusercontent.com/_RE4hfRwfzQIe9uiN9mtA4ijY92HTbl8b3SqmCX7eeoi-5nhEcPmsZVjB-nbVR_iYh5WHI31arT6 "cuda")  

위 사진과 같이 다운로드 후 아래 명령어 실행  

    $ sudo dpkg -i cuda-repo-ubuntu1604_10.0.130-1_amd64.deb  
    $ sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub  
    $ sudo apt-get update  
    $ sudo apt-get install cuda  


### cuDNN 설치  
[여기](https://developer.nvidia.com/rdp/cudnn-download)서 다운받은 CUDA 버전에 맞춰 'cuDNN Library for Linux' 다운로드 후 아래 명령어 실행  

    $ tar xvfz cudnn-10.0-linux-x64-v7.6.1.34.tgz  
    $ sudo cp -P cuda/include/cudnn.h /usr/local/cuda/include  
    $ sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda/lib64  
    $ sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*  

추가 dependencies 설치  

    $ sudo apt-get install libcupti-dev  

**환경변수 설정**  

    vi ~/.bashrc export  
    PATH=/usr/local/cuda/bin:$PATH  
    export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64"  
    export CUDA_HOME=/usr/local/cuda  

**버전 확인**  
 

    $ nvcc --version  

### Tensorflow-gpu 설치  

    $ sudo apt-get install python3-pip python3-dev  
    $ pip3 install tensorflow-gpu  

### 설치 확인  

    $ python3 -c "import tensorflow as tf; print(tf.__version__)"  




<!--stackedit_data:
eyJoaXN0b3J5IjpbNjM4NTczMDQwLC0xMDYyOTYzODM0LC04Mz
A4ODk1MjVdfQ==
-->