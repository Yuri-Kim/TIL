
## Improving Language Understanding by Generative Pre-Training  

Alec Radford, Karthik Narasimhan, Tim Salimans Ilya Sutskever (2018, OpenAI) [paper](https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf), [blog](https://openai.com/blog/language-unsupervised/)   

### Abstract  
- unlabeled text corpora는 충분하지만, 특정 task를 학습하기 위한 labeled text corpora는 부족함  
- 본 논문에서는 다양한 많은 unlabeled text에 대해 LM의 generative pre-training을 진행 한 후, 특정 task에 대해 fine-tunning하는 것이 효과적임을 보임  
- 이전 방식들과 달리 model architecture의 작은 수정으로 효과적인 transfer를 수행  
- (본 논문 기준) 12개 task 중 9개 task에서 SOTA  

### Introduction  
-  labeled text data의 부족과 labeled text data가 충분하더라도 unlabeled text data로 더 나은 성능이 나올 수 있다는 기대가 있음  
- 하지만, unlabeled text data로 word-level 이상의 정보를 활용하는 것은 아래 두가지 이유로 인해 challenging함  
	- transfer하기에 적합한 text representation을 효과적으로 학습하기에 어떤 optimization objective가 효과적인지 불분명 (최근 language model, machine translation, discourse coherence 등 다양한 objective가 연구되어 옴)  
	- 이렇게 학습된 representation이 target task로 transfer할 때 어떤 방법이 가장 효과적인지 의견일치가 되지 않음 (그래서 모델 구조를 task에 맞게 수정하거나, 복잡한 learning scheme를 거치거나, 부가적인 learning objective를 추가하는 방법이 존재)  
	- →이러한 불확실성이 semi-supervised learning을 어렵게 함  
- 본 논문에서는 unsupervised pre-training + supervised fine-tunnig을 결합해서 language understand task에대한 semi-supervised approach를 연구  
- 다양한 task에 적용가능한 universal representation을 학습하는 것이 목표  
- 본 논문에서 저자는 two-stage 학습 과정을 적용  
	- unlabeled data로 language model objective에 대해 model을 학습시킴  
	- 그리고 target task를 위한 supervised objective로 parameter를 fine-tunning (모델 구조는 transformer 사용)  

### Related Work  
#### Semi-supervised learning for NLP  
- 초기의 연구들은 unlabeled data를 word level이나 phrase level의 통계를 계산하기 위해 활용 했고, 이 값이 supervised model의 feature로 사용됨  
- unlabeled copora로 학습 시킨 word embedding을 활용해 다양한 task의 성능을 향상 시킴 → 이런 방식은 word level의 정보를 주로 전달하기 때문에 더 higher level의 의미를 전달하는 것을 목표로 하게 됨  
- 그래서 최근에는 sentence-level embedding을 적용하는 방식이 연구되어 옴  

#### Unsupervised pre-training  
- Unsupervised pre-training의 목적 : 좋은 initialization point를 찾는 것  
- 최근 연구에서 image classification, speech recogmition, entity disambiguation, machine translation등 다양한 task에서 이 방식 사용될 수 있음을 보여줌  
- GPT 연구와 가장 유사한 연구는 ULMFit와 Semi-supervised sequence labeling  
- LSTM model은 prediction능력을 short range로 제한하지만, transformer구조는 더 긴 길이의 언어에 대해 사용할 수 있음  
- GPT는 transfer할 때 model architecture의 아주 작은 수정만 하면됨  

#### Auxiliary traning objectives  
- 보조적인 unsupervised training objectives를 추가하는 것도 semi-supervised learning의 form중에 하나  
- 본 논문의 저자 또한 auxiliary objective를 사용한 실험을 해 보았지만, unsupervised pre-training이 이미 타겟 task에 충분히 학습되어 있었음  

### Framework  
첫번째 단계에서 high-capacity language model을 학습하고, 두번째 단계에서 특정 task에 대해 labeled data로 fine-tunning을 진행  

####  Unsupervised pre-training  
unsupervised 코퍼스의 token ![
](https://lh3.googleusercontent.com/ITBWFVLU4Rrdk8GB6dxs0cW4Bo5R25_Yf5nGm6_7NwATt_TKq2ursT6um9zV2y7hxDjRlyWoIHy3 "1")가 주어지면, likelihood를 최대화하는 standard language modeling objective 사용  
![
](https://lh3.googleusercontent.com/SJ1VYKY4LWWUGV5QAEEFKwQ3IEiJDi0pks77IXvo5Wystd9i_c9JF3doBc6DcZntKZmL23r_mfng "2")  
이 때, k : context window 크기 / θ : Nural network의 parameters (parameter들은 stochastic gradient descent이용하여 학습)    
Language Model에서는 multi-layer Transformer decoder를 변형하여 사용  
![
](https://lh3.googleusercontent.com/QXxopV4GZRFTDZRwDpN0Pfwrc_-1cniRh2i4QoOIUb0mM8wqNCx2k3LZJ0lUTm6KQX2zkU8H9MMV "3")
U : token의 context vector / n : layer 개수 / W_e : token embedding matrix / W_p : position embedding matrix  
위와 같을 때, 다음의 구조를 가짐  
![
](https://lh3.googleusercontent.com/z0uMqkxnuXPhXhVZGXfetR85GVQTnPTrVE8W1OGFS2eG8ZOwpjC-nLz1W0Yf1Qnmb_XvrcEBbBnN "4")  

####  Supervised fine-tuning  
Language Model objective에 대해 model을 pre-training 한 후, Labeled dataset C를 갖는 target task에 대해 parameter조정  
input token인 x ^1, ... ,  x ^m에 해당하는 label y를 예측할 때, 위 모델의 마지막 transformer 블록의 activation h_l ^m을 input으로 하는 linear layer 추가  
![
](https://lh3.googleusercontent.com/UUmpw7Cj32ESkFUVKOUqQUBr9K2tYsD16P0-OzI8a-xn-WjbdRF17N0iP9cgjlMdl2utoxqA3XWd "5")  
즉, 아래 layer가 최대가 되도록 학습  
![
](https://lh3.googleusercontent.com/y-phzzT4o5-Tic2TA9eSiMoY7MbuR6B3V3G60L5LBks3OXIYAG5DnwCO6eIO2f2ozkyXTIS3enwo "6")  
추가적으로 fine-tunning에 auxiliary objective로 LM을 포함하는 것이 supervised model의 generalization을 향상 시키고 model이 빠르게 수렴 할 수 있도록 해 학습에 도움을 줌  
즉, 아래의 objective를 최적화  
![
](https://lh3.googleusercontent.com/_u8hQTslbjXFKDD6lL4dWRsivsJv0K2ttu_Ivlatu6gbptgMqwJl8DnUl8FbxPeyTuEgKoXPcabl "7")  

####  Task-specific input transformations  
![
](https://lh3.googleusercontent.com/iPcTt3O8jLpD5K_8pIeiqJxei5VbMTKbWfSvapvxLit6dMUTvD7mRh722HKb7u3J6C9KD-02NcKZ "8")  
- 위에서 언급 했듯, text classification같은 일부 작업에 대해 model을 fine-tune할 수 있음  
- input이 질의 응답 같은 경우 순서가 있는 문장 쌍, 혹은 문서/질문/답변의 triplet일 수 있음  
- 즉, GPT모델을 사용할 때는 하고자 하는 Task에 맞춰 모델을 구성해줘야 함  

### Experiments  
####  Setup  
- pre-training data로 BookCorpus dataset 사용  
- model은 BPE(byte pair encoding) 사용 / activation function으로 GELU(Gaussian Error Linear Unit) 사용  
- BookCorpus내의 raw text를 clean하기 위해 ftfy library 사용 / 일부 구두점, 스페이스 표준화 / spaCy tokenizer 사용  

####  Supervised fine-tuning  
실험에 사용한 dataset  
![
](https://lh3.googleusercontent.com/MjLgZrirf3q92ViuHVzOLPVks_JVEHrHqwiV14jsfbUSHwmqiBdOX5f-cki9Fi1Bqi5r9ffk7cxY "dataset")   
실험 결과  
![
](https://lh3.googleusercontent.com/pUAmh0FGpOxYz2x1zZ-_wF-0Ri6r4f5xqbbme6rPJa1zGYLYIYibvY026gxqx2PSVxLoo1HDd63t "9")  
![
](https://lh3.googleusercontent.com/DaAhH75WuVlm0G5CEKOi87Dq4xebs3hL-PYgGyxM-S1ZI1br-xTrDiHgcqlDzTu2OHidVgjGdY3d "10")  

###  Analysis  
#### Impact of number of layers transferred  
![enter image description here](https://lh3.googleusercontent.com/XeXwIxyWxcLCZ6Kcgz_2C4Q5Vj8erfgTbWjFxAWVAEZ9NSR5KG9FheCZwl9SZNsE6T6rwlqyef2q "11")    
- 왼쪽 그래프 : Transformer Decoder 갯수에 따른 accuracy 변화  
	- RACE, MultiNLI : dataset
	- RACE : Question Answering(QA)를 목적  
	- MultiNLI : textual entailment 또는 Natural Language Inference(NLI)를 목적으로 함  
	- 두 데이터 셋 모두 Layer 수가 많아질수록 정확도가 비약적으로 상승(12개정도에서 정확도가 Converge하는듯 함)  
- 오른쪽 그래프 : 점선(Transforemr대신 LSTM사용)과 실선(Transformer사용)으로 Transformer의 사용 유무에 따른 차이를 보여줌  
	- 각 색상은 task를 나타냄  
	- task별로 증가율의 차이는 있지만, 모두 상대적으로 performance가 증가  

#### Zero-shot Behaviors  
- 본 논문에서는 근본적인 generative model이 LM capability를 향상시키기 위해 많은 task를 수행하는 법을 배울 수 있고 LSTM보다 Transformer의 attention memory가 transfer에 도움이 된다고 가정  
- 위에 있는 오른쪽 그림에서 확인 할 수 있듯 LSTM은 higher variance를 보이는 반면에 Transformer는 transfer에 도움이 됨  

#### Ablation studies  
![enter image description here](https://lh3.googleusercontent.com/0l1ascb4Ftv-QeLoRkN6-ExA7PXuOHIsgYQXDM0dppwVd2H50g3L1JH5U_2ToQXBCUQnvs8rDQqp "12")

- 위 표에서는 Auxiliary Objective(sub-task)가 있을 때 / 없을 때 그리고 pre-training이 없을 때의 성능을 보여줌  
- 위 결과는 왼쪽 4가지와 오른쪽 4가지 task 결과가 다른데 이것은 dataset size가 다르기 때문 → 즉, Dataset이 클수록 (QQP, MNLI, QNLI, RTE) auxiliary task가 성능 개선에 여향이 더크고 / 작을수록 (CoLA, SST2, MRPC, STSB) auxiliary task없이 학습하는 것이 오히려 성능에 도움이 됨  
- Transformer사용 여부에 대한 성능평가도 측정, 모든 경우에 LSTM대신 Transformer를 사용하는 것이 성능 개선에 도움이 됨  
- pre-training 유무에 대한 성능평가에서는 full 모델에 비해 pre-training이 없을 때 전체적으로 성능이 매우 감소(pre-traning을 안한다? → unsupervised pre-training 구조를 모두 넘겨버리고 supervised 부분만 사용)  

###  Conclusion  
- generative pre-training과 discriminative fine-tunning을 통해 task-agnostic model로 강력한 NLU를 성취할수 있음을 보임  
- 연속된 long sequence text로 이루어진 다양한 코퍼스로 pre-train함으로써, 모델이 상당한 world knowledge와 long-range dependencies를 해결할 수 있음을 보임  
- 사실 GPT-1은 BERT에 비해 그리 주목받지 못함
- 이유는, 우선 BERT가 범용적으로 쓰이기 더 용이하다는 점, 그리고 성능면에서도 BERT에 비해 좋다는 소식이 들리지 않기 때문도 있음(SQuAD 1.1이나 2.0을 살펴보면 GPT에 대한 성능 결과가 아무것도 없음)
- 하지만 그럼에도 불구하고 이 논문을 살펴봐야 할 이유 : Decoder로서 Transformer를 Pre-trained Language Model생성에 어떻게 사용하고 있는가에 대한 좋은 예시가 바로 GPT이기 때문. 많은 부분이 BERT와 비슷해도 이 점 하나는 알아갈만한 점으로 보임. (그리고 사실 BERT와 GPT-1은 많은 부분이 유사)

### Appendix  
- BERT와 비교 (아래 차이점을 제외하면 거의 유사)    
- LM pretraining 후 fine-tunning방식이 어떻게 등장하였는지에 대해 GPT(본 논문)에서 자세히 설명하고 있음  

| BERT | GPT |  
|--|--|  
| masked Im 사용 | 일반적인 lm 사용 |  
| transformer encoder 사용 | transformer decoder 사용 |  
  
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNTQwMzAxMDMsMTg0NTUyNDU5OSwtMT
c0NDE3NDU3OF19
-->