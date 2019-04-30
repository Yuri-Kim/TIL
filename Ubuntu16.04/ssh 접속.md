## Ubuntu16.04 ssh 접속  

### 다른 서버 접속하기  

    $ ssh 아이디@호스트 주소  

### 22번 port 이외 포트 사용  

    $ ssh 아이디@호스트주소 -p포트번호  

### ssh 접속시 RSA 공유키 충돌 문제 해결  
![
](https://lh3.googleusercontent.com/m2EL0RXcf1Z7Itw_9noiJcSTaw8KySiHMhLpifom-TNKESaVgAoQmnCP2A2iHEidcz4tzIwcU1w4 "ssh1")  

아래 명령어 실행 후 다시 접속  

    $ ssh-keygen -R 호스트주소  





<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMwNTEwMzU5MV19
-->