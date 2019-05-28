### triplet loss

* facenet에서 사용한 loss

* 데이터를 anchor, positive, negative 이렇게 세 그룹으로 나누어 사용한다. 그래서 붙여진 이름 triplet loss

* anchor : 기준 데이터, positive : anchor와 같은 클래스의 데이터, negative : anchor와 다른 클래스의 데이터 

* 기본적인 개념은, anchor와 positive는 같은 클래스이므로, 이 둘의 거리는 가깝게(작게), anchor와 negative는 다른 클래스이므로 이 둘의 거리는 멀게(크게) 한다! 라는 개념에 기인한다. 

* 즉, d는 거리를 구하는 함수(L2norm이라던가 유클리디안 거리 등), f(x)는 임베딩하는 함수(cnn이라던가 feature extraction)라고 할 때, 
  $$
  d(f(Xa),f(Xp)) <= d(f(Xa),f(xn))
  $$
  이라는 개념!

  여기에 차이를 확연히 하기 위해, 알파를 추가해준다

  정확히는, 거리를 둘 다 0으로 되도록 학습하는 걸 방지하기 위해.

  

* $$
  max(0,d(f(Xa),f(Xp))-d(f(Xa),f(Xn))+\alpha)
  $$

  로스함수가 이렇고, 이를 최소화하도록 학습한다. 

* 로스함수가 보통 net과는 별도로 있는 것에 비해서, triplet loss에는 net이 들어가 있단 점이 흥미롭다. 이게 2015년도에 나온 개념이라니..너무 신박하고 재미있다.

* triplet loss에는 한계가 있긴 한데, positive와 negative를 잘 선택해줘야 한다는 점이다. 너무 거리가 가까운 즉, anchor와 지나치게 비슷한 positive라던가, anchor와 너무 다른 negative를 선택하면 학습을 적게 하게 되므로, 이러한 데이터셋을 선택하면 안 된다. 그래서 facenet에서는 positive 중 가장 먼 것 (이를 hard positive라고 한다), negative 중 가장 가까운 것(hard negative) 개념을 도입했다고 한다. 