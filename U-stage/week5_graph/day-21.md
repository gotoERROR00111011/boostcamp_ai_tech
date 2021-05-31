# Week 5 - Day 21

## Introduction

### Lecture

- Week5 Overview
- 그래프란 무엇이고 왜 중요할까?
- 실제 그래프는 어떻게 생겼을까?
- 그래프를 컴퓨터 언어로 표현하기 & 페이지랭크 알고리즘 구현하기

## Graph

graph는 정점 집합과 간선 집합으로 이루어진 수학적 구조이다.  
graph는 복잡계(complex system)를 효과적으로 표현하고 분석하기 위한 언어이다.  
복잡계는 구성요소 간의 상호작용으로 이루어진다.

```
ex)
- internet
- web
- 뇌 (뉴런)
- 지식 그래프
- 화학 분자
- 단백질 상호작용
- 이미지 분해
```

- `G=(V,E)` 그래프 : graph, network 라 부른다.
- `V` 정점 : vertex, node 라 부른다.
- `E` 간선 : edge, link 라 부른다.

### 용어

- 이웃(neighbor) : 해당 정점과 연결된 다른 정점을 의미, `N(v), N_v`, `N_out(v), N_in(v)`으로 표기
- 경로(path) 정점 u와 v의 사이의 경로(path)는 아래 조건을 만족하는 순열(sequence)이다.
  - u에서 시작하여 v에서 끝나야한다.
  - 순열에서 연속된 정점은 간선으로 연결되어 있어야한다.
- 경로의 길이 : 해당 경로 상에 놓이는 간선의 수로 정의
- 거리(distance) : 정점 u와 v사이의 최단 경로의 길이
- 지름(diameter) : 정점 간 거리의 최댓값
- 연결성(degree) : 해당 정점과 연결된 간선의 수를 의미, `d(v), d_v, |N(v)|`로 표기
- 연결요소 (connected component) : 다음 조건들을 만족하는 정점들의 집합을 의미한다.
  1. 연결 요소에 속하는 정점들은 경로로 연결될 수 있다.
  1. 1의 조건을 만족하면서 정점을 추가할 수는 없다.
- 군집(community)이란 다음 조건을 만족하는 정점들의 집합이다.
  - 집합에 속하는 정점 사이에는 많은 간선이 존재한다.
  - 집합에 속하는 정점과 그렇지 않은 정점 사이에는 적은 수의 간선이 존재한다.
- 지역적 군집 계수(local clustering coefficient) : 한 정점에서 군집의 형성 정도를 측정한다.
  - 정점 i의 지역적 군집 계수는 정점 i의 이웃 쌍 중 간선으로 직접 연결된 것의 비율을 의미한다.
- 전역 군집 계수(global clustering coefficient) : 전체 그래프에서 군집의 형성 정도를 측정한다.
  - 그래프의 전역 군집 계수는 각 정점에서의 지역적 군집 계수의 평균이다.

### Directed Graph, Undirected Graph

간선에 방향이 있는 그래프와 없는 그래프

### Weighted Graph, Unweighted Graph

간선에 가중치가 있는 그래프와 없는 그래프

### Unpartite Graph, Bipartite Graph

단일 종류의 정점을 가지는 그래프, 두 종류의 정점을 가지는 그래프

## Graph의 표현 및 저장

### NetworkX

python의 graph 라이브러리

### Edge List

그래프를 간선의 리스트로 저장

- 두 정점들의 순서쌍으로 저장 : (노드, 노드)
- 방향성이 있는 경우 순서대로 저장 : (출발점, 도착점)

### Adjacent List

각 정점의 이웃들을 리스트로 저장  
각 정점의 나가는 이웃과 들어오는 이웃을 각각 리스트로 저장

### Adjacency Matrix

(정점 수)\*(정점 수) 크기의 행렬

방향이 없는 경우  
정점 i와 j사이에 간선이 있는 경우, 행렬의 (i행 j열)(j행 i열) 원소가 1  
정점 i와 j사이에 간선이 없는 경우, 행렬의 (i행 j열)(j행 i열) 원소가 0

방향이 있는 경우  
정점 i에서 j로의 간선이 있는 경우, 행렬의 i행 j열 원소가 1  
정점 i에서 j로의 간선이 없는 경우, 행렬의 i행 j열 원소가 0

## Real Graph

- real graph : 다양한 복잡계로 부터 얻어진 그래프
- random garph : 확률적 과정을 통해 생성한 그래프

### 작은 세상 효과 (Small-World Effect)

임의의 두 사람을 골랐을 때, 몇 단계의 지인을 걸쳐 연결되어 있을까?  
다양한 실험 결과로, 적은 단계로 많은 사람들과 연결되어 있다는 것을 알 수 있다.

### 연결성의 두터운 꼬리 분포

실제 그래프의 연결성 분포는 heavy tail을 갖는다. 즉, 연결성이 매우 높은 hub 정점이 존재한다.  
랜덤 그래프의 연결성 분포는 높은 확률로 정규 분포와 유사하다.

### 거대 연결 요소 (Giant Connected Component)

거대 연결 요소는 대다수의 정점을 포함한다.

### 군집 구조

실제 그래프에서는 군집 계수가 높다. 즉, 많은 군집이 존재한다.  
동질성(homophily) : 서로 유사한 정점끼리 간선으로 연결될 가능성이 높다.  
전이성(Transitivity) : 공통 이웃이 있는 경우, 공통 이웃이 매개 역할을 할 수 있다.

## Graph & AI

### Node Classification

- SNS 성향 분류
- 단백질 상호작용 분석 - 단백질 역할 분류

### Link Prediction

- graph 경향 분석
- node 연결 예측

### Community Detection

- 군집분석
- 연결관계로 사회적 무리(social circle) 분석

### Ranking, Information, Retrieval

- web에서 중요한, 관계있는 page 찾기

### Information Cascading, Viral Marketing

- 정보 전달 최대화

## Team

- 모더레이터 담당
