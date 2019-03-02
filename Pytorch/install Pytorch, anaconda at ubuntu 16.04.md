## Install Pytorch ubuntu 16.04

ubuntu16.04에 기본적으로 설치되어 있는 python version
![
](https://lh3.googleusercontent.com/D-Ep4i_UMM3cOrm_KVmeyIMkzT_tJ_0V9e8BrZpIgTwftJ19KN32x7_eOa2yBWX_WDmb0OCfTu8 "python_version")

### install python3.7 at ubuntu 16.04
download "Python-3.7.2.tar.xz" at [https://www.python.org/downloads/](https://www.python.org/downloads/)

    $cd /다운로드 받은 폴더 경로/
    $tar -xvf Python-3.7.2.tar.xz
    $cd Python-3.7.2
    $./configure
    $sudo make
    $​sudo make install

ZipImpotError 발생시
![
](https://lh3.googleusercontent.com/wbjcaEZGhjBxmHc4_jpR2yjsDMFn5ug6J6MNxfholc0I9fUXmVZMDB4rzeDHEZ_u2Xq0MMu8xbs "ZipImportError")

    $sudo apt-get install zlib1g-dev

No module named 'ctypes' 에러 발생시
![
](https://lh3.googleusercontent.com/TXBIDcm2i_5YSDpX7LyRl8g1cjyHHlC2nLQXEvlbPIxjo0MswYmM816WJIPsTzzbZNw06yV58Fw "ModuleNotFoundError")

    $sudo apt-get install libffi-dev

위의 오류 모두 해결 후 다시

    $​sudo make install  


### install Anaconda
download "Anaconda3-2018.12-Linux-x86_64.sh" at https://www.anaconda.com/distribution/
![
](https://lh3.googleusercontent.com/1kuoUZg4YUMQ1Da8jG4DelSpeE0udbP-ZWjeAK7bC6saLP0qZzYPXfywi3lY0SJep5V4kCqb1FI "download_anaconda")

    $bash /다운로드 경로/Anaconda3-2018.12-Linux-x86_64.sh
![
](https://lh3.googleusercontent.com/IiB6GVCRHOq1NUCn4Vu-ZPsoBs8COtdwQCvWO-n_iczIj8nut3GEkI-8Y9Rw2FnBMBdgSmQOxCs "installanaconda")

    $export PATH=/root/anaconda3/bin:$PATH
    $source ~/.bashrc

### ​Python 환경 설치
새로운 환경 생성
`$ conda create -n pylesson(원하는 환경이름)`​

아래 화면 나오면 y
![
](https://lh3.googleusercontent.com/Hdv-wH7KxNf-49xQmOs-eniTJX6koKBNhVwSEqVcS1YU1B8AMXaotOqerK7TY0RCJcywHo9jLRQ "create")

새로 생성한 환경 활성화

    $source activate 환경이름

### Install Pytorch

    $conda install pytorch torchvision -c pytorch


관련 라이브러리 설치

    $conda install jupyter # 개발 환경 기능 제공
    $conda install pillow # 이미지 처리 함수 제공
    $conda install matplotlib # 그래프 작성용 함수 제공
    $conda install pandas # 데이터 다루는 함수 제공
    
$ conda install scikit-learn # 머신러닝 관련 함수 제공

$ pip install konlpy # 자연어 처리 함수 제공
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU4NDMzMTIzMCwtMTY4NTIzMTEwMCwtMT
cwMzM0MzA0M119
-->