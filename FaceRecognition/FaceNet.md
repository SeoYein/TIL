**FaceNet** </br>
참고 <https://marades.tistory.com/9> 
---

* 이미지마다 deep conv net 적용해 유클리드 임베딩을 학습 
  - Conv net으로 어떻게 임베딩을 학습하지? 임베딩된 값을 conv net에 넣어서 피쳐를 뽑는 건가?

*  임베딩 공간의 l2 distance를 얼굴 유사도로 (같으면 적고 다르면 크고) 

  - Verification : 임베딩 간 거리가 차이를 넘는지

  - Recognition : k-nn classification

  - Clustering : k-means, agglomerative clustering 

* Large margin nearest neighbor

* Triplet loss 사용 output : 128차원의 임베딩 

?? 한 사람의 임베딩에 대한 구형의 cluster를 encourage 시키는 hard-positive mining techniques??

*  기존 방식은 순수하게 image pixel로부터 얻은 표현을 학습(data-driven, large dataset), cnn bottleneck layer에 접근해야  

*  본 논문의 방식

  - end-to-end learning 

  - 얼굴인식, 검증, 클러스터링 세 개 다 반영하는 triplet loss 사용 

  - Triplet loss : 한 사람과 다른 모든 얼굴로부터 나온 모든 얼굴쌍에 대해 margin 강화 ?
    - 임베딩 - 이미지 x를 d차원의 유클리드 공간에 임베딩 

-  Triplet selection
  - : 논문 상에서 주의깊게 봐야할 부분 
    : loss가 0이 안되는 triplet만 고르게 되면 기준점에 대해 가장 먼 positive point와 가장 가까운 negative point를 고면 되는데, 이를 hard positive 와 hard negative라고 함 --> 이를 매번 찾는 건 계산량과 오버피팅 위험을 증가 --> 그래서 mini batch 안에서 찾음 

-  Triplet을 online으로 생산(mini-batch) : hard positive와 hard negative를 몇 천개의 mini batch안에서 찾음  

- cpu cluster에서 1000~2000시간 훈련 

-  1x1xd conv layer를 원래 conv layer 사이에 추가 

- 평가
  - 주어진 두 얼굴쌍에 대해 L2 distance 구하기 

​        

 

**배경지식 관련 궁금점** 

---

-  PCA ?

- Triplet loss가 어떻게 작용하는지? 
  참고링크 : <https://wwiiiii.tistory.com/entry/Pairwise-Triplet-Loss> 
  - pairwise ranking 
    : - 여러개의 입력이 주어질 대 입력 간의 상대적 순위 구하기 문제 - regression하기도 애매하고, binary classification도 적덜하지 않을 때 --> pairwise ranking loss이용 입력 xi, xj가 rank(xi)>rank(xj)를 만족하면 f(xi) > f(xj) 를 만족하는 실수함수 찾기 

  : 이용 ) 주어진 이미지와 관련된 여러 레이블 뽑기 --> 예측에 실패해도 정답 레이블 확률이 높은게 좋다는 점을 살리기 위해 (?)  - softmax랑 정확히 차이가 뭐지? softmax로도 score을 어차피 알지 않나, 클래스별로 하나하나 랭킹을 알 수 있어 그런건가? 

  : 순위표 만들기 ) 모든 가능한 클래스에 대해 confidence score를 계산해 순위표 만들기  

  : 이후 각 클래스마다 따로 있는 threshold를 넘으면 해당 클래스에 속한다 판정 

  - softmax loss?
  - binary cross entropy? 

- triplet loss 

  : person re-identification 혹은 face recognition에 널리 쓰임 

  : embedding function 사용 

  : loss 의 목표 - 기준점과 비슷한 점을 임베딩 했을 때의 거리가 기준점과 다른 점의 임베딩 간 거리보다 알파 이상 더 가깝게 하는 것 (부등식 만족) f는 학습 대상, d는 기존의 것을 사용하기도 함 (L2 norm)

  - metric learning? 

    참고 <http://sanghyukchun.github.io/37/> 
   - : d(f(xi),f(x_pos)) + a < d(f(xi), f(x_neg))를 만족하게 함 

    : pairwise ranking loss와 비슷하지만 f의 결과가 고차원적이고 clustering을 위한 metric learning에 쓰임 

    : anchor-positive를 이용하기 때문에, 비슷한 점끼리 모임 

    : 각 입력에 대해 label이 필요한 classification과 달리 같은 클래스냐 다른 클래스냐 여부만 알면 학습이 가능 

    : ==> 왜 triplet이냐? : pairwise loss는 서로 다른 두 점 만을 뽑지만 , triplet loss에서는 anchor, positive(비슷한 점), negative(다른 점) 이렇게 세 개를 뽑음

    - hierarchical clustering??

	    : 여기서는 d함수가 L2 norm 

 		? 왜 hard positive와 hard negative를 보는거지? 제일 가까운 pos랑 제일 먼 neg를 봐야하는 게 아닌가?

- 1x1xd conv layer의 효과 
[참고](https://hwiyong.tistory.com/45)
 : 구글넷에서 1x1 convolution을 통해 연산을 줄임
 : 채널 조절, 계산량 감소, 비선형성 이라는 장점이 있는데 왜? 그런가 하면
 : 1x1 filter를 사용하는데, 채널 수를 조절할 수 있다. (원하는 채널 수만큼 filter 를 넣어 준다) -> 파라미터가 현저히 줄어듦
 : 1x1 convolutional layer와 ReLU를 통과하면서 비선형성이 증가 
 

-  FLOPS  ?

-  Cnn bottleneck layer
 : softmax를 거치기 전 마지막 layer
 : feature 를 extract하기 위해 
