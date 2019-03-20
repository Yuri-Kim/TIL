## Fulfillment Webhook Example  
 
 > Example test 환경
 > virtualenv 설치  
 > flask 설치 & Test  
 > ngrok 설치 & Test  
 > fulfillment example    
 
 ### Example test 환경
 
이 문서는 아래와 같은 환경 기준입니다.
  
|  |  |  
|--|--|  
| OS | windows10 |  
| python | 3.7.0 |    

### virtualenv 설치   

cmd 관리자 권한으로 실행  

virtualenv 설치  
`pip install virtualenv`  

가상환경으로 설정할 폴더 생성 후 해당 디렉토리로 이동  

    mkdir fordername  
    cd fordername  
    virtualenv venvname    

생성한 가상환경 활성화  

    call venvname/scripts/activate  

+) window10 cmd에서 D드라이브로 이동  
`D:`  


### flask 설치 & Test   

가상환경에 flask 설치

    pip install flask  

flask 작동 확인 

소스코드  

    '''python
    # import flask dependencies  
    from flask import Flask  
    
    # initialize the flask app  
    app = Flask(__name__)
    
    # default route  
    @app.route('/')
    def hello_world():
	    return 'Hello world!'
	    
	# run the app
	if __name__=='__main__':
		app.run()
    '''
    
cmd에서 실행

    python test.py  

![
](https://lh3.googleusercontent.com/Tv_5Esg7Ni_pXUzJ5dxkMDkci__Rk_iR3mnvqzsQarL0hlgJz52u7WxFijgU8JxKK2QQIAumP5a0 "flask")  

![
  ](https://lh3.googleusercontent.com/2gMm9ha5CdG6sAEERiya_prxWa3XCwrjX3TBw9ZMUNYT_gNd1GpSNsgEezE5zOO6SqkEb7G3L9yv "flask2")  

### ngrok 설치 & Test    

https://ngrok.com/ 에서 .zip 다운로드  
![
](https://lh3.googleusercontent.com/LnSbRKQQi2A8uktsBLF52Jp4kuukyiZVRIF9ysj54fEXLG3ITnVsjYqHqjehwuo-tqFC4hurtLKO "ngrok")  

압축 풀고 cmd에서 ngrok.exe 있는 폴더로 이동

    ngrok http portnumber  
ngrok http 5000 (for flask app)
![
](https://lh3.googleusercontent.com/wyf7gR-snqaHOpQU0CzscAl2Rw2Jkwa9jG_UfQ29IhtDazm8-DI8CJgXXSDrOCQHMVxL0iTglWxb "ngrok2")  

**ngrok?**  
방화벽을 넘어 외부에서 로컬에 접속 가능하게 하는 터널 프로그램  
![
](https://lh3.googleusercontent.com/vyy_IjrEMzWD13LF31gX5sMfZRGPLAzyP33C7rthaJdce7P8yeJfL_q4zRbfEPFSxvG0lX3I39Qu "ngrok3")  
출처 :[https://ngrok.com/](https://ngrok.com/)  


### fulfillment example   



<!--stackedit_data:
eyJoaXN0b3J5IjpbNDgxMjA0OTVdfQ==
-->