## Weight initialization - Xavier initialization

---

* ### 등장 배경 (기존의 문제)

  * 잘못된 방법으로 weight를 초기화했다는 주장 

    1) -1과 1 사이의 난수로 초기화할 경우 초기화 시마다 성능이 달라짐(작으면 너무 줄어들고, 크면 너무 커지고) 

    2) weight 초기값이 0이 될 경우 딥러닝은 동작하지 않음. 

  * 이러한 문제를 해결하기 위해 hinton이 restricted boltzmann machine 제시: forward랑 backward를 반복하면서 2개 layer에 대해 (현재와 다음 layer) 초기화한뒤 넘어가고 다음 2개 layer에 대해 초기화한뒤 넘어가는 방식으로 초기화를 진행 --> 하지만 구현하기 복잡하다..

    

* #### input X와 output Y의 평균과 분산이 일치하도록 weight를 초기화해야 한다. 그래서 Layer가 늘어나도 saturation에 안 빠지고 model이 train될 수 있어야 한다.  



* ### Xavier initialization

  * not too small, not too big인 값을 고르면 된다!
  * fan_in : 입력층 뉴런의 수, fan_out : 출력층 뉴런의 수 
  * 평균이 0이고 분산이 1/fan_in 인 분포를 이용
  * 그렇다면 표준편차는 np.sqrt(1/fan_in)

  - w = np.random.randn(fan_in, fan_out)*np.sqrt(1/fan_in) ==> fan_in과 fan_out 사이에서 난수를 생성한 뒤, 표준편차로 나눠줌!! 

    ==> 어차피 평균은 0이기 때문에 특정 범위에서 난수를 생성해서 표준화((값-평균)/(표준편차))를 한다고 볼 수 있는 것! 너무 작거나 너무 큰 문제 해결!

  - 혹은 평균이 0이고 분산이 1/(fan_in + fan_out)인 분포를 이용하기도 한다

    w = np.random.randn(fan_in,fan_out)*np.sqrt(1/(fan_in+fan_out))

  * uniform, normal distribution 사용 
  * 시그모이드에서 효과적인 결과 하지만 ReLU에서는 안좋음....

  

* ### He initialization

  * ReLU를 활성화 함수로 사용 시 Xavier 설정이 0으로 출력값을 수렴하게 만드는 문제 해결 

  * W = np.random.randn(fan_in, fan_out)*np.sqrt(2/(fan_in + fan_out)) 

  * 왜! 2가 곱해진 것일까 

    ![img](https://cdn-images-1.medium.com/max/800/1*MR2IwJuHNGp5qHG8gA-FDA.png)

     input x, 가중치 w, 출력값 Y 가 있다고 할 때 

    ![img](https://cdn-images-1.medium.com/max/800/1*l8ychYGg4muHUdCbtGWVwQ.png)

    ​	w와 x는 독립이므로 다음이 성립한다 

    (위키피디아 : <https://en.wikipedia.org/wiki/Variance#Product_of_independent_variables>)

  * 지금껏 그래왔듯, 평균이 0이라고 가정하면 

    ![img](https://cdn-images-1.medium.com/max/800/1*Bz5PCkV2ei49G-o8IeXpRw.png)

    요것만 남는다. 

    ![img](https://cdn-images-1.medium.com/max/800/1*diIwo7vFzktbd5awCs3vwA.png)

    이 식이 성립하고, 또한 변수간 상호 독립이자 같은 분포를 지닌다고 가정하므로(i.i.d)

    ![img](https://cdn-images-1.medium.com/max/800/1*CzASylgSE8Jsv8wXBQPeWw.png)

    다음과 같은 식이 성립한다. 

  * 입력(X)과 출력(Y)의 분산을 같게 만들고 싶어하기 때문에 Var(wi) = 1/n = 1/fan_in이 된다. 
  * input과 output의 그래디언트 값의 분산을 같게 해야 되기 때문에, fan_in = fan_out이 성립해야 한다. 그래서 결국 두 개의 평균을 취한다. 2/(fan_in+fan+out)
  * 이후 연구에서는 실험에 따라 2/fan_in을 사용하기가 권장되었다. 





---

참고링크 

<https://pythonkim.tistory.com/41> 

<https://reniew.github.io/13/>

<https://gomguard.tistory.com/184> 

<https://nittaku.tistory.com/269> ** 수학적 의미

<https://medium.com/@prateekvishnu/xavier-and-he-normal-he-et-al-initialization-8e3d7a087528> **정확
