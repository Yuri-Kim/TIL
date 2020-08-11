# docker Image commit & push 하기 

## docker image commit 

현재까지 작업했던 컨테이너를 그대로 저장하고 싶을 때, 실행중인 컨테이너 커밋  

`$ docker commit CONTAINER IMAGE_NAME`  

CONTAINER : 실행중인 컨테이너 이름 

IMAGE_NAME : 저장할 이미지 이름

제대로 저장되었는지 확인

`$ docekr images`  



## docker image push  

docker cloud에 로그인 

`$ docker login`

docker image에 tag 달기

`$  docker tag IMAGE_NAME REPOSITORY_NAME:IMAGE_NAME` 

tag달린 docker image를 docker cloud에 push 

`$ docker push REPOSITORY_NAME:IMAGE_NAME` `

+) repository name 매번 지정하기 귀찮다면, docker user id 지정해두고 사용 

`$ export DOCKER_ID_USER="name"`

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY5NTE3NzU4Nl19
-->