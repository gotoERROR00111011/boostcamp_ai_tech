# Week 3 - Day 14 - Recurrent Neural Networks

## Introduction
### Lecture
- RNN 첫걸음
- Sequential Models - RNN
- Sequential Models - Transformer

## Sequence Model
### 조건부확률
이전 시퀀스의 정보를 가지고 앞으로 발생할 데이터의 확률분포를 다루기 위해 조건부확률을 이용  
<img src="https://render.githubusercontent.com/render/math?math=P(X_1, \dots, X_t)=P(X_t|X_1,\dots,X_{t-1})P(X_1, \dots, X_{t-1})=,\dots,=\prod_{s=1}^{t} P(X_s|X_{s-1},\dots,X_1)">

### 가변 데이터
sequence data를 다루기 위해서는 길이가 가변적인 데이터를 다룰 수 있는 모델이 필요  

### Naive Sequence Model
이전 전체 데이터 고려  
<img src="https://render.githubusercontent.com/render/math?math=P(x_t|x_{t-1},x_{t-2},\dots)">

### Autoregressive Model
이전 일부 데이터 고려  
<img src="https://render.githubusercontent.com/render/math?math=P(x_t|x_{t-1},\dots,x_{t-\tau})">

### Markov Model(first-order autoregressive model)
직전 데이터 고려  
<img src="https://render.githubusercontent.com/render/math?math=P(x_1,\dots,x_T)=P(x_T|x_{T-1})P(x_{T-1}|x_{T-2})\cdots P(x_2|x_1)P(x_1)=\prod_{t=1}^T P(x_t|x_{t-1})">

### Latent Autoregressive Model
hidden state가 이전 데이터 요약  
<img src="https://render.githubusercontent.com/render/math?math=\hat x = P(x_t|h_t)">
<br>
<img src="https://render.githubusercontent.com/render/math?math=h_t=g(h_{t-1}, x_{t-1})">


## Recurrent Neural Network
멀리 있는 과거의 정보를 고려하지 못한다는 단점이 있다.  


## Long Short Term Memory


## Gated Recurrent Unit


## Transformer
### Encoder

### Attention
input vector를 (다른 sequence vector를 고려하여) 새로운 vector로 변환하는 방식  

1. input 하나에 3개의 vector(Query, Key, Value)를 만든다.
1. 한 단어의 Q vector와 전체 단어 각각의 K vector 내적 Score를 구한다.(=유사도)  
1. Score들을 K의 dim의 제곱근 <img src="https://render.githubusercontent.com/render/math?math=\sqrt{d_k}">으로 나누어 normalize 한다.
1. softmax
1. sum(V vector * softmax) = Z vector

여기서 Q, K vector는 dim이 같아야 하지만, V vector는 달라도 된다.  
input vector와 output vector의 dim도 같아야한다.  

### Multi-Headed Attention (MHA)
attention을 여러개 사용  

### Positional Encoding
attention으로는 sequence 정보를 포함하지 못하기 때문에 positional encoding을 더해준다.(bias)  

### Decoder
encoder의 V, K vector를 입력으로 사용한다.  

