### CNN(convolution neural network)



#### NN vs CNN

NN:   입력층 -> hidden -> 출력층

CNN: 입력층 -> 컨볼루션층 -> 완전 연결층 -> 출력층



#### 컨볼루션층

이미지의 각 픽셀을 그대로 feature로 사용하는 것은 좋지 않은 방법이라는 것을 언급했었다. 대신 각 이미지로부터 독특한 특성만을 뽑아내어 feature로 사용한다면 더 좋은 성능을 낼 수 있을 것이다. 이 과정을 feature extraction이라고 하고, 이미지에서 feature extractor로 동작하는 레이어가 바로 convolutional layer이다.

Dense layer에서 각 입력 샘플을 1차원의 벡터 데이터로 보았다면, Convolutional layer는 입력 샘플을 3차원의 텐서(Tensor) 데이터로 인식한다. Convolutional layer는 입력 3차원 데이터를 적절히 변형해서 또다른 3차원 데이터를 출력한다.

conv 

- 컨볼루션 연산을 통해 입력데이터의 특징을 추출하여 특징맵 만듦
- 필터와 컨볼루션 연산함

relu

- 입력으로 주어지는 값 >0 그대로 출력
- 입력값 < 0 이면 0 출력

pooling

- 입력 정보를 최대값, 최소값, 평균값 등으로 압축하여 데이터 연산량을 줄여주는 역할
- max pooling이 가장 많이 사용
- relu에서 받은 값을 pooling하여 다음 컨볼루션 층으로 전달



#### 컨볼루션 연산 *

- 입력데이터 * 필터(가중치 집합체) -> 결과값 + 바이어스 -> 특징 맵
- 스트라이드: 필터의 이동간격



#### 패딩(padding)

- 컨볼루션 연산 수행전 입력 데이터 주변을 특정 값(0)으로 채우는 것
- 컨볼루션 연산을 수행하면 데이터 크기가 줄어드는 단점을 방지하기 위해



#### 필터를  통해 데이터를 추출해서 알수 있는것

- 풀링 값이 크다는 것은 데이터 안에 해당 필터의 특징이 많이 포함되어 있는 것을 의미함
- 특징 맵 값이 압축되어 있는 폴링 결과 값을 통해 데이터의 특징을 추출할 수 있음
- ex) 가로, 세로, 대각선 필터



#### 완전 연결층

- 컨볼루션 층의 3차원 출력값을 1차원 벡터로 평탄화 작업을 수행하여 일반 신경망 연결처럼 출력층의 모든 노드와 연결시켜주는 역할



#### 출력층

- linear regression -> softmax
- 입력받은 값을 출력으로 0~1사이의 값으로 모두 정규화하며 출력 값들의 총합은 항상 1이 되도록 하는 역할 수행



#### TansorFlow API

|         |                                                     |                                                              |
| ------- | --------------------------------------------------- | ------------------------------------------------------------ |
| conv    | tf.nn.conv2d(input, filter, strides, padding, ...)  | input [batch, in_height, in_width, in_channels]<br />filter [필터높이, 필터너비, in_channels, out_channels(적용되는 필터 갯수)]<br />padding SAME(0값 추가)/VALID(작아짐) |
| relu    | tf.nn.relu                                          |                                                              |
| pooling | tf.nn.max_pool(value, ksize, strides, padding, ...) | value [batch, height, width, channels] (relu를 통과한 출력값)<br />ksize [1,height, width, 1] (폴링할 범위)<br />pooling SAME(maxpooling 하기에 데이터가 부족한 경우) |
| flatten | tf.reshape                                          |                                                              |
| softmax | tf.nn.softmax                                       |                                                              |



1 트레이닝 데이터 분리

2 입력데이터와 정답데이터 저장

3 feed forward (컨볼루션층-> 완전연결층-> 출력층)

4 손실함수 구함

5-1 손실함수가 최소가 아닌경우: optimizer사용하여 update

- cnn에서는 경사하강법 대신 adamoptimizer사용(성능개선을 위해)

5-2 손실함수가 최소인 경우: 예측값, 정확도 비교



------

##### reference

- https://youtu.be/WPdGrPxEwXc
- [https://de-novo.org/2018/05/27/convnet-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0/](https://de-novo.org/2018/05/27/convnet-이해하기/)