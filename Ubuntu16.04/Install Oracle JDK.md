## Install Oracle JDK  

### PPA(Personal Package Archive) 이용  

    $ sudo apt-add-repository ppa:webupd8team/java  
    $ sudo apt-get update  
    $ sudo apt-get install oracle-java8-installer  

### 직접 설치  
[오라클 홈페이지](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 에서 JDK(tar.gz) 다운로드  

    # 압축 해제  
    $ tar zxvf jdk-8u101-linux-x64.tar.gz  
    $ sudo mkdir /usr/lib/jvm  
    $ sudo mv jdk1.8.0_101 /usr/lib/jvm  
    # 명령어 등록(Java 처음 설치하는 경우)  
    $ sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_101/bin/java 1  
    $ sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_101/bin/javac 1  
    $ sudo update-alternatives --install /usr/bin/javaws javaws /usr/lib/jvm/jdk1.8.0_101/bin/javaws 1  
    # 기존에 다른 버전의 Java 가 설치된 경우, 명령어 실행 후 사용하고자 하는 Java 의 버전을 선택한다.  
    $ sudo update-alternatives --config java  
    There are 2 choices for the alternative java (providing /usr/bin/java).  
    Selection Path Priority Status  
    ------------------------------------------------------------  
    * 0 /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java 1071 auto mode  
     1 /usr/lib/jvm/jdk1.8.0_101/bin/java 1 manual mode  
     2 /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java 1071 manual mode  
    Press enter to keep the current choice[*], or type selection number: 1  
    update-alternatives: using /opt/jdk1.8.0_20/bin/java to provide /usr/bin/java (java) in manual mode  
    $ sudo update-alternatives --config javac  
    $ sudo update-alternatives --config javaws  

### 확인  

    $ java -version  
    java version "1.8.0_101"  
    Java(TM) SE Runtime Environment (build 1.8.0_101-b13)  
    Java HotSpot(TM) 64-Bit Server VM (build 25.101-b13, mixed mode)  


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY2ODc4NDIwMl19
-->