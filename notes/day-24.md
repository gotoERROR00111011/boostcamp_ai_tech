# Week 5 - Day 24

## Introduction
### Lecture
- 그래프의 정점을 어떻게 벡터로 표현할까?
- 그래프를 추천시스템에 어떻게 활용할까? (심화)


## Graph & Vector
### 정점 표현 학습 or 정점 임베딩(Node Embedding)
- 그래프의 정점들을 벡터 형태로 표현하는 것  
- <img src="https://render.githubusercontent.com/render/math?math=z_u"> : 각 정점 u에 대한 임베딩
- 그래프에서의 정점간의 유사도를 임베딩 공간에서도 보존하는 방식으로 벡터화
- <img src="https://render.githubusercontent.com/render/math?math=similarty(u,v)\approx z^T_v z_u"> : 정점 u, v의 유사도

### 인접성 기반 접근법
- 두 정점이 인접할 때 유사하다고 간주
- <img src="https://render.githubusercontent.com/render/math?math=A_{u,v}"> : 인접행렬에서 유사도, 정점이 인접하면 1 아니면 0
- <img src="https://render.githubusercontent.com/render/math?math=L=\sum_{(u,v)\in V\times V}||z^T_u z_v-A_{u,v}||^2"> : 손실함수

### 거리 기반 접근법
- 두 정점 사이의 거리가 충분히 가까우면 유사하다고 간주

### 경로 기반 접근법
- 두 정점 사이에 경로가 많을 수록 유사하다고 간주
- <img src="https://render.githubusercontent.com/render/math?math=A^k_{u,v}"> : 두 정점 u,v 사이의 경로 중 거리가 k 인 수
- <img src="https://render.githubusercontent.com/render/math?math=L=\sum_{(u,v)\in V\times V}||z^T_u z_v-A^k_{u,v}||^2"> : 손실함수

### 중첩 기반 접근법
- 두 정점이 많은 이웃을 공유할 수록 유사하다고 간주
- <img src="https://render.githubusercontent.com/render/math?math=N(u)"> : 정점 u의 이웃의 집합
- <img src="https://render.githubusercontent.com/render/math?math=S_{u,v}=|N(u)\cap N(v)|=\sum_{w\in N(u)\cap N(v)}1"> : 두 정점의 공통 이웃의 수
- <img src="https://render.githubusercontent.com/render/math?math=L=\sum_{(u,v)\in V\times V}||z^T_u z_v-S_{u,v}||^2"> : 손실함수

### Jaccard Similarity
- 공통 이웃의 비율 계산
- <img src="https://render.githubusercontent.com/render/math?math=\frac{N(u)\cap N(v)}{N(u)\cup N(v)}">

### Adamic Adar 점수
- 공통 이웃 각각에 가중치를 부여하여 가중합을 계산
- <img src="https://render.githubusercontent.com/render/math?math=\sum_{w\in N(u)\cap N(v)}\frac{1}{d_w}">

### 임의보행 기반 접근법
- 한 정점에서 시작하여 임의보행을 할 때 다른 정점에 도달할 확률을 유사도로 간주
1. 각 정점에서 시작하여 임의보행을 반복
1. 각 정점에서 시작한 임의보행 중에 도달한 정점들의 리스트(<img src="https://render.githubusercontent.com/render/math?math=N_R(u)">)를 구성
1. <img src="https://render.githubusercontent.com/render/math?math=L=\sum_{u\in V}\sum_{v\in N_R(u)}-\log(P(v|z_u))"> : 손실함수
- <img src="https://render.githubusercontent.com/render/math?math=P(v|z_u)=\frac{\exp(z^T_uz_v)}{\sum_{n\in V}\exp(z^T_uz_n)}">

#### DeepWalk
- 기존 임의보행 사용  

#### Node2Vec
- 2차 치우친 임의보행 (second-order biased random walk) 사용
- 현재 정점과 직전에 머물렀던 정점을 모두 고려하여 다음 정점 선택
- 직전 정점의 거리를 기준으로 경우를 구분하여 차등적인 확률을 부여
- 부여하는 확률에 따라서 다른 종류의 임베딩을 얻는다.  

#### 손실 함수 근사
- 모든 정점에 대해서 정규화하는 대신 몇개의 정점을 뽑아서 비교하는 형태
- 네거티브 샘플 : 뽑힌 정점
- <img src="https://render.githubusercontent.com/render/math?math=\log\left(\frac{\exp(z^T_uz_v)}{\sum_{n\in V}\exp(z^T_uz_n)}\right)\approx \log(\sigma(z^T_uz_v))-\sum^k_{i=1}\log(\sigma(z^T_uz_{n_i})),n_i\sim P_V">

