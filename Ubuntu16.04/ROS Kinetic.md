
## ROS Kinetic  

### Installation  
참고 문서 : [http://wiki.ros.org/kinetic/Installation/Ubuntu](http://wiki.ros.org/kinetic/Installation/Ubuntu)

우분투 저장소 설정  
sources.list : 아래 명령어로 list 추가 해줌  

    $ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'  

key 받아오기 : 접근 위한 key 발급  

    $ sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654  

ROS 설치  
설치전 update  

    $ sudo apt-get update  

ROS와 기본 패키지 설치  
Desktop-Full Install: (Recommended) : ROS, rqt, rviz, robot-generic libraries, 2D/3D simulators, navigation and 2D/3D perception 로 자동 설치  

    $ sudo apt-get install ros-kinetic-desktop-full  

rosdep 초기화  
ROS 사용하기 앞서, ROS를 돌리기 위한 설정 진행  
(rosdep이 그 역할 해줌)  

    $ sudo rosdep init  
    $ rosdep update  

위 과정에서 아래와 같은 오류가 난다면,  

    ERROR: default sources list file already exists:  
    /etc/ros/rosdep/sources.list.d/20-default.list  
    Please delete if you wish to re-initialize  

아래 명령어 입력 후 다시 진행  

    $ sudo rm -r /etc/ros  
    $ sudo rosdep init  

환경설정  
bashrc를 통해 shell을 켤 때 마다 자동으로 환경변수가 설정되도록 해줌  

    $ echo "source /opt/ros/kinetic/setup.bash"  >>  ~/.bashrc  
    $ source ~/.bashrc  

환경변수 확인  
ROS_ROOT등이 나오면 정상적으로 추가된 것  

    $ printenv | grep ROS  

rosinstall 설치  

    $ sudo apt-get install python-rosinstall  

ROS Workspace 생성  

    $ mkdir -p ~/catkin_ws/src  
    $ cd ~/catkin_ws/src  
    $ catkin_init_workspace  

(아무것도 없지만) build 해보기  

    $ cd ~/catkin_ws/  
    $ catkin_make  

위 결과로 build, devel 폴더 생김  

아래 명령 실행 후, 방금 전 setup으로 workspace가 overlay되게 하기 위해 환경변수 포함시켜 줌  

    $ source devel/setup.bash  
    $ echo $ROS_PACKAGE_PATH  /home/youruser/catkin_ws/src:/opt/ros/kinetic/share  

---
주의할점  
- 똑같은 명령어로 설치해도 vertualenv같은 가상 머신에서는 의존성 깨지는 문제 발생... (아직 해결방법 못찾음)  
  



<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAxODc0NDgxMSw2MjAyMjA2NDJdfQ==
-->