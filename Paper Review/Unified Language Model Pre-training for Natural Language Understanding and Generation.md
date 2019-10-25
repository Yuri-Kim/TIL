
## Unified Language Model Pre-training for Natural Language Understanding and Generation  

Li Dong, Nan Yang, Wenhui Wang, Furu Wei et al. (Microsoft Research) [Paper](https://arxiv.org/abs/1905.03197)  
Source code : [github](https://github.com/microsoft/unilm)  

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
-  UNILM은 여러가지 LM task들을 사용하여 학습되기 때문에 segment embedding역시 

**2. Backbone Network: Transformer**  

![](https://lh3.googleusercontent.com/LbQyXgk9NoDbpPLzOhIUUTIrDU8kXsod-SSpLkPjNBMUxmrZHvbTP1nY4SDF2ZLAxAhs7jnxASL- "01")  

**3. Pre-training Objectives**  

**4. Pre-training Setup**  

**5. Fine-tuning on Downstream Tasks**  

### Experiments  

**1. Abstractive Summarization**
![enter image description here](https://lh3.googleusercontent.com/VH5BF1kRAOwAWC-4nN1wB-kbg1iznrVb8G694eJi6hngO8BFI_E3IAHW3ma_aZQmE2ptD08Zublk "14")  

**2. Question Answering**  
![enter image description here](https://lh3.googleusercontent.com/1DVwRt7VM94FPElQNbyEdGjbJysuGyzLIDrLgLi2kDdDSU47x-QkybfJI2-DU96jjx599g4mjAsu "15")  

![](https://lh3.googleusercontent.com/atsTyOGHLcLmZJfk3vbKGl4_2C6eYWf-F06WNTW1xwgBvmhD1ER_n_mnAB6G598PGYYIz5hUsmT2 "16")  

![](https://lh3.googleusercontent.com/64mT5qigUZZqa56_3OG8dFolpTbTyq92ZCYo2Inr11HPGz3nlAq0lC9LDc_DgVJfmLslGyNiUXAy "17")  

**3. Question  Generation**  
![enter image description here](https://lh3.googleusercontent.com/4Xcju7mdOvJWKG76dSbVxo47-XQ97YtSNimHct_-gkArCasq9LsGuKoHIAmOjqBAFtDv1i16iOti "18")  

![](https://lh3.googleusercontent.com/evyUIAAvW3_BNdnwYI-tA8I4bO-AiZXHyYCB6-9LgQOlMpdGG9jZPB0AdcPi1mELFbLqhfShK-AM "19")    

**4. GLUE Benchmark**  
![](https://lh3.googleusercontent.com/oZMiEeikhKEEqM2XSIazCl4PdbMksXSxMZHkb9fz8_S0QNZNPQn3475dorpb6xoOLHzXsMuDZrT_ "20")    

**5. Long Text Generation : A Case Study**  

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
eyJoaXN0b3J5IjpbMTM1NzYxNjEwOCwtNDU5NTgzNTMsLTg4OT
g3MjUyNV19
-->