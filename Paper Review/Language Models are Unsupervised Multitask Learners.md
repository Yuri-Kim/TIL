## Language Models are Unsupervised Multitask Learners  

Alec Radford, Jeffery Wu, Rewon Child, David Luan, Dario Amodei, Ilya Sutskever (openAI, 2019)  [paper](https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf), [blog](https://openai.com/blog/better-language-models/)    


### Abstract  
- question-answering, machine translation, reading comprehension, summerization 같은 NLP Task는 보통 task-specific한 dataset을 이용하는 supervised learning이 일반적임  
- WebText라는 (이 논문에서 만든 dataset) 수백만 dataset으로 학습할 때 어떤 라벨링이나 explict supervision없이 위 LM을 학습시키고 싶음  
- LM의 능력은 zero-shot task에 필수적임.  
- **GPT-2**는 1.5B parameter Transformer이고 LM dataset 8개 중 7개에서 SOTA (4개의 model을 제시했는데 각 모델의 차이는 parameter차이)  

### Introduction  
- 많은 데이터를 이용한 supervised learning은 데이터의 분포에 민감 ( 즉, 모델이 학습한 데이터가 아닌 새로운 데이터에 대해서는 잘 작동하지 않을 수 있음(narrow expert)) → 그래서 저자는 새로운 dataset을 만들고 labeling하는 작업 없이 많은 task들에서 성능을 낼 소 수 있는 general system을 지향하고 싶음  
- 보통 data를 수집하여 train set / test set으로 나눠 train / test를 진행 하는 것이 일반적 (IID를 만족한다고 가정) → 이 방법은 captioning models, reading comprehension systems, image classifiers 같은 다양한 input에 대해서 제대로 동작하지 않는 단점이 있음  
-  저자는 이러한 문제가 single domain dataset에 대한 single domain training에 있다고 생각  
-  최근 벤치마크들은 GLUE, decaNLP를 통해 평가됨  
- Multitask learning을 이용한 시도도 있지만, NLP에 대한 Multitask learning은 아직 초기 단계 → Multitask learning을 하려면 결국 많은 dataset이 필요하기 때문에 scale을 크게 하기 힘듦 (task가 추가 될 때 마다 새롭게 dataset 구축하고, train해야함.. 그래서 우리가 제안한 model이 Multitask learning에도 도움될 것임)  
- 현재 language task에서 가장 좋은 성능을 내는 모델은 pre-trained + supervised fine-tunning(BERT도 그렇듯이)    
	- word-vector + task-specific 모델 학습  
	- contextual representaion 이용  
	- BERT 방식 (많은 self-attention block 이용)  

![
](https://lh3.googleusercontent.com/G4hhXH3PN3hjxyvfxy2bPmJ2FbEXHrkFAXtCyTO1B2Xby3k6cDDXYFdvfzpHiOjMbDbA-KtapttV "gpt2_1")    

### Approach  
- 본 논문 접근법의 핵심은 Language modeling방법으로 접근 했다는 것  
- 보통 Language modeling은 조건부 확률을 이용해 sequential하게 단어를 예측(conditional probablities)  
![
](https://lh3.googleusercontent.com/sZ-ol9yZvQrPXl9UPRpWE0Jz22ltxGAF6rZD1tNdja1tG7EvcysPnDhNShDSejyIfXMkk-hpx-lx "gpt2_ex1")   
- 즉 p(output|input)하는 것인데 general system에서 여러개의 task를 진행해야 한다면 → p(output|Input, task) (→ 보편 시스템은 여러 다양한 작업을 수행할 수 있어야 하며, 심지어 동일한 인풋값을 받더라도 인풋에 대한 것뿐 아니라 수행해야 할 다른 작업에 대해서도 조건화할 수 있어야 함)  
- 이 말은 어떤 task를 해야할 지 model의 조건으로 넣어준다는 것  
- How? → 선행 연구 중 Multi-task learning 논문을 래퍼런스로 소개(McCann)  
- McCann? : (translate to french, English text, french text) / (answer the question, document, question, answer) 처럼 처음에 무슨 task를 진행하는지 언급해 주고 그 다음에 input들이 들어가서 원하는 결과(french text or answer) 를 출력하는 방식 (아래 예시 그림을 보면, 원하는 task를 question형식으로 줌)     
![
](https://lh3.googleusercontent.com/uV8vYBkLGNKAIs7IRxEVxKGQwk84cjUmOKhnQiNYn1IardL_j5RXHD5bp4ASqZfMu3WLC64vKVO_ "McCann")  
- 이런게 가능하네? → openAI에서 시도  
- McCann과의 차이점 : McCann은 multi-task learning으로 실제 여러 개의 데이터 세트를 가져와서 학습한것 / GPT2는 LM을 unsupervised-learning으로 한것  
- 즉, GPT2는 fine-tunning의 과정이 없다고 볼 수 있으며, 어떤 task에도 적용 가능 → 실제로 학습 해 보면, Multi-task learning에 비해 매우 느림  
- 결론적으로 충분한 capacity가 있으면 모델은 general system을 가질 수 있고 LM을 통해 unsupervised multi-task learning을 할 수 있음!  

**2.1 Traning Dataset**  
- 이전의 LM에서는 single domain text를 사용 (ex. News articles, Wikipedia, Fiction blocks 등)  
- 다양한 도메인의 dataset도 존재 (Common crawl) but, 문제점 존재하는 dataset (한 레퍼런스 논문에서 Common crawl 데이터의 많은 부분이 이해 할 수 없는 내용이라고 함 / 실제로 openAI가 해당 데이터로 연구를 시작했는데 비슷한 문제점 발견)  
- 그래서, Web scrape을 해서 데이터를 제작! 제작방법을 간단히 정리하면,
	- 사람에 의해 필터링되거나 큐레이팅 된 웹페이지만 스크랩  
	- Reddit의 link 사용  
	- 이중 Karma 3개 이상 받은 것만 사용(Karma : 페북의 좋아요 같은거)  
	- 모아진 텍스트인 WebText는 4500만개 링크의 텍스트 서브세트를 포함, HTML에서 텍스트를 추출하기 위해 우리는 Dragnet과 Newspaper를 조합해 사용  
	- 2017년 12월 이전 post만 가져왔음  
	- 40GB text, 총 8백만 문서 생성  
	- Wikipedia 문서는 부분은 제거 (다수의 링크가 위키피디아로 향하고 있어서 중복될 우려가 있었기 때문)    

**2.2 Input Representation**
- 제대로 이해가 안됐는데.. 결론적으로 byte-level 접근이 generality 측면에서 좋고 Unicode string은 pre-processing, tokenization,  vocab size에 대한 걱정없이 LM에  적용 가능...?  
- GPT-2 모델에서는 byte단위로 작동  

**2.3 Model**
- openAI GPT와 구조는 비슷한데 세부 사항 수정이 있음 (Transformer기반 아키텍쳐 사용)  
	- Moving normalization layer to the input of each sub-block  
	- Adding normalization layer after final self-attention model  
![
](https://lh3.googleusercontent.com/WaIq15m3TeUv9_EuLBfeg2TFkL6amYEK1jSe9ShFdVrqolQQn2c843maxbcH_Zn6V-oPSe67C3P4 "gpt1")   

4가지의 다른 시나리오로 학습 (다른 parameter를 가지는 4가지 모델을 train)  
![
](https://lh3.googleusercontent.com/lbVvHul56eup4Dp8MjWrpyQigFteRJFQNqt3jYuYcycIbSRxyfHVMBLhhB7osO10m6En4K587_X7 "gpt2_2")  

### Experiments  
WebText만 가지고 실험하니까 underfit이 되는 것을 알 수 있음  

**3.1 Language Modeling**  
![
](https://lh3.googleusercontent.com/ZEgwFdCM8uV3OEqyNeRlob3tnGL0qJvpM_kvexiQps8qmvRG4sJh-3fdGvM_ZuE7iSJjShHcABzX "gpt2_3")   
- 8개 항목 중 7개에서 SOTA  
- Peen Treebank, WikiText-2같은 소규모(1~2백만 개) 데이터셋에서 눈에띄는 개선   
- LANBADA, Children's Book 같은 long-term dependencies 해결을 위한 dataset에서도 눈에 띄는 개선  
- 1BW에서 성능이 안좋음 → 1BW’s sentence level shuffling removes all long-range structure     

**3.2 Children's Book Test**  
long-term dependencies 측정을 위한 데이터 셋  
일단 생략    

**3.3 LANBADA**  
long-term dependencies 측정을 위한 데이터 셋  
일단 생략    

**3.4 Winograd Schema Challenge**  
일단 생략  

**3.5 Reading Comprehension**  
- CoQA (Conversation Question Answering dataset - 7개 domain으로 구성)로 test   
- Input : [Paragraph, QA history, final Q, token A]  
	- token A : Answer하라는 의미의 token  
- Unsupervised-learning인데도 불구하고 dev셋에서 base-line system 3개 보다 좋다고 하는데, CoQA 리더 보드에 있는 BERT기반 모델에 비해서는 성능 떨어짐  

**3.6 Summarization**  
![
](https://lh3.googleusercontent.com/lWGbE9LNK6Fm1xUyYJXQkz0pgMm76YdoP-4GRcT5d-ePA0JrCZVSFymmKdp2vKtdpIZYYYxWxEz_ "gpt2_3")   
- CNN and Daily Mail dataset으로 실험  
- Input : [Paragraph , TL, DR]  
	- TL : Too Long  
	- DR : didn't read  
- LM으로 생성할 때, Top-2확률 word 중에서 random sampling 100개의 token 생성  
- 생성된 token 중 처음 3개의 문장을 요약된 결과라고 지정  
- classic neural baseline 보다 살짝 좋은 정도의 성능 (Summarization만을 위한 모델보다는 성능 떨어짐)  

**3.7 Translation**  
- 앞서 언급한 McCann처럼 무슨 task인지 처음에 알려줌  
- 영어 → 프랑스어 task를 하려면 [Example sample pair, english sentence] 처럼 입력 넣으면 됨 (반대의 경우도 마찬가지)    
- Eng → French : 성능 매우 안좋음 / French → Eng : SOTA는 아니지만 다른 unsupervised learning보다 괜찮음  
- openAI가 데이터를 만들 때, 영어가 아닌 언어로 된 문서들은 제거 했는데 성능나옴 → why? 10MB의 French language가 남아있었음 → 이것은 더 많은 프랑스어 데이터가 있었다면 더 좋은 성능이 나왔을 수도 있다는 것을 나타냄  

**3.8 Question Answering**  
- Translation처럼 example을 통해서 알려줌  
- Natural Question dataset 사용 시 믿을 만함  
- SQuAD에서도 test해봄  
추가적인 정리 필요  

### Generalization vs Memorization  
- 최근의 연구들에서 dataset 문제가 존재 했음 → CIFAR-10에는 train/test 간 3.3%의 overlap이 있었음(2019년 어떤 논문에서 발견) → 그래서 새롭게 나온 데이터 셋이 CIFAIR  
- 위의 문제(overlap) 때문에 generalizatoin performance가 over-reporting될 수 있음  
- WebText를 만들 때 고려해야 했음
	- Bloon filter 사용   
	- 8-gram 겹치는정도를 데이터 간 비교 후 측정  
	- 많은 데이터에서 overlap 문제점 존재  
	- CoQA는 document(paragraph)는 15% 겹치지만 QA는 겹치는게 없음  

![
](https://lh3.googleusercontent.com/VOsknt70D9Rye5a1ayjR0iEIpy-tMV80la4sloKXuBUEG578YXXqyOQvQAC-bGKXot8-X5jTKcwL "gpt2_5")   
 - 이런 overlap, similar text가 학습에 끼치는 영향을 알아내는 것이 중요함  
 - 어떻게 overlap을 검출하는지도 중요 → 현재는 n-gram방법 쓰는 것을 추천  
![
](https://lh3.googleusercontent.com/ItrJ7hZx0RVwNz1R_0TqWZZbixHF0MBD-pYc1wEp5MTFovIDO7-HV_6yEOsgsOXH-3TC-uJWnaEn "gpt2_6")  
- 위 그림을 보면 LM 파라미터가 늘어날수록 train, test 모두 perplexity가 떨어짐  
- 즉, GPT-2 또한 아직 underfitting 됨  

### Related Work  
나중에 정리해야지  

### Discussion  
- Supervision없이 task를 배우는 pre-training기술도 가능성이 있다!  
- 현재 상태는 충분한 capacity가 있을 때, 몇개의 baseline보다 성능이 좋은 정도이다!(아직 각 task마다 성능이 훨씬 뛰어난 모델이 많다...)    
- GPT-2로 많은 zero-shot task에 성능을 측정 해 보았을 때, 가능성은 있지만 아직 이것의 fine-tunning ceiling은 명확하지 않음  
- BERT에서 언급했듯 uni-directional representation은 비효율적이라고 했는데 GPT-2에서 이것을 어떻게 극복할지는 불분명 (GPT-2는 transformer의 decoder을 쓰기 때문에 LM의 특성상 sequential한 상황으로 사용. 즉, 이렇게 하면 uni-direction이 됨. BERT처럼 bi-direction embedding이 될 수 없음)  

### Conclusion  
- 크고 다양한 dataset을 이용해 언어 모델을 학습하면 많은 dataset과 domain에 대해 좋은 성능이 나올 수 있음  
- 본 논문에서 제안한 GPT-2는 8개의 dataset 중 7개에서 SOTA   

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNTQyNTU2NjgsLTE3MTM5NDIzMDZdfQ
==
-->