## Remove dir (+permission denied)  

    $ rmdir (directory_name)  
기본적으로 위 명령어 통해 삭제 가능  
파일 삭제에 사용되는 rm을 통해서도 삭제 가능

    $ rm -rf (directory_name)  
-f : 파일 유무와 관계없이 삭제  
-r : 디렉토리도 같이 삭제  

**permission denied** 
    $ sudo rm -rf (directory_name)  
root 권한으로 강제 삭제  

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMDA2NDc3NjZdfQ==
-->