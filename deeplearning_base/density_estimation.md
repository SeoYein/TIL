## density-based novelty detection

​     </br>

- 데이터의 분포를 사용하여 이상치 검출하는 방법 

- 기존에 존재하는 데이터 분포 사용 (training data의 분포를 모델링) 

​     </br>

### 가우시안 밀도 추정 

-  데이터가 하나의 정규 분포를 따른다고 가정하고 사용하는 방법론 

![Imgur](https://i.imgur.com/o0wdkoW.png)

</br>

* 장점
  * 데이터 스케일링에 민감하지 않음 
  * 확률값 구할 시 마할라노비스 거리 계산 - 스케일링 없이 분산까지 고려

</br>

</br>

### Maximum likelihood estimation 최대 우도 추정

- spherical

  ![Imgur](https://i.imgur.com/vZWtNIk.png)

- diagonal 

  ![Imgur](https://i.imgur.com/VAIKKYd.png)

  

- full

  * 공분산을 전부 고려 (축이 기울어지게 됨)
  * full은 변수가 너무 많을 시 공분산 행렬이 singular matrix가 돼서 역행렬을 못 구하게 된다는 단점이 있다

  ![Imgur](https://i.imgur.com/ic7e1Nx.png)

