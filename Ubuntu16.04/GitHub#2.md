## GitHub #2  

 - git init : 새로운 local repository 생성  
 - git add : 변경된 파일을 storage에 추가  
 - git commit : add한 파일을 local repository에 저장  
 - git push : local repository를 remote repository에 업로드  

소스코드가 있는 폴더로 이동  

    $ cd 폴더 경로  

해당 폴더에 local repository 생성  

    $ git init  

버전 관리 대상 파일들의 상태 파악  

    $ git status  

버전 관리할 파일들 추가 (. 하면 모든 파일 추가)  

    $ git add .  

commit message 작성  

    $ git commit -m "메세지 내용"  

remote repository 등록 (origin : 매번 주소를 입력 하는 것이 귀찮으므로 사용하는 별칭 같은 것)    

    $ git remote add origin {remote repository 주소}  

commit한 내용 remote repository에 push  

    $ git push origin master  

master가 아닌 다른 branch로 push하고 싶다면 아래와 같이 브랜치 명으로 명령어 실행  

    $ git push origin {branch name}  

push오류 날 때 임시방편(강제 push)  

    $ git push -u origin +master  

특정파일/폴더 제외하고 push  
(git rm --cache  명령어는 Staging Area에서 파일을 제거하고 working directory에서는 파일을 유지하는 명령어 / 명령어를 실행한 후 꼭  commit 해줘야 함)

    // 파일 제외  
    # git rm --cached 파일명  
    // 디렉토리 제외  
    # git rm --cached 폴더명\ -r  

여러 폴더/파일을 제외하고 싶다면, 

    $ vi .gitignore  
    // 커밋에서 제외할 폴더나 파일 입력  
    .idea/  
    // git commit 수행  
    $ git commit -m 'ignore files'  
      



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI1NTE5NTU2OSw1OTE4ODQ5NjksMTg1Nj
Y2NDEyMCwtMjE0MzY2MTQzM119
-->