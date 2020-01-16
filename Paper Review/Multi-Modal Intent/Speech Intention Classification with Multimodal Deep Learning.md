## Speech Intention Classification with Multimodal Deep Learning

### Canadian AI, 2017

### Yue Gu, Xinyu Li, Shuhong Chen, Jianyu Zhang, Ivan Marsic

[Paper Link](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6261374/)

---

**얻고자 하는것** (multi-modal 사용에 대한 기본 개념 얻기)

음성 정보를 feature로 어떻게 뽑는지 

다른 정보와 fusion을 어떤식으로 하는지

그거에 대한 기존 연구가 뭐가있는지 

---

이 페이퍼는 general action-based intention recognition을 진행 

- 6개 intention

- textual, acousitc features 사용 

- CNN(VGG Net)사용

- dataset은 직접 구축 

  - dataset domain : 외상 시나리오에서 환자의 intention

    (Trauma-related language contains rich used for the detection of medical processes)

### Intro

- 기존 intention 연구는 대부분 text feature만 사용
  - pitch toner, stress pattern, rythm 등의 음성적 정보를 고려하지 않음
  - 문장구조가 복잡하지 않은 이상 음성정보를 무시할 이유가 없다 → textual, acoustic 모두 고려하겠다

### Related Work

여러 type feature combine하는 연구들

[11] audio + text 초창기 연구

[12] audio + vidio + text : dataset 어케 활용했는지 확인 해봐 / visual feature가 성능을 올렸대

[13, 14] 최근 ConvNet(visual + text feature) 활용한 연구 많음 / dataset 확인 (검색 keyword : multi modal ~ dataset로 찾아보기 ex. multi modal opinion dataset)

[14] 기존 연구가 음성 feature를 자동 추출하지 않았다는 점 → 이 연구는 음성&text 둘 다 ConvNet으로 자동 추출할거다! 

### Dataset

- 직접 수집 (record on a mono channel with 16000 Hz sampling rate) & labeling (6개)
- 수집 후 문장 단위 cut → 6424 문장 + 오디오 clip
- 80 : 20 = train : test → 83.10 accuracy

### Model

- ConvNet이 제공하는 feature가 manufactured feature보다 나은 성능을 보임

#### Data Preprocessor

- 초기화 방식 : text → word vectors / audio → MFSC Maps

**Text** (**dim : 26 * 300** sentence length by word-vector length)

- 26 : max sentence length (더 짧은거는 0으로 채움 zero-padded)
- 300 : 각 단어는 300 * 1의 vector로 embedding (pretrained word2vec skip-gram, unknown word : initialized ramdomly)

**Audio** (**dim : 64 * 256 * 3**)

- 보통 speech recognition에서 주로 사용하는 MFCCs대신 MFSC사용 (∵DCR 피하려고)
- 각 오디오 클립에 대해 static, delta, double delta MFSC 추출
- 0 - 8000Hz → 64개 주파수 대역으로 나눔 
- 64 * n MFSC Maps for n-second clip → 모든 MFSC Map은 64 * 256(bicubic interpolation)으로 rescale

#### Feature Extractor

**Text**

![An external file that holds a picture, illustration, etc. Object name is nihms-993283-f0002.jpg](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6261374/bin/nihms-993283-f0002.jpg)

- size 1, 2, 3인 필터 사용 (∵ domain 자체가 문법 안맞거나 문장이 짧음)
- 1 Conv layer & 1 max-pooling layer
- 각 필터 결과 300 feature map → max pooling → 900 dimensional feature. vector (acoustic feature(1024)와 비슷하게)

**Audio**

![An external file that holds a picture, illustration, etc. Object name is nihms-993283-f0003.jpg](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6261374/bin/nihms-993283-f0003.jpg)

- 8 layer ConvNet
- MFSC map에서 audio feature 추출
- 3 * 3 convolution, 2 * 2 max-pooling filters with zero padding
- 더 깊게 학습 안한 이유 : HW 제약 때문에

#### Feature Fusion Layer

- FC layer를 통해 feature fusion (feature-level fusion)
  - data-level fusion이 아닌 feature-level fusion을 사용한 이유
    1. ConvNet 구조로 음성 & 텍스트 feature 모두 추출하기 때문에 feature-level fusion에서 2가지 data를 융합할 필요가 없음
    2. 선행 연구[14]에서 둘 다 해봤는데 featrue-level fusion이 성능이 더 좋아서 사용

#### Decision Making

- dicision → softmax layer
- 1924 dim feature vector from fusion layer
  - ∵ 실험 결과 제일 좋음, HW 제약 때문에 그냥 softmax만 사용

![An external file that holds a picture, illustration, etc. Object name is nihms-993283-f0001.jpg](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6261374/bin/nihms-993283-f0001.jpg)

#### Implementation

- keras 사용
- learning rate = 0.01
- Adam optimizer(minimize loss)
- drop-out func & 5-cross validation drop-out (to avoid overfitting)

### Evaluation Results

![](https://lh3.googleusercontent.com/5bVjukeX5MiJrtp7kh046Lzeu3Hixy-t3OCORO4B3MLu_QL6wkkoCQmHEXeKiahMq7I55kAjDnBQ "table1")

- CNN_T : Q, CL 같이 의문을 나타내는 class 잘 구별
- CNN_A : 다른 speaking manner를 나타내는 class 잘 구분 (Q, DIR, RS, RP)
  - 두 데이터 유형은 서로를 상호 보완
- RP class 성능이 상대적으로 낮은 이유 : 문장 내용이 다양하고, 다른 class랑 음향적으로도 비슷해서 (즉, textual autical feature 둘 다 특징이 적음)
  - ex. 강조할 때 말끝을 올림 → 의문 나타내는 class랑 비슷함

![An external file that holds a picture, illustration, etc. Object name is nihms-993283-f0004.jpg](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6261374/bin/nihms-993283-f0004.jpg)



![](https://lh3.googleusercontent.com/ctfrro6Y8_QdrA_Gf5efpmUCDtvZ4_ppf9kZQpsYjo9GAHIVWndVWC95NX6rg6pgXuHmAgOFCM4p "table2")

### References

[11] Chuang ZJ, Wu CH : Multi-modal emotion recognition from speech and text. Comput. inguist. Chin. Lang. Process. 9(2), 45-62 (2004)

[12] Poria S, Cambria E, Howard N, Huang G-B, Hussain A : Fusing audio, visual and textual clues for sentiment analysis from multimodal content. Neurocomputing 174, 50-59(2016)

[13] Poria S, Iti C, Erik C, Amir H : Convolutional MKL based multimodal emotion recognition and sentiment analysis. In: ICDM (2016)

[14] Poria S, Cambria E, Gelbukh A : Deep convolutional neural network textual features and multiple kernel learning for utturance-level multimodal sentiment analysis. In : Proceedings of 2015 Conference on Empirical Methods in Natural Language Processing (2015)

### Appendix

- PPT정리본 - 200103 보고자료 참고
