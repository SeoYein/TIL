## Image Classification과 Image Retrieval의 차이

직역을 하면 이미지 분류와 이미지 검색의 차이라 볼 수 있겠다. 

이미지 검색(Retrieval)의 부분이 완전히 와닿지 않아서 찾아봤다. 둘의 차이는?





### Image Classification은

Training set으로 학습시키고, 학습된 걸 기반으로 test image가 뭐일지 class를 결정해주는 것. 



### Image Retrieval은

query image가 주어졌을 때, 데이터베이스 상에서 그 이미지와 가장 유사한(벡터공간상에서 가까운!) 이미지를 찾는 것. 

순수하게(purely) 거리 기반의 접근. 



둘의, 차이를 본다면, training 과정의 유무라고 볼 수 있겠다. 

참고 글에서는 label의 유무라고 했지만, unlabeled data를 training set으로 잡아서 특징 공간을 만든 다음에 분류를 진행하는 쪽으로 많이 발전이 되고 있기 때문에..!(물론 class가 binary("겨 아녀?")일 경우에 그렇다)



그리고, Image Classification은 클래스를 반환하지만, 

Image Retrieval은 가장 유사한 이미지를 반환한다. 



같은 클래스의 컨텐츠를 반환하도록 만들면 Classification이 Retrieval이 될 수 있는 거 아닌가? 싶지만 사실 그렇지 않다. 

빨간 자동차 이미지를 test 혹은 query 이미지라고 하면, Classification은 'car'이라는 class에 해당하는 이미지를 반환하게 될 것이다. 라벨링을 좀 더 세세하게 해도, 'red car'인 이미지들을 다 반환하지 그 중에서 가장 유사한 이미지를 반환하지 않는다. 

반면 Retrieval은 갖고 있는 이미지 중 가장 가까운, 가장 유사한 이미지를 class에 구애받지 않고 반환하게 된다. 애초에 Retrieval은 Class, 즉 label이 필요하지 않기 때문. 



---

참고링크

<https://stackoverflow.com/questions/15104318/difference-between-image-retrieval-and-image-classification>