### 변환식 정점 표현 학습과 귀납식 정점 표현 학습
- 변환식(Transductive) 방법 : (거리, 경로, 중첩, 임의보행) 학습의 결과로 임베딩 자체를 얻는다.
- 귀납식 (Inductive) : 인코더 - 정점을 임베딩으로 변환시키는 함수  
- <img src="https://render.githubusercontent.com/render/math?math=ENC(v)=z_v">


## 넷플릭스 챌린지
### Data
- training data : 2000년~2005년, 48만명 사용자, 1만 8천개 영화, 1억개 평점
- test data : 각 사용자의 최신 평점 280만개

### Goal
- 2006년~2009년, 2700팀 참여  
- 추천 시스템의 성능을 10% 이상 향상시키는 것  
- 평균 제곱근 오차 0.9514를 0.8563까지 낮출 경우 상금 100만불
- 1.1296 : 전체 평점 평균
- 1.0651 : 사용자별 평점 평균
- 1.0533 : 영화 별 평점 평균
- 0.9514 : 당시 넷플릭스 추천 시스템
- 0.94   : 기본 협업 필터링
- 0.90   : 잠지 인수 모형
- 0.89   : 사용자와 상품의 편향을 고려한 잠재 인수 모형
- 0.876  : 시간적 편향을 고려한 잠재 인수 모형
- 0.8563 : 목표 오차

### 잠재 인수 모형 (Latent Factor Model)
- 사용자와 상품을 벡터로 표현
- 잠재 인수 : 학습한 인수
- 사용자와 상품의 내적이 평점과 유사하도록 임베딩
- <img src="https://render.githubusercontent.com/render/math?math=p_x"> : 사용자 x의 임베딩
- <img src="https://render.githubusercontent.com/render/math?math=q_i"> : 상품 i의 임베딩
- <img src="https://render.githubusercontent.com/render/math?math=r_xi"> : 사용자 x의 상품 i에 대한 평점
- <img src="https://render.githubusercontent.com/render/math?math=p^T_xq_i\approx r_{xi}"> : 임베딩 목표
- <img src="https://render.githubusercontent.com/render/math?math=\lambda_1, \lambda_2"> : 정규화의 세기
- <img src="https://render.githubusercontent.com/render/math?math=\(r_{xi}-p^T_xq_i)^2"> : 오차
- <img src="https://render.githubusercontent.com/render/math?math=\[\lambda_1\sum_x||p_x||^2%2B\lambda_2\sum_i||q_i||^2]"> : 모형복잡도
- <img src="https://render.githubusercontent.com/render/math?math=\sum_{(i,x)\in R}(r_{xi}-p^T_xq_i)^2%2B[\lambda_1\sum_x||p_x||^2%2B\lambda_2\sum_i||q_i||^2]"> : 손실함수

### 고급 잠재 인수 모형
#### 사용자와 상품의 편향을 고려한 짐제 인수 모형
- 각 사용자의 편향은 해당 사용자의 평점 평균과 전체 평점 평균의 차
- 각 상품의 편향은 해당 상품의 평점 평균과 전체 평점 평균의 차
- <img src="https://render.githubusercontent.com/render/math?math=r_{xi}=\mu%2Bb_x%2Bb_i%2Bp^T_xq_i"> : 평점=전체평균+사용자편향+상품편향+상호작용
- <img src="https://render.githubusercontent.com/render/math?math=\sum_{(i,x)\in R}(r_{xi}-(\mu%2Bb_x%2Bb_i%2Bp^T_xq_i)^2%2B[\lambda_1\sum_x||p_x||^2%2B\lambda_2\sum_i||q_i||^2%2B\lambda_3\sum_xb^2_x%2B\lambda_4\sum_ib^2_i])">

### 시간적 편향을 고려한 잠재 인수 모형
- 넷플릭스 시스템 변화로 평균 평점이 크게 상승하는 사건이 있었다.
- 영화의 평점은 출시일 이후 시간이 지남에 따라 상승하는 경향
- <img src="https://render.githubusercontent.com/render/math?math=r_{xi}=\mu%2Bb_x(t)%2Bb_i(t)%2Bp^T_xq_i"> : 평점=전체평균+사용자편향(시간)+상품편향(시간)+상호작용

### Result
- Ensemble 우승


## Team


