
## Unified Language Model Pre-training for Natural Language Understanding and Generation  

Li Dong, Nan Yang, Wenhui Wang, Furu Wei et al. (Microsoft Research) [Paper](https://arxiv.org/abs/1905.03197)  
Source code : [github](https://github.com/microsoft/unilm)  
33rd Conference on Neural Information Processing Systems (NeurIPS 2019), Vancouver, Canada.  

### Abstract  
- UNILM : Unified Pre-trained Language Model  
- UNILM은 NLU와 generation task에서 모두 fine-tune할 수 있는 모델  
- 세가지 language modeling objecives를 사용하여 모델을 Pre-train함 
	- unidirectional (both left-to-right and right-to-left)  
	- bidirectional  
	- sequence-to-sequence prediction  
- Shared Transformer network 사용,  prediction condition들의 control하는데 utilizing specific self-attention mask 사용 → unified modeling  
- 단방향 디코더나 양방향 인코더, seq2seq 모델로 UNILM을 fine-tune하여 down stream NLU와 generation task를 할 수 있음  

### Introduction  
- LM의 pre-training은 다양한 NLP task를 발전 시킴  
- Pre-trained LM은 context에 기반한 prediction word token들을 이용해 상황에 맞는 text를 representation  
- 거대한 양의 text data를 pre-training 한 후 downstream task에 맞게 모델을 fine-tuning할 수 있음  
- 아래 표와 같이 다양한 유형의 LM을 pre-train하기 위해 다양한 prediction task와 training objective들이 사용되고 있음  
![enter image description here](https://lh3.googleusercontent.com/_ZiA8SqkJWfBvo0VI50jesr0XYb8hD8EU1eCF54rM98zfEZXrQY76ihlSnaE_sgrz3JSD2nJjkh1 "1")  
	-	**ELMO** (Peters et al,, 2018)는 long short-term memory networks를 기반으로 한 두개의 unidirectional LM을 학습 (forward LM : text를 왼쪽 으로 읽고, backward LM : text를 오른쪽 으로 인코딩)    
	-	**GPT** (Radford et al., 2018)는 left-to-right Transformer를 이용해 text sequence를 word단위로 predict  
	-	**BERT** (Devlin et al., 2018)는 bidirectional Transformer encoder를 사용해 masked word들을 predict하기 위해 오른쪽과 왼쪽 context를 fuse(융합?)  
	-	또한 **BERT**는 한 쌍의 텍스트의 관계를 명시적으로 모델링 할 수 있어 자연어 추론(Natural Language Inference)같은 pair-wise NLU task에 유리함 but, 광범위한 NLP task에서 성능을 향상시켰지만, bidirectionality때문에 NLG(generation task)에 적용하기는 어려움  
- 본 논문에서는 **NLU와 generation task모두에 적용가능한 UNILM(UNIfied pretrained LanguageModel)을 제안**  
-  UNILM은 deep Transformer network (대량의 text에 대해 3가지 유형의 unsupervised language modeling objectives로 활용됨(아래 표 참조)  
![enter image description here](https://lh3.googleusercontent.com/7LqaYkbzODAnYXnBOA8C4ag9O2O0_0Jnjy4OLBJ1g67mfzh7WZJMwCtFXO8nUu4HafjjNNPvEZWI "2")  
	- 특히 위 표에서 LM을 위한 cloze tasks를 설계함 (masked된 단어는 context기반으로 predict됨)  
	- 왼쪽 → 오른쪽 단방향 LM : predict할 masked 단어의 context는 왼쪽 모든 단어로 구성  
	- 오른쪽 → 왼쪽 단방향 LM : predict할 masked 단어의 context는 오른쪽 모든 단어로 구성  
	- 양방향 LM : context가 왼쪽 오른쪽 모든 단어로 구성  
	- seq2seq LM : predict해야하는 두번째 (타겟) sequence의 context는 첫번째 (소스) sequence의 모든 단어들과 타겟 sequence의 왼쪽에 있는 단어들로 구성 됨  
- BERT와 유사하게 UNILM을 다양한 downstream task들에 맞게 fine-tune할 수 있음 (필요할 경우 추가적인 task-specific layer 이용)  
- 하지만 NLU에 자주 사용되는 BERT와 달리 다른 self-attention mask들을 사용한 UNILM은 다양한 타입의 LM의 context를 수집해 NLU와 generation task 모두에 적용가능  
- **UNILM의 큰 세가지 장점**  
	- 통합된 pre-training 절차를 통해 파라미터와 아키텍쳐를 공유하는 단일 Transformer가 생성되기 때문에 여러개의 LM에 대한 분리된 학습이나 hosting이 불필요  
	- prarameter sharing이 학습된 text representation들을 더 general하게 만들어줌 (왜냐하면,  

### Unified Language Model Pre-training  
- UNILM은 multi-layer Transformer network를 기반으로 함  
- input 시퀀스 x = x_1, ... , x_|x|가 주어지면 모델은 각 토큰에 대해 상황에 맞는 vector representation를 얻음  
- input token들은 word, position, text segment에 따라 표시됨  
- input vector는 multi-layer transformer 블록들의 스택에 입력되며  self-attention을 사용하는 이 블록은 전체 입력 시퀀스를 고려하여 text representation들을 계산함 (? 맞아? 원문 : Next, the input vectors are fed into a stack of multi-layer Transformer blocks, which uses self-attention to compute the text representations by considering the whole input sequence. )  
- 아래 그림에서 볼 수 있듯, unified LM pretraining은 여러 unsupervised LM objective들(unidirectional LM, bidirectional LM, sequence-to-sequence LM)에 대해 shared Transformer network를 최적화  
- predict될 word token의 context에 대한 접근을 제어하기 위해(왜?) self-attention에 다른 mask들을 사용함  
- 다시 말해, masking을 사용해 contextualized representation을 계산할 때 토큰이 얼마나 많은 context에 영향을 주는지 제어  
- Unified LM이 pre-train되면 다양한 downstream task들에 대한 task-specific data를 fine-tune할 수 있음  
 
![](https://lh3.googleusercontent.com/9OxCWCThMcBncK1ZBjPxKABJqZudPUkNIZg3aFbKJqDIFFCj03htqjXcAmDLZ0bkxxa4MP4typVt "3")

**1. Input Representation**  
- input x는 word sequence로 unidirectional LM의 text segment이거나 bidirectional LM과 seq2seq LM가 함께 묶인 한 쌍의 segment임  
- input을 시작할 때 항상 ([SOS]) 토큰(special start-of-sequence) 추가  
- corresponding output vector를 전체 출력으로 사용  
- 각 segment 끝에 ([EOS])토큰(special end-of-sequence)추가  
- 토큰이 한 쌍의 segments의 경계를 표시 함  
- [EOS]토큰은 NLU task에서 문장 간의 경계를 표시하면서, genertation task를 위한 모델 학습 시 decoding process를 종료하는데 사용됨  
-  input representation은 BERT를 따라감 (뭔지 다시 확인해서 정리)  
	- 예를 들어서, "forecasted"  → "forecast", "##ed" (##는 하나의 단어에 포함됨을 나타냄)  
- 각 input token의 vector representation은 corresponding token embedding + position embedding + segment embedding (sum)  
-  UNILM은 여러가지 LM task들을 사용하여 학습되기 때문에 segment embedding이 어떤 LM 인지 구분하는 식별자 역할을 함 (각 LM마다 다른 segment embedding을 사용하기 때문)   

**2. Backbone Network: Transformer**  
- input 벡터 ![](https://lh3.googleusercontent.com/8NsGvrXPp8zylZiMIkZA_EwMyaar4J5pcOj1Ak01UyRp8-YA09Klh09jGosujKTpJR6br8mcjJSZ "001") 를 먼저 ![](https://lh3.googleusercontent.com/Nsd8dzf6Yl39jU691nvGt6HkGacK8BsyH6ZHnX_ADSWTOHaVUN6AljhUgzXTSW9eaLXJ2uuzPHvR "002") 로 압축하고 서로 다른 level의 abstract에서![](https://lh3.googleusercontent.com/AWKkW01Zj62nPlhVU8SWN6MiBRGwyhFnAybYizsCp0tCjkdgRPEI2F2Dd_0Wm-kTMPqWNjq0GnsX "c2")     contextual representation으로 인코딩 하는데 이때 L-layer Transformer 사용![](https://lh3.googleusercontent.com/VQU9KaI607AFpN0WtBYd6qGVU7AVQjr3cLmcHdpZVbIcnTvy3jSJEFpzKctZapNYTKYeQbiL3FDz "c3")   
-  각 Transformer block안에는 여러개의 self-attention head가 존재하고, 그 head들이 이전 layer의 output 벡터를 aggregate함(어떻게? 코드확인)  
- l번째 Transformer layer에서 self-attention head ![](https://lh3.googleusercontent.com/1l8TUw-JR-bAXOx6RGyvs1sfy4zgYYs8LnWWT9YCifM9ZOkV422o_VrDrpZ80rL9LlNUw7M_KVQe "c4") 의 출력은 아래 식을 통해 계산됨  

(띠용 읽는 도중에 논문 업데이트 됨 아래는 원래 수식)  
![](https://lh3.googleusercontent.com/MZA4z7Il0nf6lm3xcxWVbrQMjfC5qAGeWF9QyHTekFxtXYLyd3tLoSmIVskIf0xT5PW9gZttSTUs "0")   
![](https://lh3.googleusercontent.com/LbQyXgk9NoDbpPLzOhIUUTIrDU8kXsod-SSpLkPjNBMUxmrZHvbTP1nY4SDF2ZLAxAhs7jnxASL- "01")  

(이게 조금 수정된 수식 거의 똑같음)  
![](https://lh3.googleusercontent.com/-Xd_UlHkaeLKDqxI7TQxbcxnYvh7YD0cqRu7-qJ6AMWqkEQN7FNj4EVh_VoSz1H06yxPEwrnyovL "c1")  
- 이전 layer의 output인 ![](https://lh3.googleusercontent.com/CpKvvOjCzX4YXCrv1E7WBhqZesdsRf6Ntvg_hX5S1g0joTKTZ7xWeKVg171T4OUQFsvI9LNmnToH "c4") 는 각각 매개 변수 행렬 ![](https://lh3.googleusercontent.com/T-kml37_wXpVaGET4XH2kUiYxzFWFA7IhjkVOuQGdxBgYQMYs9rLs5tOQ_qHORP5HnV98hGpY5vW "c5")  
를 이용해 query, key, value들이 3배로 linearly project되며 mask 행렬 ![](https://lh3.googleusercontent.com/n2SlmCHDid6lQ6UXsDzS2m-9fHYdrJh1bL0eyVgA1c086wxstVTH1ZvjJGEN8Ez8z_Qo3MXEO7et "c6") 은 한쌍의 token들이 서로 attended 할 수 있는지여부를 결정  
![](https://lh3.googleusercontent.com/9OxCWCThMcBncK1ZBjPxKABJqZudPUkNIZg3aFbKJqDIFFCj03htqjXcAmDLZ0bkxxa4MP4typVt "3")    
- 위 그림 처럼 contextualized representation을 계산할 때 token이 어떤 context에 영향을 줄지를 조절하기 위해 mask 행렬인 M 사용  
- bidirectional LM을 예로 들면, mask 행렬의 요소는 모두 0이며 모든 token이 서로 access할 수 있음을 나타냄  

**3. Pre-training Objectives**  
- 서로 다른 language modeling을 위해 설계된 네가지  cloze task를 사용해 UNILM을 pretain    
- cloze task에서 임의의 일부 WordPiece token을 선택해 special token [MASK]로 바꿈  
- 그다음, Transformer network에서 계산된 output 벡터를 softmax classifier을 이용해 masked token을 predict함  
- UNILM의 parameter들은 predicted token들과 original token들을 이용해 cross-entropy loss를 최소화하는 방향으로 학습 함  
- cloze task를 사용하면 모든 LM에 대해 undirectional, bidirectional 모두 같은 training procedure를 사용할 수 있음(?)(It is worth noting that the use of cloze tasks makes it possible to use the same training procedure for all LMs, unidirectional and bidirectional alike.)    
##### Unidirectional LM  
##### Bidirectional LM  
##### Sequence-to-Sequence LM  
##### Next Sentence Prediction   
- bidirectional LM같은 경우 BERT와 같이 pre-training을 위한 다음 문장 예측작업도 포함함  

**4. Pre-training Setup**  

**5. Fine-tuning on Downstream NLU and NLG Tasks**  

### Experiments  
- NLU, NLG task에 대해 실험 진행  
- NLU : GLUE benchmark, extractive question answering   
- NLG : abstractive summarization, question generation, generative question answering, dialog response generation  

**1. Abstractive Summarization**
![](https://lh3.googleusercontent.com/52WTVHoVESHBM_OVrx5vROywWLAuq7GTS_z3_pB4nKGy8x9fxcVNkKDoMWZGFVMByKCrxlgB3Svp "t1")  
  
**2. Question Answering**    
![](https://lh3.googleusercontent.com/j3LDjp7dEDDzVubmuKgjM5O74ciX6gSG5hIr8sOB5Tezinl3lsn8l8w6UlwFfJLoHCAjJMVtbZ5V "t2")  

**3. Question  Generation**      
![](https://lh3.googleusercontent.com/Q-xtZvpx9wIoxAYUKSSUHMLpudlnUx4h378_pmIxN2Wcnm-71HYfDio1lmGT2WBaNFWxiu-N_h0N "t3")   

**4. Response Generation**  
![](https://lh3.googleusercontent.com/8tczXWonXY1AENcDOVArs-4sfnFB3JHnbIntLrJRzYlT2571AZs82DeF5pXveYIDQeto7zl1FQ2g "t4")    

**5. GLUE Benchmark**  
![](https://lh3.googleusercontent.com/mKGOy05vx7gJJ8S1aQQQpf6VSe3El3K6TcuiscPuTIwc6q0lWktefcSPq7REWujM_EAKXbQ6Q9Zt "t5")    

### Conclusion and Future Work  
**Conclusion**  
- parameter를 공유함으로써 여러가지 LM objectives에 대해 최적화 된 unified pre-training model을 제안함  
- bidirectional, unidirectional, sequence-to-sequence LMs들의 통합으로 NLU, generation task에 대해 모두 사용가능한 pre-tranined 된 LM을 fine-tune할 수 있음  
- GLUE벤치마크와 두가지 question answering dataset 실험 결과에서 UNILM이 BERT보다 우세하게 나타남  
- 또한, unified pre-trained LM은 세가지 자연어 generation task들에서 (CNN/DailyMail abstractive summarization, SQuAD question generation, CoQA generative question answering) 기존 SOTA모델보다 좋은 성능을 나타냄  

**Future Work**  
앞으로 아래와 같이 작업을 진행할거임  
- 더많은 epoch와 더 큰 모델을 webscale text corpus로 학습시켜서 현재 모델의 한계를 해결할 거임  
- At the same time, we will also conduct more experiments on end applications as well as ablation experiments to investigate the model capability and the benefits of pre-training multiple LMs with the same network.  
-  현재는 단일언어 NLP task에 중점을 두고 실험을 하고 있지만, 기계번역 같은 다중언어간 작업을 지원하기 위해 모델을 통합하는 것에 관심이 있음    
- NLU와 NLG에 대해 multi-task fine-tuning를 수행 할 것임 (이는 Multi-Task Deep Neural Network (MT-DNN)의 확장)  
 
![enter image description here](https://lh3.googleusercontent.com/QqYOlVcPHO-NB2O3LVAIfsptzfbl5zq1bKmJWWotdxElh8ZjdM_5r--Zh3qJx58HGCS809XG1B3g "21")
위 표는 UNILM left-to-right generation을 이용해 Text 생성한 예시  

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5NDEzNTEwNywxMzU3NjE2MTA4LC00NT
k1ODM1MywtODg5ODcyNTI1XX0=
-->