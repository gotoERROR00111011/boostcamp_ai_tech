# Week 5 - Day 25

## Introduction

### Lecture

- 그래프 신경망이란 무엇일까? (기본)
- 그래프 신경망이란 무엇일까? (심화)

## Graph Neural Network

### 변환식 정점 표현 학습의 한계

- 출력으로 임베딩 자체를 얻는다.
- 학습이 진행된 이후에 추가된 정점에 대해서는 임베딩을 얻을 수 없다.
- 모든 정점에 대한 임베딩을 미리 저장해 두어야한다.
- 정점이 속성(attribute) 정보를 가진 경우에는 활용할 수 없다.

### 귀납식 정점 표현 학습 장점

- GNN
- 출력으로 인코더를 얻는다.
- 학습이 진행된 이후에 추가된 정점에 대해서도 임베딩을 얻을 수 있다.
- 모든 정점에 대한 임베딩을 미리 저장해 둘 필요가 없다.
- 정점이 속성(attribute) 정보를 가진 경우에 이를 활용할 수 있다.
- ENC(v) : 그래프 구조와 정점의 부가정보를 활용하는 복잡한 함수

### 그래프 신경망 구조

- <img src="https://render.githubusercontent.com/render/math?math=A"> : 그래프의 인접행렬 (이진행렬)
- <img src="https://render.githubusercontent.com/render/math?math=X_u"> : 각 정점 u의 속성 m(속성 수)차원 벡터
- 그래프 신경망은 그래프와 정점의 속성 정보를 입력으로 받는다.
- 그래프 신경망은 이웃 정점들의 정보를 집계하는 과정을 반복하여 임베딩을 얻는다.
- 각 집계 단계를 layer라고 부르고, 각 층마다 임베딩을 얻는다.
- 대상 정점마다 집계되는 정보가 상이하다. 대상 정점 별 집계되는 구조를 computation graph라 부른다.
- 서로 다른 대상 정점간에도 층 별 집계함수는 공유한다.

### 집계 함수

1. 이웃들 정보의 평균 계산
1. 신경망에 적용

<img src="https://render.githubusercontent.com/render/math?math=h^0_v=x_v"><br>
<img src="https://render.githubusercontent.com/render/math?math=h^k_v=\sigma\left(W_k\sum_{u\in N(v)}\frac{h^{k-1}_u}{|N(v)|}%2BB_kh^{k-1}_v\right),\forall k>0"><br>

### Loss

- 정점간 거리를 보존하는 것을 목표로 한다.
- <img src="https://render.githubusercontent.com/render/math?math=L=\sum_{(u,v)\in V\times V}||z^T_u z_v-A_{u,v}||^2"> : 인접성 기반
- <img src="https://render.githubusercontent.com/render/math?math=L=\sum_{v\in V}y_v\log(\sigma(z^T_v\theta))+(1-y_v)\log(1-\sigma(z^T_v\theta))"> : 후속 과제 (downstream task)의 손실함수를 이용한 종단종(end-to-end) 학습
- layer 별 집계함수를 공유하기 때문에 전체 정점에 대해서 학습하지 않고, 일부 정점에 대해서만 학습해도 된다.

## Graph Convolutional Network

### 집계 함수

<img src="https://render.githubusercontent.com/render/math?math=h^0_v=x_v"><br>
<img src="https://render.githubusercontent.com/render/math?math=h^k_v=\sigma\left(W_k\sum_{u\in N(v)\cup v}\frac{h^{k-1}_u}{\sqrt{|N(u)||N(v)|}}\right),\forall k\in\left\{1,\dots,K\right\}"><br>
<img src="https://render.githubusercontent.com/render/math?math=z_v=h^K_v"><br>

## GraphSAGE

### 집계함수

<img src="https://render.githubusercontent.com/render/math?math=h^0_v=x_v"><br>
<img src="https://render.githubusercontent.com/render/math?math=h^k_v=\sigma\left([W_k\cdot AGG(\left\{h^{k-1}_u,\forall u\in N(v)\right\}), B_kh^{k-1}_v]\right)"><br>
<img src="https://render.githubusercontent.com/render/math?math=z_v=h^K_v"><br>

- mean : <img src="https://render.githubusercontent.com/render/math?math=AGG=\sum_{u\in N(v)}\frac{h^{k-1}_u}{|N(v)|}">
- pool : <img src="https://render.githubusercontent.com/render/math?math=AGG=\gamma (\left\{Qh^{k-1}_u,\forall u\in N(v)\right\})">
- LSTM : <img src="https://render.githubusercontent.com/render/math?math=AGG=LSTM([h^{k-1}_u,\forall u\in \pi(N(v))])">

## Graph Attention Network

- 기본 그래프 신경망에서는 이웃들의 정보를 동일한 가중치의 평균으로 사용한다.
- GCN에서도 단순히 연결성을 고려한 가중치 평균으로 사용한다.

- GAT 에서는 가중치 자체도 학습

1. <img src="https://render.githubusercontent.com/render/math?math=\tilde h_i=h_iW"> : 해당 층의 정점i의 임베딩에 신경망W를 곱하여 새로운 임베딩을 얻는다.
1. <img src="https://render.githubusercontent.com/render/math?math=e_{ij}=a^T[concat(\tilde h_i,\tilde h_j)]"> : 정점i와 정점j의 새로운 임베딩을 연결한 후 어텐션 계수 내적
1. <img src="https://render.githubusercontent.com/render/math?math=\alpha_{ij}=softmax_j(e_{ij})=\frac{\exp(e_{ij})}{\sum_{k\in N_i}\exp(e_{ik})}"> : softmax

- <img src="https://render.githubusercontent.com/render/math?math=h^\prime_i=concat_{1\leq k\leq K}\sigma(\sum_{j\in N_i}\alpha^k_{ij}h_jW_k)"> : multi-head attention

## 그래프 표현 학습, Graph Embedding

- 그래프 전체를 벡터 형태로 표현하는 것

### Graph Pooling

- 정점 임베딩들로부터 그래피 임베딩을 얻는 과정
- 미분가능한 풀링 (differentiable pooling, diffpool)은 군집 구조를 활용해 임베딩을 계층적으로 집계한다.

## 지나친 획일화 문제 (Over-Smoothing)

- 그래프 신경망 층의 수가 증가하면서 정점의 임베딩이 서로 유사해지는 현상
- 작은 세상 효과와 관련이 있다.
- <img src="https://render.githubusercontent.com/render/math?math=h^{(l%2B1)}_u=h^{(l%2B1)}_u%2Bh^{(l)}_u"> : Residual을 넣는 것으로도 효과는 제한적

- Jumping Knowledge Network : 모든 층의 임베딩을 함께 사용한다.
- APPNP : 0번째 층을 제외하고는 신경망 없이 집계 함수를 단순화

## 그래프 데이터 증강

- 그래프에도 부정확하거나 누락된 간선이 있을 수 있고, 데이터 증강을 통해 보완할 수 있다.
- 임의보행으로 정점간 유사도 계산 -> 유사도가 높은 정점간에 간선 추가

## Team

- 그래프 분야 정리
