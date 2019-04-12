#### 공분산

n-1로 나누기도 함 : 표본이기 때문에 그럼. 모분산이 아니라 표본을 통해 얻은 것이므로. 근데 샘플이 크면 n이나 n-1이나 그게 그거 

* 내적을 n으로 나누면 왜 분산인가..
* 전치는 왜 하나.. ==> symetric으로 만들라구

공분산 행렬의 의미 : 데이터가 어떻게 변하나...(?)를 보기 위해 

의미 2) shearing(선형변환) : 선처럼 늘여주는 것. 



</br>

### 정사영

참고자료 : <https://j1w2k3.tistory.com/240>

![ì ì¬ìì´ëì ëí ì´ë¯¸ì§ ê²ìê²°ê³¼](http://mblogthumb3.phinf.naver.net/20110906_178/at3650_1315292358247GbSXe_JPEG/182.jpg?type=w2)

* 정사영 : 영어로는 orthogonal(수직) projection(그림자)
* 어떤 대상에 수직으로 빛을 비추어서 만들어진 부분
* 수직 : 빛의 방향과 그림자가 수직이다

</br>

</br>

### PCA : 데이터 구조를 잘 살리면서 차원 감소를 하게 하는 방법

- 구조를 잘 살린다.. / 영어점수, 국어점수 -> 문과적 능력 / 수학,과학 -> 이과적 능력 

- 기본적인 방법 : 정사영 

- 주축에 정사영을 시켜야 한다. 그러라면 어떤 벡터에 정사영시킬까?.?

  ![1554963665521](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1554963665521.png)

![1554963976096](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1554963976096.png)

- 잘 살려 줬는가? 는 선상에서 퍼진 정도(분산)으로 알 수 있다. 정사영 후의 데이터 분포 분산이 크면..좋다. 왜? 왜 크면 좋담///?? 압축으로 인한 왜곡이 크지 않은거라....? 불명확 
- 주축은? eigenvector -> 엄밀한 증명 : 라그랑주 
- 3차원인 경우?
- N차원 데이터의 경우 : N개의 eigenvector (직교 orthogonal)
- 필요없는 차원을 줄인다. 

![1554966536452](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1554966536452.png)



![1554966557025](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1554966557025.png)

</br>

</br>

### Eigenvector 

* "어떠한 선형변환 A가 있을 때, 그 크기만 변하고 방향이 변하지 않는 벡터가 있나요?, 그 벡터의 크기는(람다) 얼마나 되나요?"

  ![1554968803370](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1554968803370.png)

  파란색과 보라색 벡터는 값은 변해도 방향은 변하지 않음. 

</br>

</br>

### Determinant(행렬식)의 기하학적 의미

* ad-bc
* 행렬 : 열벡터의 모음 

![1554969203866](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1554969203866.png)

![1554969386841](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1554969386841.png)

* det(A)는 평행사변형의 넓이 

  ![1554969646863](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1554969646863.png)



</br>

</br>

### 자연상수 e

* e의 의의 : 성장을 표현하기 위함, 자연의 연속한 성장(growth)



</br>

</br>

---

참고자료

<https://www.youtube.com/watch?v=Nvc7ZRVjciM>

<https://www.youtube.com/watch?v=EI1btogsxZA> 