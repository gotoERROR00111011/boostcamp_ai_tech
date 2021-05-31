# Week 3 - Day 11 - 딥러닝 기초

## Introduction

### Lecture

- Week3 Overview
- 베이즈 통계학 맛보기
- 딥러닝 기본 용어 설명 - Historical Review
- PyTorch 시작하기
- 뉴럴 네트워크 - MLP
- 데이터셋 다루기

## Bayesian Statistics

### Conditional Probability

조건부확률 <img src="https://render.githubusercontent.com/render/math?math=P(A|B)">는 사건 B가 일어난 상황에서 사건 A가 발생할 확률을 의미한다.

### 베이즈 정리

베이즈 정리는 조건부확률을 이용하여 정보를 갱신하는 방법을 알려준다.  
<img src="https://render.githubusercontent.com/render/math?math=P(A\cap B)=P(B)P(A|B)">
<br>
<img src="https://render.githubusercontent.com/render/math?math=P(B|A)=\frac{P(A\cap B)}{P(A)}=P(B)\frac{P(A|B)}{P(A)}">
<br>

- <img src="https://render.githubusercontent.com/render/math?math=P(\theta|\mathcal D)"> : posterior(사후확률), 데이터 관찰 이후에 측정하는 확률
- <img src="https://render.githubusercontent.com/render/math?math=P(\theta)"> : prior(사전확률), 데이터를 분석하기 전에 가정한 확률분포
- <img src="https://render.githubusercontent.com/render/math?math=P(\mathcal D|\theta)"> : likelihood(가능도), 현재 주어진 가정에서 데이터가 관찰될 확률
- <img src="https://render.githubusercontent.com/render/math?math=P(\mathcal D)"> : Evidence , 데이터의 분포

likelihood와 evidence를 통해서 사전확률을 사후확률로 업데이트한다.  
<img src="https://render.githubusercontent.com/render/math?math=P(\theta|\mathcal D)=P(\theta)\frac{P(\mathcal D|\theta)}{P(\mathcal D)}">

confusion matrix으로 조건부확률의 시각화를 볼 수 있다.

<table>
  <tr>
    <td><td>
    <td><img src="https://render.githubusercontent.com/render/math?math=P(\theta)"><td>
    <td><img src="https://render.githubusercontent.com/render/math?math=P(\neg\theta)"><td>
    <td><td>
  </tr>
  <tr>
    <td><img src="https://render.githubusercontent.com/render/math?math=P(\mathcal D|\theta)"><td>
    <td>True Positive<td>
    <td>False Positive<td>
    <td><img src="https://render.githubusercontent.com/render/math?math=P(\mathcal D|\neg\theta)"><td>
  </tr>
  <tr>
    <td><td>
    <td>False Negative<td>
    <td>True Negative<td>
    <td><img src="https://render.githubusercontent.com/render/math?math=P(\neg\mathcal D|\neg\theta)"><td>
  </tr>
</table>

### Example

- 발병률 10%
- 병에 실제로 걸렸을때, 검진될 확률 99%
- 실제로 걸리지 않았을때, 오검진될 확률 1%

어떤 사람이 질병에 걸렸다고 검진결과가 나왔을 때, 실제로 감염되었을 확률은?

- <img src="https://render.githubusercontent.com/render/math?math=\theta"> : 발병 사건이라 정의 (관찰 불가)
- <img src="https://render.githubusercontent.com/render/math?math=\mathcal D"> : 테스트 결과라 정의 (관찰 가능)
- 사전확률 <img src="https://render.githubusercontent.com/render/math?math=P(\theta)"> = 0.1
- 가능도 <img src="https://render.githubusercontent.com/render/math?math=P(\mathcal D|\theta)"> = 0.99
- 가능도 <img src="https://render.githubusercontent.com/render/math?math=P(\mathcal D|\neg\theta)"> = 0.01
- evidence <img src="https://render.githubusercontent.com/render/math?math=P(\mathcal D)=\sum_{\theta}P(\mathcal D|\theta)P(\theta)"> = 0.99X0.1 + 0.01X0.9 = 0.108
- <img src="https://render.githubusercontent.com/render/math?math=P(\theta|\mathcal D)=0.1\times\frac{0.99}{0.108}\approx0.916">
  <br>

새로운 데이터가 들어왔을때, 앞서 계산한 사후확률을 사전확률로 사용하여 갱신된 사후확률을 계산할 수 있다.

## Deep Learning

### AI, ML, DL

> Artificial Intelligence : Mimic human intelligence
>
> > Machine Learning : Data-driven approach
> >
> > > Deep Learning : Neural network

## Tech

- 구현 능력
- 수학 능력
- 최신 논문

## Key Components

- data
- model
- loss
- algorithm

## Loss

### MSE

regression task  
<img src="https://render.githubusercontent.com/render/math?math=\text{MSE}=\frac{1}{N}\sum^{N}_{i=1}\sum^{D}_{d=1}(y^{(d)}_i-\hat y^{(d)}_i)^2">

### CE

classification task  
<img src="https://render.githubusercontent.com/render/math?math=\text{CE}=-\frac{1}{N}\sum^{N}_{i=1}\sum^{D}_{d=1}y^{(d)}_i\log\hat y^{(d)}_i">

### MLE

probability task  
<img src="https://render.githubusercontent.com/render/math?math=\text{MLE}=\frac{1}{N}\sum^{N}_{i=1}\sum^{D}_{d=1}\log \mathcal{N}(y^{(d)}_i;-\hat y^{(d)}_i,1)">

## Pytorch

밑바닥부터 코드를 작성할 경우, 커뮤니티도 없고, 공유도 힘들다.  
그래서 deep learning 의 구현은 대부분 프레임워크를 사용한다.  
현재 TensorFlow, Pytorch 두 프레임워크가 주를 이룬다.

## Team

- kaggle - titanic 스터디에 대한 이야기
