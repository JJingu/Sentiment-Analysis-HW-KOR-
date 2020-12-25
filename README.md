### 자연어처리 감정분석 실습: 네이버영화 리뷰 데이터를 활용한 한글 데이터 감정 분석

- 실습 및 코드 수정자: 김진구
- 메일: kim.jin.gu@hanmail.net

코드원본(https://github.com/Parkchanjun/KU-NLP-2020-1)
- Transformer를 이용한 감정분석기 - 한국어 Data
- 원본 제작자: Park Chanjun (박찬준)
---



#### Overview

네이버 영화 리뷰데이터(Naver Sentiment Movie Corpus,NSMC)를 활용한 감정분석 과제(사실상 실습코드)


* 데이터 준비
* 토큰화
* 정수인코딩
* 패딩
* TRANSFORMER Class
* 학습
* 결과 비교

---

#### Data

학습데이터는 [github](https://github.com/e9t/nsmc)에서 받음

* `rating_train.txt`: 학습 데이터 총 15만개
* `rating_test.txt`: 테스트 데이터 총 5만개
* ko_data.csv
* ko_data_UTF8.txt : 캐글용 데이터를 Colab에서 변환하지 못해서 임의로 텍스트 파일로 변환하여 적용함. 

---
#### Package
필요한 패키지는 다음과 같습니.

* Konlpy
* Tensorflow
* Pandas
* Numpy
* keras
* konlpy (okt 사용)

---

#### Preprocessing

https://wikidocs.net/44249 블로그 참조해서 전처리과정을 진행하였다. 
중복제거, 불용어처리 등의 형태소 분석 및 
정수인덱싱과 패딩 적용

---

#### Training

모델은 고려대 컴퓨터학과 자연어처리에서 실습으로 사용한 코드를 기초로 하였다
코드원본(https://github.com/Parkchanjun/KU-NLP-2020-1)

embed_dim = 32  # Embedding size for each token # 원 논문에서는  512
num_heads = 2  # Number of attention heads # 원 논문에서는 8
ff_dim = 32  # Hidden layer size in feed forward network inside transformer # 원 논문에서는 2048

학습 옵션
adam, sparse_categorical_crossentropy
---


#### Result

모델에는 5에폭으로 학습

Epoch 1/5
3655/3655 [==============================] - 66s 17ms/step - loss: 0.4912 - accuracy: 0.7311 - val_loss: 0.3570 - val_accuracy: 0.8440
Epoch 2/5
3655/3655 [==============================] - 62s 17ms/step - loss: 0.3146 - accuracy: 0.8655 - val_loss: 0.3574 - val_accuracy: 0.8441
Epoch 3/5
3655/3655 [==============================] - 62s 17ms/step - loss: 0.2719 - accuracy: 0.8832 - val_loss: 0.3726 - val_accuracy: 0.8418
Epoch 4/5
3655/3655 [==============================] - 63s 17ms/step - loss: 0.2507 - accuracy: 0.8928 - val_loss: 0.3849 - val_accuracy: 0.8364
Epoch 5/5
3655/3655 [==============================] - 62s 17ms/step - loss: 0.2277 - accuracy: 0.9028 - val_loss: 0.4175 - val_accuracy: 0.8357




##### 모델 summary
Model: "model_1"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
input_2 (InputLayer)         [(None, 128)]             0         
_________________________________________________________________
token_and_position_embedding (None, 128, 32)           1566848   
_________________________________________________________________
transformer_block_1 (Transfo (None, 128, 32)           6464      
_________________________________________________________________
global_average_pooling1d_1 ( (None, 32)                0         
_________________________________________________________________
dropout_6 (Dropout)          (None, 32)                0         
_________________________________________________________________
dense_14 (Dense)             (None, 20)                660       
_________________________________________________________________
dropout_7 (Dropout)          (None, 20)                0         
_________________________________________________________________
dense_15 (Dense)             (None, 2)                 42        
=================================================================
Total params: 1,574,014
Trainable params: 1,574,014
Non-trainable params: 0
_________________________________________________________________
1537/1537 [==============================] - 7s 5ms/step - loss: 0.4253 - accuracy: 0.8322
Test_acc:  0.8322314023971558


---
