## Install & Test Chatscript at Windows10

Index  
> chatscript
> IIS & PHP
> Console에서 테스트하기
> Web에서 테스트하기

## Chatscript  
ChatScript-0.0.zip 다운로드 (0.0은 버전 번호) [https://sourceforge.net/projects/chatscript/files/](https://sourceforge.net/projects/chatscript/files/)   
![
](https://lh3.googleusercontent.com/s8HnXYxysuAn8wTcizXAJJZLbzYzOhnuOUuI5x0kgF-QxOey_kLHVKvz7oIqj-P0cwNYfaenJqQ "downloadchatscript")  

다운로드 받은 파일의 압축을 풀기. 이 때 위치는 일반적으로 “C:\Users\컴퓨터이름\Documents”  

ChatScript 개발을 위해서는 문서편집기 필요. 메모장, Notepad++등 편한 것을 사용.  

Window 내장 콘솔은 UTF-8의 지원이 불안정해 문자열을 처리하는 과정에서 에러를 반복적으로 발생시키기 때문에 룰 매칭이 안되었을 때 스크립트 문제인지 콘솔이 문자처리를 잘못한 것인지 알 수 없음. 따라서 다른 콘솔을 다운받아 사용하는 것을 추천.  
(ex. ConEmu :  ConEmu 설치법은 아래에 추가로 정리)  

같은 이유로 테스트를 웹이나 앱 환경에서 하는 것을 추천.  


## IIS & PHP (Windows10)
위에서 언급했듯 테스트를 앱이나 웹 환경에서 하는 것을 추천. 웹환경에서 테스트 하기 위해 Windows10 환경에 IIS와 PHP 설정을 진행. (물론 따로 서버를 사용해도 무관.) 

**제어판>Windows 기능 켜기/끄기**  
![
](https://lh3.googleusercontent.com/zfff1JtQ1fEtXWXaCIodW6gIJvKDXXg-nTFEWfqEPrtku0X5EnSNeTGXLpbnAU4COzuukSpqdHc "installiisphp1")  

**.NET Framework 3.4(.NET 2.0 및 3.0포함) 체크**  
![
](https://lh3.googleusercontent.com/ysaPWGzrB6V1crqliUjn0x5NZKCOMg2Ugl951xbS9vjhxlU0Nxi5j6j45FIf7jcVAql9-BO3hn8 "installiisphp2")  

**"인터넷 정보서비스" 중 아래 사진에서 체크 된 항목 모두 체크 후 확인 버튼 클릭**  
![
](https://lh3.googleusercontent.com/3lRsAjcbz7JKqYDrxLzcpYo_HmrVmkWE8nsVIulsVpoov42ka8XPYWf1EYyjnI0Y6WE-BmTF3zI "installiisphp3")  

**download PHP**  
[http://php.net/downloads.php](http://php.net/downloads.php) 에서 **Non Thread Safe**버전 중 **.zip 다운로드 후 압축 해제**  
 manual에서는 압축 해제 위치로 **C:\PHP 권장**    (windows 환경에서 PHP를 구동하려면, Microsoft Visual C++가 설치 되어 있어야 함)  

다운로드 받은 폴더에 있는 php.ini-production 파일을 복사하고 이름을 php.ini로 변경  
(문제가 생긴다면 C:Windows\ php.ini 폴더로 복사)  

**php.ini 파일 수정**  
|   |   |   |   |   |
|---|---|---|---|---|
|   |   |   |   |   |
|   |   |   |   |   |
|   |   |   |   |   |

원본 | 수정본
---|---
; extension_dir = “ext” | extension_dir = “.\ext”   
; log_errors = On | log_errors = On
추가 | Error_log=”C:\inetpub\temp\php-errors.log”
;cgi.force_redirect = 1 | cgi.force_redirect = 0
추가 | cgi_fix_pathinfo = 1
;fastcgi.impersonate = 1 | fastcgi.impersonate = 1
;fastcgi.logging = 0 | fastcgi.loggin = 0


**IIS에서 PHP를 처리 할 수 있게 변경**  
IIS(인터넷 정보 서비스) 관리자 실행 / IIS 항목에서 처리기 매핑 클릭  
![
](https://lh3.googleusercontent.com/XrIqv9ZSHlXr2Cxg7ea7r8NsW4toJ7Xrtsk7frQdGrODWrPoLZDdzlk4LHxYgY-EOlhBQ3BRnKM "installiisphp4")  
![
](https://lh3.googleusercontent.com/e2lANGTwpKz09ZGy6ILIzP8dsJNqYQfvobPKfTzt6ekBA7bgq15XhjAbe1EBuBeMEpE9_nA6N6k "installiisphp5")  

우측 작업 탭에서 “모듈 매핑 추가” 클릭 후 아래 내용 추가  
![
](https://lh3.googleusercontent.com/XD8ppvFCBjhpCNMjQnsRdb8scG8Luh0DkM9d3Tu11jN8zicaHh1WSi_gBadcxdjpGxZBsXLqWjo "installiisphp6")  

**Test PHP**  
test.php 파일 생성 후 C:\inetpub\wwwroot 에 파일 추가  

    <?php echo "php runs!"; ?>

웹 브라우저 실행 [localhost/test.php](http://localhost/test.php)  


## Console에서 테스트하기  

    $ cs
    $ chatscript

원하는 chatscript를 실행할 때는

    $ :build 원하는 chatscript 이름

![
](https://lh3.googleusercontent.com/AtcJUf3nhQHjKf0mYqvid5KiVN_x3iZQ5XVmBdqFZMllrrvzEUJ1ABRPf-SdysTIpatYWsN9kxQ "testconsole")  


## Web에서 테스트하기  
Webinterface/simple 폴더 내의 index.php를 사용하거나, CS_Interface_PHP.zip을 다운 받아 사용.  

사용할 php 파일을 www폴더에 이동 후 콘솔에서 chatscript server 가동.  

    $ chatscript port=1024 userlog

서버 가동 되면 브라우저에서 php 파일 실행 후 테스트 (명령어는 동일).  


## Install ConEmu  
ConEmu.exe 파일 다운로드 후 실행 [https://conemu.github.io/en/Downloads.html](https://conemu.github.io/en/Downloads.html)  
![
](https://lh3.googleusercontent.com/WJYXE-CieSdThyr1qoZj6mA18qmeE8wFgNXTee2fnxy_7AvqPrYgbrGIXhlemIZ5g9kj5ve-tKw "downloadConEmu")  

설치 완료 하면 프로그램 위쪽 공백에 우클릭>Settings (Win+Alt+P) Startup>Environment 들어가서 아래 내용 추가

    chcp 65001
    alias cs=cd C:\Users\username\Documents\ChatScript\BINARIES
![
](https://lh3.googleusercontent.com/qeXDe-5b1PySB1h8peENOfn_QppiDbKYjeSoojvAhY263XeXXLUwcD_nGGlvZcAwLmn1Az-jTtU "settingconemu")  


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA0NDg2MTUwNywxODAzNjAzMjA0XX0=
-->