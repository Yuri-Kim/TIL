## Improving Language Understanding by Generative Pre-Training  

Alec Radford, Karthik Narasimhan, Tim Salimans Ilya Sutskever (2018, OpenAI) [paper](https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf), [blog](https://openai.com/blog/language-unsupervised/)   

### Abstract  
- unlabeled text corpora는 충분하지만, 특정 task를 학습하기 위한 labeled text corpora는 부족함  
- 본 논문에서는 다양한 많은 unlabeled text에 대해 LM의 generative pre-training을 진행 한 후, 특정 task에 대해 fine-tunning하는 것이 효과적임을 보임  
- 이전 방식들과 달리 model architecture의 작은 수정으로 효과적인 transfer를 수행  
- (본 논문 기준) 12개 task 중 9개 task에서 SOTA  

### Introduction  


### Related Work  


### Framework  
####  Unsupervised pre-training  


####  Supervised fine-tuning  


####  Task-specific input transformations  


### Experiments  
####  Setup  


####  Supervised fine-tuning  


###  Analysis  


###  Conclusion  



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg0NTUyNDU5OSwtMTc0NDE3NDU3OF19
-->