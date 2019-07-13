## BERT : Pre-training of Deep Bidirectional Transformers for Language Understanding  

Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova (Google AI Language, 2018) [paper](https://arxiv.org/pdf/1810.04805.pdf)  

### Abstract    
- BERT : Bidirectional Encoder Representation from Transformers  
- 모든 layer에서 양방향으로 학습  
- pre-trained model에 layer 하나만 추가하여 11개 task에서 SOTA  

### Introduction  
- Language model pre-training은 많은 NLP task를 향상시키는데 효과적  
- 예를 들면, natural language inference, paraphrasing 같은 sentence-level task와 개체명 인식, question answering 같은 token-level task를 수행 할 수 있음   
- downstream task에 pre-tained language representation을 적용하는 방법은 두가지 존재  
	- **feature-based (ex. ELMo)** : task-specific architecture (추가적인 feature로 pre-trained representation 사용)    
	- **fine-tuning (ex. GPT)** : task-specific parameter를 최소화, pre-train된 parameter에 대해 fine-tunning하며 downstream task를 학습함
	- 위 두가지 방법은 pre-train 된 para

### Related Work  


### BERT  

### Experiments  

### Ablation Studies  

### Conclusion  

#### Appendix  
- Transfer Learning : 기존의 만들어진 모델을 사용하여 새로운 모델을 만들때 학습을 빠르게 하고 에측을 더 높이는 방법 → 이미 잘 훈련된 모델이 있고 해당 모델과 유사한 문제를 해결 할 때 transfer learning 사용    
- 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTI0MjQxNjhdfQ==
-->