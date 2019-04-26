# MultiGrain: a unified image embedding for classes and instances

### Abstract

joint training을 한다. 

cross-entropy 최소화.(classification 측면) + ranking loss 최소화(data augmentation과의 일치 여부) 

pooling layer가 주요 요소. 저해상도 이미지로 훈련된 네트워크를 고해상도 이미지에 이용. 

linear classifier에 돌려봐도, 79.4%라는 state-of-art한 정확도를 얻었음 

</br>

### Introduction

Image retrieval(이미지 검색)의 성능은 주로 image embedding을 어떻게 하는가에 달려있다. 그래서 데이터베이스 사이즈와 스피드 및 정확도 사이에서 trade-off 관계가 생성됨.

