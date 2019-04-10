#### I. INTRODUCTION

A. Automation in X-Ray Security Imaging

* TD, SA, MV, AD라는 방법이 있는데 기존연구는 주로 TD에 집중해왔으나, 데이터 확보의 문제로 현재는 AD가 필요로 되는 상태 

* 인공위성 영상에서 AD는 많이 쓰이고 그보다 좀 적게는 비디오에서 쓰이고 아주 드물게 x-ray security분야에 쓰인다(저자 및 저자 관련인의 연구)

  

B. Anomaly Detection in X-Ray Security Imaging

* x-ray security에서의 anomaly란? : 정상으로부터 다른 generating process가 발생한다는 것, 즉 불법적인 걸 숨겨오려 할 때 

* 분류를 다음과 같이 진행할 예정 

  major : appearance, semantic, appearance-given semantic

  minor : relative-appearance, arrangement, low-level, co-occurrence, passenger-route-relative 

  

C. Approaches to Anomaly Detection

1) data representation

* 세 가지 방법 있다. raw, engineered, learned 

* raw는 risky하고 engineered는 까다롭고, learned는 CNN사용할 경우  - 충분한 데이터만 있으면- 성능이 좋고 간편하니 learned representation을 쓸 것이다. 
* 저자의 기존 연구 : auto-encoder하고 internal label을 시도했는데, 이 둘은 어쨌든 다 충분한 데이터셋이 있었다
* 근데 x-ray security data는 라벨이 충분치 않다. 그래서 transfer learning으로 representation을 진행할 것이다. 

2) outlier detection 

* anomaly 구분을 위해 네 가지 방법 존재 : boundaries(SVM), trees(Isolation Forest), distance-based(mean-distance, k-nearest, compare local average), density 
* density method는 test data의 likelihood를 평가한다 보통 독립을 가정하고 진행하지만 그렇지 않아도 효과적인 방법이다. 
* 이 논문에서는 parametric density estimation 접근 방식을 쓸 거임! 고차원의 데이터를 잘 다루기 때문 
* semantic anomaly를 위해서는 scalar-valued vector representation이, appearance anomaly를 위해서는 binary vector representation이 쓰일 것  



D. The Proposed Approach 

* 데이터는 SoC 이용
* CNN pooling layer 이용해 appearance anomalies 검출, logit layer 이용해 semantic anomalies 검출



#### II. DATASETS

* SoC
* Pre-processing
  - automatically cropped
  - reduced an unstructured set of 224x224 pixel patches : stride - 112 or less 
  - -> an average of 26 patches produced for each dual-view SoC image



#### III. REPRESENTATIONS

* Wolfram ImageIdentify CNN 사용 
* 4315개에 대해 구분할 수 있도록 카테고리화 된 모델이라 선택 
* softmax에 들어가기 전 4315 dimension을 지닌 층에서 semantic anomaly에 대해 파악 

A. Appearance

* apearance representation 구하기 : 1024-dimension인 binary vector를 쓰는데,  이는 마지막 pooling layer에서 activation을 거친 0과 1사이의 값에 threshold를 적용해서 0과 1로 이루어진 값을 나타낸 것. 이유는 분포때문! 

B.Semantic 

*  전체에서 한 개의 이미지에 대한 representation을 구하고 싶기 때문에 maximum-over-patches방식을 이용. 
* wolfram imageIdentify Net을 보면 짐꾸러미에 없는 class가 나오기도 하고, 총이 실제 있는 것보다 더 적게 검출하는 걸 알 수 있다. -> 다른 도메인이기 때문에 형편없는 결과 



#### IV. THREAT DETECTION

* 기존에 많이 사용하는 방식인 TD에 관해 appearance와 semantic anomaly 구분하기 
* representation이 supervised TD에 얼마나 잘 작동하나 보기 
* appearance의 경우 99%, semantic은 92% 정확도를 보임 

​	



#### V. ANOMALY DETECTION

* basic하게 접근 시 : 총기는 더 어두우니까 총기가 있는 그림은 pixel값이 더 높을 것이라 생각하고 진행할 시 성능은 60~70%정도(AUC)

A. Appearance

* full-covariance gaussian model을 썼다. 그게 성능이 좋음. 95%

B.Semantics

* 4315개 클래스에 대한 subset이 아닌 996개에 대해서만 데이터 사용, anomalous가 아닐 만한 건 배제 , 4315개 모두 쓸 경우 88%(full-schema)로 낮은 성능 
* variance를 각 차원에서 mean한다음 사용 
* 벗어남에 대해서도 12개(총기 종류 수)만 고려 : 벗어나도 위험과 상관없는 카테고리 배제 
* full scheme일 경우 95%

C.Combined 

* appearance와 semantic anomaly score의 가중합으로  측정 
* 결과는93.4% : 92.5와 88.2보다 높은 수준 

* figure 13 설명. 하드한 threshold를 줬지만, 잘 구분안된 걸 보면 usual해 보이고 괜찮은데  anomaly로 구분된 걸 보면 unusual하다..

D.Traning set size

* 4096 SoC images로 학습을 했고 이는 충분했다. 
* 그런데 데이터 수가 적을 경우 combined가 성능이 잘 안 나옴. maximum에 도달할 때까지 semantic이 더해질 수 없어서 그런듯. 
* 데이터가 적을 경우는 diagonal covariance가 더 빨리 안정권에 접어듦 

E. Hyper-Parameter Sensitivity

* 세 개의 hyper parameter가 있음. 1) appearance vector 구할 때 사용하는 binarization threshold. 2) excursion(배제)의 개수. 3) combine appearance를 구하기 위한 weight의 비율
* fig.15에서 이 파라미터의 변화에 따라 변하는 효과를 볼 수 있더라. 
* binarization threshold는 0.4-0.24의 6-fold range로,  excursion의 개수는 3에서 15까지 총 5-fold range로, weight ratio는 8에서 64까지 8-fold range로 진행. 

F. Choice of CNN

* Wolfram Image Identify (v11.1) CNN 사용 
* Inception하고 생긴 게 비슷하고 그런데 class는 더 많음! 
* high-dimension에 좋음 

G. Computational Cost

* Titan X로는 성능 충분. 
* 코딩 잘하면 반으로 줄일 수 있을듯. 
* per-image 과정
  * crop boundary
  * patch로 나누기 
  * 각 patch를 CNN으로 processing
  * thresholding & combining by max
  * extract vectors
  * 마할라노비스 거리 구해서 score구하기 

H. An AnoGAN Approach

* 생각보다 성능 안 나왔다. 70%대
* 아마 normal class에 대해 다양함에 있어 차이가 있어서 그런게 아닌가 
* 성능을 위해선 더 engineering이 필요할 것으로 결론



#### VI. SUMMARY & CONCLUSIONS

* Training set 커지면서 anomaly detection의 성능도 올라감. 

* anomaly detection 성능을 보면 supervised training 했을 때보다 낮긴 낮지만, 기존에 없던 것도 찾을 수 있고 TD의 보충으로 사용할 수도 있고 

* localization 성능은 조잡(crude)하다. 

* 5개의 방법으로 성능을 올릴 수 있을 것 

  * 다른 종류의 CNN architecture를 사용

  * X-ray Trained된 CNN을 사용 

  * modeling distributio을 다르게 사용  

  * outlier detection에는 density modelin보다는 boundary-based(SVM, isolation forest)를 사용 

  * Training data 증가 

    

#### 기타

* TIP 관련 자료 (영문)

<https://www.wi-ltd.com/x-ray-baggage-scanner-features/>