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



## 조건부확률
<img src="https://render.githubusercontent.com/render/math?math=P(y|x)"> 입력변수 x에 대해 정답이 y일 확률  


## 몬테카를로(Monte Carlo) 샘플링
확률분포를 모를 때 데이터를 이용하여 기댓값을 계산하려면 몬테카를로 샘플링 방법을 사용해야한다.  


## Team
- 스터디 논의
