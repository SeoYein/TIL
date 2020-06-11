* iccv 2019 best paper 
  * 또 다른 구술 발표 초청 paper들은? 혹은 트렌드는? 
* iccv 2017 best paper은
  * mask rcnn

* 2017 cvpr best paper : simGAN
  * 데이터를 구하기 어려울 때, 시뮬레이션을 통해 데이터를 얻기 쉬운 상황을 만들고, 시뮬레이션 데이터를 실제 데이터처럼 바꿔주는 GAN을 학습시킨 뒤 실제같은 가짜 데이터를 추가적으로 지도 학습에 적용해 성능 향상  
* 2018 cvpr best paper 
  * taskonomy : transfer learning을 각기 다른 테스크들을 합쳐서 진행





### 0. abstract 

* 모델이 학습되는데 그건 이미지 내부 패치의 분포를 알아내려고 (to capture the internal distribution of patches within the image)

* convolutional GAN의 피라미드를 갖고 있다(contains a pyramid of fully convolutional GANs). 각각의 GAN은 이미지 패치의 분포를 여러가지 이미지 스케일(at a different scale of the image)에서 학습한다. 

  → 그래서 다양한 크기와 각도 등의 이미지를 생성이 가능함 

### 1. Introduction

* 피라미드를 이루고 있는 각각의 GAN들은 training과 추론을 한다. 
* 테스크 : unconditional generation learned from a single natural image. 
* 한 장에서의 이미지 패치들의 내부 분포 (? internal statistics of patches)를 통해 강력한 generative model을 만들 수 있음
* 같은 클래스로 이루어진 db를 만들 필요가 없음 
* single natural image로 학습이 가능한 이유는 
  *  "pyramid of fully convolutional light-weight GANs" 
  * 피라미드 형식으로 되어 있어서 이미지 패치들의 분포를 다른 스케일로(at a different scale) 포착(capturing)해 냄 
* 한 번 트레이닝이 되고 나면, SinGAN은 높은 수준의 다양한 이미지 샘플을 생성할 수 있음. (어떤 임의의 차원에서도(of arbitrary dimensions))
* ? modeling the internal distribution of patches within a single natural image 는 컴퓨터 비전 테스크에서 강력한 우선순위로 여겨져 옴 : denoising, deblurring, super resolution



#### 1.1. related work

* single image deep models
  * 이전에 이미지 한 장으로 internal GAN based 모델도 있고, 한 장으로 일종의 오버 피팅을 시키는 모델은 있지만 데이터나 다룰 수 있는 테스크가 하나라던가의 제약이 있었다. 
  * unconditional single image GAN이라는 건 texture generation에 특화가 되어 있었다. 이런 모델들은 non-texture image를 생성하는데 적합하지 않다.
  * SinGAN은 texture에 한정된 게 아닌, 자연적인 이미지에도 적용이 가능하다. 
* super resolution, texture expansion 
  
* generative models for image manipulation

  * 한 이미지와 유사한 이미지를 생성하게 하는 게 아니라, 모든 overlapping하는 multi scale 이미지 패치를 고려한다.

     

### 2. Method

* 목적 : unconditional generative model을 학습시키는 것 

  * 세팅 자체는 전통적인 GAN 세팅과 같다. 
  * 다른 점은 single image만 있으면 된다는 것. 
  * texture generation이상으로 가고, 더 제너럴한 자연 이미지를 다루기 위해, 복잡한 이미지의 분포(statistics)를 다른 스케일로 잡아내는 게 필요하다. 
  * arrangement나 큰 물체의 모양이라던가를 잡아내게 됨. 

* 목적을 이루기 위해 그림과 같이 특정한 generative framework를 사용함(fig.4)

  ![1572939135425](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1572939135425.png)



* 구조를 보면

  * GAN 피라미드가 있는데, 이 GAN 피라미드는 training과 inference를 동시에 진행한다. 거친 특징에서부터 세세한 특징으로 추론해낸다(coarse-to-fine fashion).
  * GAN들에 들어가는 scale이 다른데, 각각의 scale마다 생성자는 다운샘플된 트레이닝 이미지랑 구분이 어렵도록 이미지 샘플을 생성한다.(At each scale, Gn learns to generate image samples in which all the overlapping patches cannot be distinguished from the patches in the down-sampled training image, xn, by the discriminator Dn) 
  * 패치 사이즈가 점점 작아진다. 

  * 노이즈를 넣고→ 생성하고→ 업샘플링하고→업샘플링된 이미지 사이즈에 맞춰 노이즈를 넣고 → 노이즈와 이전 단계에서의 생성물을 갖고 생성하고 

    ![1572941236237](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1572941236237.png)

    

#### 2.1. multi-scale architecture

* x0~xn으로 학습되는데, xn은 다운샘플링된 이미지임 
* coarse scale부터 fine scale까지 
* 모든 generator은 유사한 구조를 갖고 있음. 
* 노이즈를 계속 같이 넣음으로서(이전 GAN의 )결과에 noise를 무시하는 걸 방지함 (conditional일 경우 randomness만 포함해서 학습시키면 발생하곤 했음(disregard))

* convolutional layers를 넣어서 upsampling하면서 디테일한 부분을 복원 
* fully convolutional net 
  * 5-conv blocks로 이루어져 있음 32커널로 시작함 → 테스트 시 임의의 크기로 사이즈 생성 가능(fully convolution)



#### 2.2 Training

* sequentially(coarse → finest)하게 train
* 각각의 GAN이 학습이 되면 그건 고정이 됨. (?학습이 되었는지를 어떻게 판단하나 기준이 있나)
*  ![1572943662629](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1572943662629.png)
  * Ladv는 adversarial loss : 패치들의 분포와 생성된 피치들의 분포 간 거리에 대해 패널티를 주는 것임. 그러니 생성자는 이를 감소시켜야 함 
  * Lrec는 reconstruction loss : noise 중에서 실제랑 유사하게 만들어지는 노이즈를 고정하여 보존함. 