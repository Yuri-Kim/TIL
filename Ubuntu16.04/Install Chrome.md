## Install Chrome  

**apt-get** 설치

    $ get -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -  
    $ sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'  
    $ sudo apt-get update  
    $ sudo apt-get install google-chrome-stable  

`apt-get update` 명령어로 패키지 목록을 업데이트 할 때 아래와 같은 오류가 난다면,  

    W:  Target  Packages  (main/binary-amd64/Packages)  is configured multiple times in  /etc/apt/sources.list.d/google-chrome.list:3  and  /etc/apt/sources.list.d/google.list:1  

아래 명령어 입력  

    $ sudo rm -rf /etc/apt/sources.list.d/google.list  

**wget** 설치  

    $ sudo apt-get install libxss1 libgconf2-4 libappindicator1 libindicator7  
    $ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb  
    $ sudo dpkg -i google-chrome-stable_current_amd64.deb  


<!--stackedit_data:
eyJoaXN0b3J5IjpbNTYwNDY0MDc4XX0=
-->