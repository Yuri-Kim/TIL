
## Permission 관리  

현재 위치의 디렉토리나 파일의 권한 보기  

    $ ls -al  


    drwx-w-r-x  

이런 문구가 해당 폴더나 파일의 권한을 나타냄  

| d | r | w | x | - | w | - | r | - | x |  
|--|--|--|--|--|--|--|--|--|--|    
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |    
| -:파일, d:디렉토리 | 소유자 read | 소유자 write | 소유자 execute | 그룹 read | 그룹 write | 그룹 execute | 방문자 read | 방문자 write | 방문자 execute |  

위 표의 숫자로 나타냈을때 2~10번 자리는 세자리씩 묶어서 생각하면 됨  

    drwx-w-r-x  

위 예시로 설명하면,  
이 디렉토리의 **소유자**는 **읽기, 쓰기, 실행하기** 모두 할 수 있고  
소유자와 같은 **그룹**의 사용자는 **쓰기**만 할 수 있음  
**방문자**는 **읽기**와  **실행**만 가능  

![
](https://lh3.googleusercontent.com/U2Yt6qDplZhzVU9g3gCajFz3ndLaBLEnf9q7KqbnfBbzsdtbWbDqwLk6AiLLMpRTWytrFcdrp9cQ "permission1")  

위 사진에서 3번째 출력이 소유자, 4번째 출력이 그룹  
ex. root root → 소유자 : root, 그룹 : root  

권한 변경 명령어  

    $ chmod 755 name  

name은 권한을 바꿀 파일이나 디렉토리 이름  
숫자는 아래 표의 구조로 이루어 짐  
  
 r | w | x |  
|--|--|--|  
| 4 | 2 | 1 |  

즉,  

 1 | 2 | 3 | 4 | 5 | 6 | 7 |    
|--|--|--|--|--|--|--|    
| --x | -w- | -wx | r-- | r-x | rw- | rwx |   

예를 들어 755는 4+2+1, 4+1, 4+1 → 즉, rwxr-xr-x를 나타냄   


 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg1ODUwOTk4NSwxNjI0MDc2MjVdfQ==
-->