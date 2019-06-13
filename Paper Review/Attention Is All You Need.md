
## Attention  Is All You Need  

Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N.Gomez, Lukasz Kaiser, Illia Polosukhin (NIPS 2017) [paper](https://arxiv.org/abs/1706.03762)  

### Abstract  
- 현재 대부분의 sequence model은 RNN, CNN을 encoder와 decoder로 활용함  
- 가장 좋은 성능을 보이는 모델 역시 attention mechanism을 활용한 encoder, decoder모델  
- 본 논문에서는 CNN과 RNN을 없애고 attention mechanism에만 기반을 둔 새로운 모델인 Transformer를 제안 함  
- 이를 통해 paralleizable익 가능해졌고, train시간이 감소 됨  
- 2개의 machine translation 실험 결과 좋은 성능을 보였음  

### Introduction  
- RNN과 LSTM, GRU는 sequence modeling과 machine translation에서 SOTA  
- RNN은 input sequences와 output sequences들의 position을 계산하는데 뛰어남  
- position 순서대로 연산을 하면서 이전(t-1) position의 hidden state $$h_{t-1}$$ 값과 현재 position에서의 input t를 통해 현재의 hidden state $$h_{t}$$를 만들어 냄  
- 따라서 구조상 sequential한 특성을 가짐  
- 이는 paralleization에 취약 → sequence 길이가 길어진 경우 batch로 풀고자 할 때 문제가 될 수 있음  
- 최근 연구에서 factorization trick와 conditional computation을 통해 계산 효율성을 크게 향상 시켰음 → 하지만 sequential computation의 근본적 문제가 여전히 남아있음  
- attention mechanism은 input sequence, output sequence의 길이에 관계없이 dependency를 모델링 할 수 있게 해줌 → sequence model에 필수적이 요소가 됨  
- 아직 대부분 RNN과 결합하는 형태로 쓰임  
- 본 논문이 제안하는 모델인 Transformer는 전적으로 input, output의 global dependency를 끌어내는 attention mechanism에 기반  
- Transformer는 훨씬 더 많은 병렬처리가 가능하며 속도도 빠름    

### Backgound  
- sequential한 연산을 줄이기 위해 Extended Neural GPU, ByteNet, ConvS2S 등이 생겼는데 모두 hidden representation을 parallel하게 계산 하기 위해 CNN 활용  
- 이 모델들은 input과 output을 연결하는데 많은 연산이 필요(ConvS2S는 선형적으로(linearly, ByteNet은 대수적으로(logarithmically) position간 거리 증가) → 멀리 떨어져 있는 position끼리의 dependency들을 학습하는 것이 어려움  
-  Transformer는 attention-weighted position을 평균을 취해 줌으로써 effective를 잃었지만, 이 operation의 수가 상수로 고정되며 줄어듦  
- self-attention(intra-attention)은 seq representation을 얻고자하는 하나의 시퀀스에 있는 다른 position을 연결해주는 attention기법 (reading comprehension, abstractive summarization, textual entailment, learning task-independent sentence representations등에서 활용)  
- sequence aligned recurrence대신 recurrent attention mechanism를 기반으로 한 end-to-end memory network는 simple- language question answering과 language modeling tasks에서 좋은 성능을 보임  
- 하지만!! 우리의 Transformer는 RNN이나 CNN없이 self-attention만으로 representation을 구현한 최초의 모델임!!!

### Model Architecture  
- neural sequence transduction model 중 가장 뛰어난 모델은 encoder-decoder 구조 활용  
- encoder가 symbol representation을 갖고 있는 input sequence(x1, x2, ... , xn)를 연속적 representation(z1, z2, ... , zn)으로 변환  
- decoder는 그 z를 가지고 순차적인 symbol을 가진 output sequence(y1, y2, .... , ym) 생성 (한번에 one element씩)    
- 각 step에서 다음 symbol 생성 할 때 이전 generated symbol(output)를 추가입력으로 이용 (ex. "나는 사람이다."에서 '사람이다.'를 생성할 때 '저는'이라는 symbol을 이용 → auto-regressive하다고 표현)  

![
](https://lh3.googleusercontent.com/fpwQvGT8e3ufYD2bS0YHCFetcSwhNtIcr1x69elQpuAxMdGYAe8Gy09XSHY5hDKMp9H0JcjZBOmu "model architecture")  

- Transformer는 위와 같은 구조  
- self-attention이 stacked 되어있으며 encoder, decoder모두 fully-connected layer를 가짐  

#### 3.1 Encoder and Decoder Stacks  
- **Encoder**  
	- N=6개의 똑같은 layer로 (stacked) 구성, 각 layer는 두개의 sub-layer를 가짐  
	- sub-layer는 multi-head self-attention mechanism과 position-wise fully connected feed-forward network를 가짐  
	- 각각의 sub-layer에 대해 residual connection을 사용한 후 layer nomalization을 적용  
		- residual connection? : input을 output으로 그대로 전달하는 것. 이때 sub-layer의 output dimension을 embedding dimension과 맞춰줌 ∵ x + Sublayer(x)를 하기 위해 → residual connection하기 위해  
	- 각 sub-layer의 output은 LayerNorm(x + Sublayer(x))  
	- residual connection을 편하게 해주기 위해 모든 sub-layer는 512 차원 output을 생성하도록 함  

- **Decoder**    
	- decoder역시 N=6개의 똑같은 layer로 (stacked) 구성  
	- encoder와 다르게 두개의 sub-layer (multi-head self-attention mechanism과 position-wise fully connected feed-forward network) 이외에도 multi-head attention을 수행하는 sub-layer추가  
	- encoder와 마찬가지로 각각의 sub-layer에 대해 residual connection을 사용한 후 layer nomalization을 적용  
	- 또한, decoder의 self-attention sub-layer를 수정하여 이전의 position을 후속되는 position에서 참조하지 못하도록 함(masking 함) ∵ decoder는 encoder와 다르게 순차적으로 결과를 만들어 내야 하기 때문  
		- 아래 예시를 보면 "abc"라는 순차적인 데이터가 있을때, a 예측 시 a이후 b, c에는 attention 안줌, b 예측시 b이전 a만 attention, b 이후인 c에는 attention 안줌  
		![
](https://lh3.googleusercontent.com/ICignM-L0NWwgMmZ_gkZ192TOXCGVM036DDZufWlpDKKMoKLFtfvE4_vg611cCNoKRzic-v6MdOM "2")  

#### 3.2 Attention  
- attention은 query, key-value pair를 output에 매핑하는 함수  
- query, key, value, output은 모두 vector  
- output은 value들의 가중합으로 계산되며 여기서 각 value들의 가중치는 해당 key의 compatibility function을 통해 계산 됨     

**3.2.1 Scaled Dot-Product Attention**  
![
](https://lh3.googleusercontent.com/ZUvuc7STXrnSuXsY5VDAaR46KJlXAKy0Gwtcnc99EYNvNUDCVQDSOlezl8abnT3bHFTtmPOXOwIz "3")  
- 본 논문의 attention을 Scaled Dot-Product Attention이라 함   
- input은 dk dimension을 갖는 query, key들, dv dimension을 갖는 value들  
- 이때 모든 query, key에 대해 dot-product 계산 후 각각을 √dk 로 나눠줌 (dot-product 후 √dk로 scaling을 해주기 때문에 Scaled Dot-Product Attention) 그 후 에 softmax를 적용해 value들에 대한 weight(어디에 attention 할 지)들을 얻어냄  
	- key, value는 attention이 이루어지는 위치에 상관없이 같은 값 가짐  
	- 이 때, query, key에 대해 dot-product를 계산하면 각각의 query, key 사이의 유사도를 구할 수 있음(ex. cosine similarity : dot-product/vector의 magnitude)   
	- √dk로 scaling을 해주는 이유는 dot-products의 값이 커질수록 softmax함수에서 기울기의 변화가 거의 없는 부분으로 가기 때문  
	- softmax를 거친 값을 value에 곱해주면, query와 유사한 value일수록(중요한 value일수록) 더 높은 값을 가지게 됨 → 더 중요한 정보에 관심을 주자는 attention의 원리에 맞음!  
- 우리는 query들을 동시에 계산해서 matrix Q로 묶음  
- key, value들도 matrix K, V로 묶음  
- output 계산은 아래와 같이 진행  
![
](https://lh3.googleusercontent.com/LdUOY_sLIJctnCuSTlolWWCELbwcG8IWw-5L9dSMZrCB8Zvbww_Hkyb7Hqr4_GYSnG9g5BCbGPdU "4")  

**3.2.2 Multi-Head Attention**  
![
](https://lh3.googleusercontent.com/DyezM3UMSXdqI5J6GOAqhHO693qh3YIBIfooIh6vBfjMO_N1Fs2zLPsIdJ8Ql7T3VcQR_YXJqH_K "5")  
- 위 그림을 수식으로 나타내면?  
![
](https://lh3.googleusercontent.com/lsPHKM3e8qtnetLhCK-fZpV00KytczKbuDeUlucCfoOXQ7JVSs2us-QrVfjNWCeG0qxMG6MtDXLW "6")   

![
](https://lh3.googleusercontent.com/em_nDSHNJdLWNUnMcsg4upWfNiYzcQTUxHrPfHkpA2AxxaWCrU_u22lF_x4MNTSYvYExkLimuzME "7")   

- d_model dimentsion의 query, key, value들로 하나의 attention을 수행하는 것 보다 query, key, value에 대해 각각 다른 학습된 linear projection을 h번 수행하는 것이 더 좋다!  
- 즉, 동일한 Q, K, V에 각각 다른 weight matrix W를 곱해줌 (이 때 parameter matrix는 위 그림과 같음 순서대로 query, key, value, output에 대한 parameter matrix)     
- projection이라고 하는 이유는 각각의 값들이 parameter matrix와 곱해졌을 때 dk, dv, d_model 차원으로 project되기 때문(본 논문에서는 dk = dv = d_model/h 사용했지만, 꼭 dk=dv일 필요는 없음)  
- 이렇게 project된 key, value, query들은 병렬적으로 attention function을 거쳐서 dv dimension output 값으로 나옴  
- 그 다음 여러개의 head를 concatenate 하고 다시 projection수행 → 최종적인 d_model dimension ouptut값 나옴  
![
](https://lh3.googleusercontent.com/XVcr1PfWqQVl0qWqfqaeYcWfIguQarZ7eOuVn0CLtUBoMiBhv8MxaigHuxj5Vv_2SoyU9D3gL-9O "8")  

- 각각의 과정에서 dimension 표현하면 위 그림과 같음  

**3.2.3 Applications of Attention in our Model**  
- 여기서 부터는 앞으로 정리 할거임! 

#### 3.3 Position-wise Feed-Forward Networks  

#### 3.4 Embeddings and Softmax  

#### 3.5 Positional Encoding    

### Why Self-Attention  

### Training  
**5.1 Training Data and Batching**  

**5.2 Hardware and Schedule**  

**5.3 Optimizer**  

**5.4 Regularization**  

### Results  
**6.1 Machine Translation**  

**6.2 Model Variations**  

**6.3 English Constituency Parsing**  

### Conclusion  


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk1MTkyOTg0LC02NzU0MzM5NDIsMjA1Mz
Y0NDE2OCwtMTgxMjk5NDkzMV19
-->