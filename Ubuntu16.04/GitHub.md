## GitHub 사용하기  (ubuntu)  

### install git  

    $ sudo apt-get install git-core  

### GitHub 개인 정보 등록  

    $ sudo git config --global user.name "본인 계정 입력"  
    $ sudo git config --global user.email "본인 메일 주소 입력"  
    $ sudo git config --global color.ui "auto"  

### work directory 생성  

    $ sudo mkdir /workspace  
    $ cd /workspace  

### GitHub 저장소 복제  

    $ sudo git clone https://github.com/Yuri-Kim/test.git  

### 원격 저장소 등록  

    $ sudo git remote add origin https://github.com/Yuri-Kim/test.git  
    $ sudo git fetch origin  

### 변경된 모든 파일 추가(commit전에 필수 실행)  

    $ sudo git add -A  

아래의 명령어를 치고 엔터 누르면 변경 목록이 보임  

    $ sudo git commit  

### commit message 입력  

    $ sudo git commit -m "커밋 메시지 입력"  

### 저장소에 올리기 (계정&암호 물어보면 입력하기)  

    $ sudo git push  

### 저장소 업데이터 (내려받기)  

    $ sudo git pull  

### git 상태 확인  

    $ git status  




<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk1NDUwNDY0OF19
-->