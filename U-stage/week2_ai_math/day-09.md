# Week 2 - Day 09 - Pandas II / 확률론

## Introduction

### Lecture

- pandas II
- 확률론 맛보기

## 딥러닝에서의 확률론

딥러닝은 확률론 기반의 기계학습 이론에 바탕을 두고 있다.  
loss function들의 작동 원리는 데이터 공간을 통계적으로 해석해서 유도  
L2 norm은 예측오차의 분산을 최소화하는 방향으로 학습 유도  
cross-entropy는 모델 예측의 불확실성을 최소화하는 방향으로 학습 유도

## 확률분포

### 이산확률변수

확률변수가 가질 수 있는 경우의 수를 모두 고려하여 확률을 더해서 모델링한다.  
<img src="https://render.githubusercontent.com/render/math?math=P(X\in A)=\sum_{x\in A}P(X=x)">

### 연속확률변수

데이터 공간에 정의된 확률변수의 밀도 위에서의 적분을 통해 모델링한다.  
<img src="https://render.githubusercontent.com/render/math?math=P(X\in A)=\int_{A}P(x)\text{d}x">

### 확률분포는 데이터의 초상화

- <img src="https://render.githubusercontent.com/render/math?math=x\times y"> : 데이터 공간
- <img src="https://render.githubusercontent.com/render/math?math=\mathcal{D}"> : 데이터 공간에서 데이터를 추출하는 분포
- <img src="https://render.githubusercontent.com/render/math?math=(x,y)\sim\mathcal{D}"> : 확률변수 데이터
- <img src="https://render.githubusercontent.com/render/math?math=P(x,y)"> : <img src="https://render.githubusercontent.com/render/math?math=\mathcal{D}">를 모델링

## 조건부확률

<img src="https://render.githubusercontent.com/render/math?math=P(y|x)"> 입력변수 x에 대해 정답이 y일 확률

### 기대값

- 확률분포가 주어지면 데이터를 분석하는데 사용 가능한 여러 종류의 통계적 범함수(statistical functional)를 계산할 수 있다.
- 기대값(expectation)은 데이터를 대표하는 통계량이면서 동시에 확률분포를 통해 다른 통계적 범함수를 계산하는데 사용
- 기대값을 이용해 분산, 첨도, 공분산 등 여러 통계량을 계산할 수 있다.
- 연속확률분포-적분 : <img src="https://render.githubusercontent.com/render/math?math=\mathbb{E}_{x\sim P(X)}[f(x)]=\int_{\mathcal{X}}f(x)P(x)dx">
- 이산확률분포-급수 : <img src="https://render.githubusercontent.com/render/math?math=\mathbb{E}_{x\sim P(X)}[f(x)]=\sum_{x\in\mathcal{X}}f(x)P(x)">

## 몬테카를로(Monte Carlo) 샘플링

확률분포를 모를 때 데이터를 이용하여 기댓값을 계산하려면 몬테카를로 샘플링 방법을 사용해야한다.  
<img src="https://render.githubusercontent.com/render/math?math=\mathbb{E}_{x\sim P(X)}[f(x)]\approx\frac{1}{N}\sum^N_{i=1}f(x^{(i)}),\,\,\,x^{(i)}\sim P(x)">

## Team

- 스터디 논의
