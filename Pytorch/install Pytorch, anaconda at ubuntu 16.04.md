## Install Pytorch ubuntu 16.04

ubuntu16.04에 기본적으로 설치되어 있는 python version
![
](https://lh3.googleusercontent.com/D-Ep4i_UMM3cOrm_KVmeyIMkzT_tJ_0V9e8BrZpIgTwftJ19KN32x7_eOa2yBWX_WDmb0OCfTu8 "python_version")

#### install python3.7 at ubuntu 16.04
download Python-3.7.2.tar.xz at [https://www.python.org/downloads/](https://www.python.org/downloads/)

    $cd /다운로드 받은 폴더 경로/
    $tar -xvf Python-3.7.2.tar.xz
    $cd Python-3.7.2
    $./configure
    $sudo make
    $​sudo make install

만약 아래와 같은 오류가 난다면,
![
](https://lh3.googleusercontent.com/wbjcaEZGhjBxmHc4_jpR2yjsDMFn5ug6J6MNxfholc0I9fUXmVZMDB4rzeDHEZ_u2Xq0MMu8xbs "ZipImportError")

    $sudo apt-get install zlib1g-dev
    $sudo make install

#### install Anaconda

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYwMDE2NzgyNywtMTY4NTIzMTEwMCwtMT
cwMzM0MzA0M119
-->