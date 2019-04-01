**FaceNet**

---

* 이미지마다 deep conv net 적용해 유클리드 임베딩을 학습 
  - Conv net으로 어떻게 임베딩을 학습하지? 임베딩된 값을 conv net에 넣어서 피쳐를 뽑는 건가?

*  임베딩 공간의 l2 distance를 얼굴 유사도로 (같으면 적고 다르면 크고) 

  - Verification : 임베딩 간 거리가 차이를 넘는지

  - Recognition : k-nn classification

  - Clustering : k-means, agglomerative clustering 

* Large margin nearest neighbor

* Triplet loss 사용 à output : 128차원의 임베딩 

?? 한 사람의 임베딩에 대한 구형의 cluster를 encourage 시키는 hard-positive mining techniques??

*  기존 방식은 순수하게 image pixel로부터 얻은 표현을 학습(data-driven, large dataset), cnn bottleneck layer에 접근해야  

*  본 논문의 방식

  - end-to-end learning 

  - 얼굴인식, 검증, 클러스터링 세 개 다 반영하는 triplet loss 사용 

  - Triplet loss : 한 사람과 다른 모든 얼굴로부터 나온 모든 얼굴쌍에 대해 margin 강화 ?
    - 임베딩 - 이미지 x를 d차원의 유클리드 공간에 임베딩 

-  Triplet selection

-  Triplet을 online으로 생산(mini-batch) 

- cpu cluster에서 1000~2000시간 훈련 

-  1x1xd conv layer를 원래 conv layer 사이에 추가 

- 평가
  - 주어진 두 얼굴쌍에 대해 L2 distance 구하기 

​        

 

**배경지식 관련 궁금점** 

---

-  PCA ?

- Triplet loss가 어떻게 작용하는지? 

- 1x1xd conv layer의 효과 ?

-  FLOPS ?

-  Cnn bottleneck layer