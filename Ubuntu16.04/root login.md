## root 계정 login

root 계정 활성화  

    $ sudo passwd root  
    
root 계정으로 전환  

    $ su  

원래 계정으로 돌아오기  

    $ exit  

GUI 환경에서 로그인 할 수 있도록 설정  

    $ vi /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf  

위 파일에 들어가서 맨 아래 줄 추가  

    [Seat:*]  
    user-session=ubuntu  
    greeter-show-manual-login=true  

재부팅 하면 로그인 시 사용자 이름 입력할 수 있는 칸이 활성화 되며 root를 입력하고 로그인 할 수 있음  


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI1NTM4MzY2M119
-->