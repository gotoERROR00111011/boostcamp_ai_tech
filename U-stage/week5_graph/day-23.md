# Week 5 - Day 23

## Introduction

### Lecture

- 그래프의 구조를 어떻게 분석할까?
- 그래프를 추천시스템에 어떻게 활용할까? (기본)

## 군집 (Community)

### 군집이란?

- 집합에 속하는 정점 사이에는 많은 간선이 존재한다.
- 집합에 속하는 정점과 그렇지 않은 정점 사이에는 적은 수의 간선이 존재한다.

### 군집 탐색 (Community Detection) 문제

그래프를 여러 군집으로 잘 나누는 문제

- 배치 모형 (configuration model) : 각 정점의 연결성을 보존한 상태에서, 간선들을 무작위로 재배치하여서 얻은 그래프
- 군집성(modularity) : 배치 모형과의 비교를 통해 통계적 유의성을 판단한다.

### 군집 탐색 알고리즘

#### Girvan-Newman 알고리즘

- 매개 중심성 : 해당 간선이 정점 간의 최단 경로에 놓이는 횟수
- <img src="https://render.githubusercontent.com/render/math?math=\sigma_{i,j}"> : 정점 i로 부터 j로의 최단 경로 수
- <img src="https://render.githubusercontent.com/render/math?math=\sigma_{i,j}(x, y)"> : 간선 (x, y)를 포함한 것
- <img src="https://render.githubusercontent.com/render/math?math=\sum_{i<j}\frac{\sigma_{i,j}(x,y)}{\sigma_{i,j}}"> : 간선 (x, y)의 매개 중심성

- top-down 군집 탐색 알고리즘

1. 전체 그래프에서 시작
1. 매개 중심성이 높은 순서로 간선을 제거 & 군집성 기록
1. 군집성 최대 지점 복원

#### Louvain 알고리즘

- bottom-up 군집 탐색 알고리즘

1. 크기 1의 군집에서 시작
1. 군집성이 최대화 되도록 정점을 기존 혹은 새로운 군집으로 이동
1. 더 이상 군집성이 증가하지 않을 때까지 2를 반복
1. 각 군집을 하나의 정점으로 하는 군집 레벨의 그래프를 얻은 뒤 3을 수행
1. 한개의 정점이 남을 때까지 4를 반복

### 중첩이 있는 군집 탐색

#### 중첩 군집 모형

중첩 군집 탐색은 주어진 그래프의 확률을 최대화하는 중첩 군집 모형을 찾는 과정이다.

1. 각 정점은 여러 개의 군집에 속할 수 있다.
1. 각 군집 A에 속하는 두 정점은 P_A의 확률로 간선으로 직접 연결된다.

#### 완화된 중첩 군집 모형

- 정점이 각 군집에 속해있는 정도를 실수 값으로 표현
- 경사하강법 등을 사용 가능하다.

## 그래프 & 추천시스템

### 내용 기반 추천시스템 (Content Based Recommendation)

- 각 사용자가 구매/만족했던 선택과 유사한 것을 추천하는 것

1. 상품 프로필 수집 : 상품의 특성을 나열한 벡터
1. 사용자 프로필 구성 : 선호한 상품의 상품 프로필을 선호도를 사용하여 가중평균한 벡터
1. 사용자 프로필, 상품 프로필 매칭 : 코사인 유사도 계산 <img src="https://render.githubusercontent.com/render/math?math=\frac{\overrightarrow{u}\cdot\overrightarrow{v}}{||\overrightarrow{u}||\,||\overrightarrow{v}||}">
1. 상품 추천 : 코사인 유사도가 높은 상품 추천

### 협업 필터링 추천시스템

사용자-사용자 협업 필터링

1. 추천의 대상 사용자 x와 유사한 취향의 사용자들을 찾는다.
1. 유사한 취향의 사용자들이 선호한 상품을 찾는다.
1. 상품들을 x에게 추천한다.

취향의 유사성은 상관 계수(Correlation Coefficient)를 통해 측정한다.

- <img src="https://render.githubusercontent.com/render/math?math=r_{xs}"> : 사용자 x의 상품 s에 대한 평점
- <img src="https://render.githubusercontent.com/render/math?math=\overline{r_{x}}"> : 사용자 x가 매긴 평균 평점
- <img src="https://render.githubusercontent.com/render/math?math=S_{xy}"> : 사용자 x와 y가 공동 구매한 상품들
- <img src="https://render.githubusercontent.com/render/math?math=sim(x,y)=\frac{\sum_{S\in S_{xy}}(r_{xs}-\overline{r_{x}})(r_{ys}-\overline{r_{y}})}{\sqrt{\sum_{S\in S_{xy}}(r_{xs}-\overline{r_{x}})^2}\sqrt{\sum_{S\in S_{xy}}(r_{ys}-\overline{r_{y}})^2}}"> : 취향의 유사도

- <img src="https://render.githubusercontent.com/render/math?math=N(x%3bs)"> : 상품s를 구매한 사용자 중 x와 취향이 가장 유사한 k명의 사용자
- <img src="https://render.githubusercontent.com/render/math?math=\hat r_{xs}=\frac{\sum_{y\in N(x%3bs)}sim(x,y)\cdot r_{ys}}{\sum_{y\in N(x%3bs)}sim(x,y)}"> : 평점 <img src="https://render.githubusercontent.com/render/math?math=r_{xs}"> 추정

### 추천 시스템 평가

1. 데이터 분리 : 훈련 데이터와 평가 데이터로 분리
1. 평가 데이터는 주어지지 않았다고 가정
1. 훈련 데이터로 평가 데이터 추정
1. 추정한 평가와 실제 평가 데이터 비교, 오차 측정

## Team

- P stage 코스 이야기
- 마스터 클래스 질문 선정 투표
