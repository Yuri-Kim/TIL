## Python 버전 관리  

-   Ubuntu16.04에는 기본적으로 python path가 2.7 버전으로 설정되어 있음  
-   Linux의 alternative를 이용하여 python 버전을 쉽게 변경 및 관리 가능  
-   Python은  `/usr/bin/python`의 link 파일이고, 이 파일은  `/usr/bin/python2.7`의 link 파일  
- `/usr/bin/python`에는 다양한 버전의 python이 설치된 상태  

    $ python -V  
    Python 2.7.14    
    $ which python  
    /usr/bin/python  
    $ ls -al /usr/bin/python  
    lrwxrwxrwx 1 root root 24  8월 13 19:28 /usr/bin/python -> /usr/bin/python2.7  
    $ ls /usr/bin/ | grep python  
    python  
    python2  
    python2.7  
    python3  
    python3.5  
    .....

###  설정 하기  
- `--config python` : Python의 버전을 변경하는 옵션  
- 아래 명령어로 python 버전 변경 가능  

    $ sudo update-alternatives --config python  
    update-alternatives : error : no alternatives for python  
- 위와 같은 오류 발생 시 `--install [sybolic link path] python [real path] number` 명령어 사용으로 Python 버전을 등록해주면 됨  

    $ sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1  
    $ sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2  

- `sudo update-alternatives --config python` : 설치되어있는 Python 버전 선택 메뉴  

    $ sudo update-alternatives --config python  
    There are 2 choices for the alternative python (providing /usr/bin/python).  
    Selection    Path                Priority   Status   
    \* 0            /usr/bin/python3.6   2         auto mode  
    1            /usr/bin/python2.7   1         manual mode  
    2            /usr/bin/python3.6   2         manual mode  
    Press <enter> to keep the current choice[*], or type selection number:  

원하는 버전의 번호를 선택한 후 엔터 > 해당 버전이 default path로 설정 되어있음  

    $ python --version  
    Python 2.7.12  

---  
### Symbolic link 변경

    $ alias python='/usr/bin/python3.5'  
 ---  

### 원하는 버전 없을 때 설치(ex. 3.6)  

    $ sudo add-apt-repository ppa:jonathonf/python-3.6  
    $ sudo apt-get update  
    $ sudo apt-get install python3.6  

### Python 버전 2, 3을 분리하여 관리하는 방법  
버전별로 각각 등록하여 관리하면 됨  

    $ sudo rm /usr/bin/python2  
    $ sudo update-alternatives --install /usr/bin/python2 python2 /usr/bin/python2.7 1  
    $ sudo rm /usr/bin/python3  
    $ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1  
    $ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2  

아래 명령어로 원하는 버전 선택(python3)    

    $ sudo update-alternatives --config python3  

시스템의 기본 python 환경 구성  

    $ sudo rm /usr/bin/python  
    $ sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 1  
    $ sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 2  

시스템의 기본 python 환경에서 2.x를 쓸지 3.x를 쓸지 결정  

    $ sudo update-alternatives --config python  

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU1Mjk1NzMxM119
-->