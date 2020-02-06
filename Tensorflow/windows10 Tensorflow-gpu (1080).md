
## Install tensorflow-gpu (windows10)

> 설치 환경  
> Visual Studio C++ 컴파일러 설치  
> CUDA 설치  
> CuDNN 설치  
> tensorflow-gpu 설치  


### 설치 환경  
이 문서는 아래와 같은 환경 기준입니다.
  
|  |  |  
|--|--|  
| OS | windows10 |  
| GPU | NVIDIA Geforce GTX 1080 8GB |  
| python | 3.6.8 |  

### Visual Studio C++ 컴파일러 설치  

[여기서](https://support.microsoft.com/ko-kr/help/2977003/the-latest-supported-visual-c-downloads) Visual C++ 2017 다운로드 및 설치  

### CUDA 설치  
[여기서](https://developer.nvidia.com/cuda-10.0-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exenetwork) CUDA 10.0 다운로드 및 설치  
![enter image description here](https://lh3.googleusercontent.com/Qahox58kI75WEN5MbtmTalsL1XHrfhW_DqDfS4BdZ3HtW-ncr6RhDY98dmOWYaa2Vgrc5OtyYg72 "1")  
(설치할 때 화면이 깜빡일 수 있음)  

환경 변수 설정  
사용자 변수 - Path에 아래 내용 추가  

    C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\bin   

### CuDNN 설치  
[여기서](https://developer.nvidia.com/rdp/cudnn-download) 버전 맞춰 다운로드 후 압축 해제 (회원가입 필요)    
![
](https://lh3.googleusercontent.com/pYk7TJYEHboUkVpX0jnZDKSXE2BK1DpD5t3Jp2-4yB_FHsDLimRlfcj7pTvYExPF1HVChGf5uTZE "wingqu1")  
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0 에 파일 복사 붙여넣기    

### tensorflow-gpu 설치  
anaconda prompt로 들어가서 업데이트  

    conda update conda  
    conda update --all  

새로운 Anaconda 환경 생성  

    conda create -n tensorgpu pip python=3.6  
    conda activate tensorgpu  

tensorflow-gpu (1.13.1) 설치  

    pip install --ignore-installed --upgrade tensorflow-gpu  

설치 확인  

    python -c "import tensorflow as tf; print(tf.__version__)"  

![
](https://lh3.googleusercontent.com/h6hNMlLXiu1diuILVFykk5kP4coOvpDXnRKRqvwus_0ATyIbCjelE35n0-6hSZtW4vNeUf0rB6EC "gpu")  

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg5MjY3OTU5M119
-->