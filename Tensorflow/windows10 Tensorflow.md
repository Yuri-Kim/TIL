## Install tensorflow (windows10)

> 설치 환경  
>  Anaconda 설치
> tensorflow 설치  


### 설치 환경  
이 문서는 아래와 같은 환경 기준입니다.
  
|  |  |  
|--|--|  
| OS | windows10 |  
| python | 3.7.0 |  

### Anaconda 설치  

공식 홈페이지에서 'Anaconda 2018.12 for Windows Installer (Python 3.7 version)' 다운로드 후 설치 https://www.anaconda.com/distribution/  

#### ​Anaconda 명령어 (가상환경 생성)  
가상환경 생성  

    conda create -n env_name python=3.6 

가상환경 활성화  
windows    

    activate env_name  

Linux, OsX   

    source activate env_name  

가상환경 비활성화  
windows  

    deactivate  

Linux, OsX  

    source deactivate    

### Tensorflow 설치  

    conda install tensorflow==1.12.0  


matplotlib 설치  

    conda install matplotlib  


### 구동 확인  

    $python
    >>>import tensorflow as tf   
    >>>tf.__version__  


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5OTIwMzg5NTMsMTkzMzU3NDEyOV19
-->