## Install tensorflow-gpu (ubuntu16.04)

> 설치 환경
> NVIDIA 드라이버 설치   
> CUDA 설치  
> cuDNN 설치  
> tensorflow-gpu 설치  


### 설치 환경  
이 문서는 아래와 같은 환경 기준입니다.
  
|  |  |  
|--|--|  
| OS | ubuntu16.04 |  
| GPU | NVIDIA Geforce GTX 1060 |  
| python | 3.7.1 |  

** Initial checks **  
GPU device

    lspci | grep -i nvidia  

Linux version  

    uname -m && cat /etc/*release | head -n0  

GCC  

    gcc --version  


###  NVIDIA 드라이버 설치  

드라이버가 설치 되었는지 확인  


설치 되지 않았다면,  

ctrl + alt + f1 을 눌러서 콘솔모드로 이동
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgzMDg4OTUyNV19
-->