# AI

[TOC]



##### 인공지능

- 인간의 지능에 가까운 기능을 갖춘 컴퓨터 시스템

##### 머신러닝

- 인공지능 시스템을 구현하는 구체적인 접근 방식
- 컴퓨터가 데이터를 학습함으로써 기존 데이터와 유사하지만 처음보는 데이터를 자동으로 해석할 수 있게 하는 기법
- 모델선택 -> 최적의 변수 찾기(손실함수이용) 

##### 인공신경망 모델

- 머신러닝 방법 중 생물학적 신경망의 시냅스 결합을 모방한 모델
- 두개 이상의 신경망층을 쌓은 모델 - 심층 신경망(deep neural network)

##### 선형회귀(Linear Regression)

- 주어진 데이터를 가장 잘 설명하는 직선을 찾는 문제

- 모델의 기본 형태 
  $$
  y=wx + b
  $$

- 대표적 손실함수 : 평균 제곱 편차(Mean Squared Error)
  $$
  MSE =
  $$

- 최적화 함수: 손실을 최소로 만드는 기울기와 편차를 찾는 함수 ex) 경사하강법

##### 신경망 네트워크(Neural Network)

- 선형 모델로 해결하기에 한계가 있음
- CNN(컨볼루션 인공신경망)





--------

개발환경

##### 아나콘다

https://www.anaconda.com/distribution/

```cmd
가상환경 생성 및 활성화
> conda create -n AI python=3.7
> conda activate AI

라이브러리 설치
(AI)> conda install git matplotlib scikit-learn tqdm scipy numpy tensorflow-gpu==2.0.0
```



------

### 전처리

##### 1 load image

- 이미지 가져오기
- 사이즈 맞춰주기
- 