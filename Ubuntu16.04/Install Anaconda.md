### install Anaconda  
download "Anaconda3-2018.12-Linux-x86_64.sh" at https://www.anaconda.com/distribution/  
![
](https://lh3.googleusercontent.com/1kuoUZg4YUMQ1Da8jG4DelSpeE0udbP-ZWjeAK7bC6saLP0qZzYPXfywi3lY0SJep5V4kCqb1FI "download_anaconda")

    $bash /다운로드 경로/Anaconda3-2018.12-Linux-x86_64.sh  
![
](https://lh3.googleusercontent.com/IiB6GVCRHOq1NUCn4Vu-ZPsoBs8COtdwQCvWO-n_iczIj8nut3GEkI-8Y9Rw2FnBMBdgSmQOxCs "installanaconda")

    $export PATH=/root/anaconda3/bin:$PATH
    $source ~/.bashrc

#### ​Anaconda 명령어 (가상환경 생성)  
새로운 가상 환경 생성  

    # 기본 명령어  
    $conda create -n name(원하는 환경이름)  ​  
    # python 버전 지정  
    $conda create -n name python=3.7 anaconda   
    

아래 화면 나오면 y  
![
](https://lh3.googleusercontent.com/Hdv-wH7KxNf-49xQmOs-eniTJX6koKBNhVwSEqVcS1YU1B8AMXaotOqerK7TY0RCJcywHo9jLRQ "create")

가상환경 활성화  

    $source activate 가상환경이름

가상환경 비활성화  

    $deactivate  

가상환경 목록 확인  

    $conda info --envs  

가상환경 삭제  

    $conda remove -n 가상환경이름 --all  
(--all :가상환경에 설치했던 패키지까지 모두 삭제)  

가상환경 복제  

    $conda create --name "원본 가상환경 이름" --clone "새로운 가상환경 이름"  

이미 생성한 가상환경에 추가로 패키지 설치  

    $conda install -n "가상환경 이름" numpy  



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM5MzMyMTg0MF19
-->