
## Neural Text Summarization Model  

Presenter : 전동현(NAVER)  

### Text Summerization Approaches  
추출 요약 (Extractive Summarization)  
- 문서에서 중요한 문장을 선택하고 추출하는 방식  
- 정확한 정보 전달  
- 가독성 및 간결함 부족, 문장 분리 필요

생성 요약 (Abstractive Summerization)  
- 문서에서 핵심 word들이나 phrase들의 조합 또는 적절한 표현으로 paraphrasing하는 방식  
- 자연스러운 내용 연결, 가독성 및 간결함  
- 부정확한 정보 생성 가능성  

( ex. 지식IN 본문 → Summarizer → 지식IN 질문 제목  
뉴스 본문 → Summarizer → 뉴스 제목 )

---  

### 생성 요약 모델링
1. Baseline models : Attentional Seq2Seq Model  
- NMT 모델에서 사용되던 RNN 계열의 Encoder-Decoder 형태에서 시작  
- Decoder는 Beam search를 사용  
![
](https://lh3.googleusercontent.com/T2hew2NkrZxX-eQSbqS_SUHJLldHQHOUgKswSoF9kECXL6RBNNje8q6_iYXupXtkETe9ZQQRf5Am "NTSM1")  
(A. See, "Get to the point : Summerization with pointer-generator networks", ACL, 2017 [Paper](https://arxiv.org/abs/1704.04368) )  

- Main problem  
	- Vocabulary에 없는 단어 잘못된 생성 → Germany beat Argentina 3-2 ...  
	-  Decoder 단어 반복 (decoder's over-reliance on the decoder input) → Germany beat Germany beat Germany beat ....  

2. Pointer-generator Model (추출 + 생성 hybrid)  
- Attention Seq2Seq model에 Copy mechanism(pointer network) 및 Coverage mechanism 적용  
	- Copy mechanism : 문서에서 특정된 단어들(e.g. Named Entity 등)은 그대로 추출해서 요약문에서 활용 → Out-of-vocabulary로 인해 부정확한 재현 문제를 해결
	- Coverage mechanism : 현재까지 사용되었던 단어 분포 누적값 coverage vector를 통해 반복적으로 등장한 단어에 대한 penalty을 loss에 반영하여 활용 → 단어 반복 문제를 해결  
![
](https://lh3.googleusercontent.com/4M63I4Kh6svVJZtvfzxtf8snLyWd-sHNf6V44zG11baYwO1__0nvliFIxWQuTyQM9SrGCggMH14Z "NTSM2")  

$$
P_{final}(w) = p_{gen}P_{vecab}(w)+(1-p_{gen})\Sigma_{i:w_{i}=w}a^t_{i}
$$ 

생성 부분  
$p_{gen}P_{vecab}(w)$  
추출 부분    
$(1-p_{gen})\Sigma_{i:w_{i}=w}a^t_{i}$  
  
생성 확률  
$p_{gen}=\sigma(w^T_hh^*_t+w^T_sS_t+w^T_xx_t+b_{ptr})$  

\+ Coverage penalty  
$covloss_t=\Sigma_imin(a^t_i,c^t_i)$  

- Pointer-generator Model의 문제점  
	- Coverage loss로 줄이긴 했지만, 단어 반복 이슈  
	- UNK 처리 이슈  
	- 비문생성 이슈  

- 후처리  
	- 디코딩 시 N-gram repetition avoidance + length penalty 추가  
	- [UNK]는 source에서 attention이 가장 높은 단어로 대체  
	- NSML의 AutoML 이용해 hyper-parameter 튜닝  

### 모델링 관련 기타 시도한 것  
1. Trasformer 기반의 Pointer-generator  
	- 생성적인 부분을 보완하기 위해 Pointer-generator Model에서 seq2seq 모델을 Transformer model로 바꿈 → Inference time 느려짐    

2. 추출 요약을 활용한 Hierarchical 생성요약 적용  
	- 네이버 내부 추출요약기 활용  

3. 추가적인 Feature Embedding 활용  
	- Morphological Feature Embedding 활용(POS tag)  
	- ELMo 적용 (large, small 버전 테스트) → Inference time 약 10배 증가  

4. Pre-trained word embedding 적용  
	- FastText 활용  

5. Word Piece Model (BPE) 적용  
	- Subword tokenization  

6. Curriculum learning 적용  
	- 길이가 짧은 데이터 부터 학습  

7. 강화학습 적용 → ROUGE 점수를 기준으로 feedback을 주기 때문에 human evaluation이 좋지 않음  
 
### Future Works  
- ROUGE 점수가 믿을 만 한가?
	- Human Evaluation 필요  
- 부정확한 정보 생성 보완  
	- Article → Content Selector (Include / Not include) → Word-level extractioin → PG based Summarizer → Summery  
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg5NDI3NjQ1NCwyODA5ODA2MzIsLTY3NT
gyMjY2MF19
-->