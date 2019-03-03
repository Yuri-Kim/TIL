## Overview Intent  

Index  
> google Dialogflow?  
> Intent?  

---  
### google Dialogflow?  
Google의 챗봇 플랫폼  
 
Api.ai + Google의 머신러닝 엔진 → API.ai의 편리함 + Google machine learning engine의 성능  

**Dialogflow의 대화 흐름**  
 - 사용자 입력  
 - Dialogflow agent의 구문 분석    
 - Agent가 user에게 답변 전달    

---  
### Intent?

**Intent란?**  

 - 대화를 정의하기 위해 사용사가 agent에 input과 reponse를 매핑하는 intents를 정의함.  
 - 각 intent는 각 intent를 유발할 수 있는 사용자 발화의 예시, 발화에서 추출할 대상, 응답 방법을 정의.  
 - 일반적으로 인텐트는 하나의 대화 턴을 나타냄. (ex. 선호하는 색에 대한 사용자의 입력을 인식하고 응답하는 agent를 생성할 수 있음)  

**Intent의 요소**  

 - Intent name : intent의 이름  
 - Training phrases : 각각의 intent에 매칭될 수 있는 사용자 발화의 예시  
 - Action and parameters : 사용자 발화에서 parameter를 추출하는 방법 정의. parameter에는 날짜, 시간, 이름, 장소 등이 있음. parameter를 정보검색, 작업수행, 응답 반환 같은 다른 logic에 사용할 수 있음   
 - Response : 사용자에게 표시되거나 말해지는 발화  

**Intent matching**  

Dialogflow는 사용자가 발화할 때마다 특정 intent와 발화를 일치시키려고 시도하고 해당 intent내에서 응답 반환. 이 때 인식되지 않는 사용자 발화를 위해 fallback intent를 생성할 수 있음.  

Dialogflow는 개발자가 정의한 학습 문장, 중요 단어, 문장, 값 등을 이용해 intent와 매칭.  

![
](https://lh3.googleusercontent.com/JufjDsdi6XXARpIZ8Ggh8QHFL4c6SFfCB_JcTR6Xv94FogsNCpoJ8KiYZVqFrvCSYs78ote6Egw "intent1")  
(그림) 사용자 발화가 intent와 성공적으로 일치되었을 때의 대화 흐름  

출처 : https://dialogflow.com/docs/intents  

<!--stackedit_data:
eyJoaXN0b3J5IjpbOTY2MTM0MjUyXX0=
-->