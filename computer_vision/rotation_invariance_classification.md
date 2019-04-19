## 회전에 강건한 이미지 분류

</br>

</br>

### Image retrieval
* 사전학습없이 주어진 데이터셋(책 페이지) 안에서 가장 유사한 이미지를 반환 à 정확도가 90%이하가 대부분. Annotation의 어려움 해결을 위해 주로 수행 

* 회전과 조도 변화에 강건

</br>

### 방법

*  Attentive Deep Local Feature 이용 (suitable for large-scale image retrieval) -“Large-Scale Image Retrieval with Attentive Deep Local Features(2017)” 

  : 추출된 feature에 attention을 적용해 keypoint를 추출 

* BoW (bag of words) – “CNN Image Retrieval Learns from BoW: Unsupervised Fine-Tuning with Hard Examples(2016)”

* Image embedding – “Hyperbolic Image Embeddings (2019)”

  : 구 공간에 이미지를 임베딩하여 cosine 유사도로 비교 

  : few-shot learning, retrieval 가능하기 때문에 

  : 네트워크 마지막에 구에 사영시키는 operator 추가 (compute embedding)

  : 5-shot 5-way(n-way는 클래스가 n개) 정확도가 70프로대 

* Combining multiple Descriptor (FC layer) – “Combination of Multiple
  Global Descriptors for Image Retrieval(2019)”

</br>

### Fine-Grained Image Classification / Fine-Grained Visual Classification(FGVC)

* 유사한 이미지 간 분류 (differentiating between hard-to-distinguish object classes)

</br>

### 방법

*  Autoaugment learning – “AutoAugment: Learning Augmentation Policies from Data(2018)”

  : search algorithm 을 이용해 가장 적합한 augmentation policy를 찾음 

* Attribute aware attention – “Attribute-Aware Attention Model for Fine-grained Representation Learning”

  : imagenet dataset으로 학습된 pre-trained CNN이용

</br>

### One-shot Learning

*  learning a class from a single labelled example 

* 새로운 이미지의 학습 반영 빠름 

* 학습할 때 한 class 당 1장~5장

</br>

### Few-shot Learning

* n-way one-shot task 

* n= 페이지 수 

  : 1) 1-Nearest Neighbor : 간단히 테스트 이미지 중 유클리디언 거리로 가장 가까운 이미지 선택하기 

  : 2) HBPL : 획에 대한 학습 필요 ==> X