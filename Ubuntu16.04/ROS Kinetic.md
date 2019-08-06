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

환경설정  
bashrc를 통해 shell을 켤 때 마다 자동으로 환경변수가 설정되도록 해줌  

    $ echo "source /opt/ros/kinetic/setup.bash"  >>  ~/.bashrc  
    $ source ~/.bashrc  

환경변수 확인  
ROS_ROOT등이 나오면 정상적으로 추가된 것  

    $ printenv | grep ROS  

rosinstall 설치  

    $ sudo apt-get install python-rosinstall  


<!--stackedit_data:
eyJoaXN0b3J5IjpbNjIwMjIwNjQyXX0=
-->