# Week 5 - Day 22

## Introduction
### Lecture
- 검색 엔진에서는 그래프를 어떻게 활용할까?
- 그래프를 바이럴 마케팅에 어떻게 활용할까?

## PageRank

### 검색 엔진
웹은 웹페이지(정점)와 하이퍼링크(간선)로 구성된 방향성 있는 그래프이다.  
이런 특성을 활용해 페이지랭크 방식으로 검색 엔진을 만든다.  

초기 검색 엔진은 다음과 같은 방식들을 사용했지만, 관련성과 신뢰성에 문제가 있었다.  
- 웹을 카테고리 디렉토리로 정리
- 키워드에 의존한 검색

페이지랭크는 투표와 임의보행 두가지 관점에서 정의할 수 있다.  

### 투표
- 웹페이지가 하이퍼링크를 통해 투표한다.  
- 투표하는 웹페이지의 관련성과 신뢰성에 따라서 가중 투표를 한다.  
- 나가는 이웃에게 ```(자신의 페이지랭크 점수) / (나가는 이웃의 수)``` 만큼의 가중치로 투표한다.  
- 페이지랭크 점수 : <img src="https://render.githubusercontent.com/render/math?math=r_j=\sum_{i\in N_{in}(j)}\frac{r_i}{d_{out}(i)}">

#### 임의보행 (Random Walk)
- 임의보행을 통해 웹을 서핑하는 웹서퍼를 가정 : 웹페이지에 있는 하이퍼링크 중 하나를 균일한 확률로 클릭하는 방식으로 웹서핑
- 웹서퍼가 t번쨰 방문한 웹페이지가 웹페이지 i일 확률을 p_i(t)라고 가정 : p(t)는 길이가 웹페이지 수와 같은 확률분포 벡터가 된다.  

- t가 무한히 커지면 확률분포 p(t)는 수렴 : p(t+1)=p(t)=p
- 정상분포 p : <img src="https://render.githubusercontent.com/render/math?math=p_j(t+1)=\sum_{i\in N_{in}(j)}\frac{p_i(t)}{d_{out}(i)}\rightarrow \sum_{i\in N_{in}(j)}\frac{p_i}{d_{out}(i)}">

### 계산
#### 반복곱 (Power Iteration)  
1. 각 웹페이지 i의 페이지랭크 점수 <img src="https://render.githubusercontent.com/render/math?math=r^{(0)}_i">를 동일하게 ```1 / (웹페이지의 수)```로 초기화
1. <img src="https://render.githubusercontent.com/render/math?math=r^{(t%2B1)}_i=\sum_{i\in N_{in}(j)}\frac{r^{(t)}_i}{d_{out}(i)}"> 각 웹페이지의 페이지랭크 점수 갱신
1. <img src="https://render.githubusercontent.com/render/math?math=r^{(t)}_i\approx r^{(t+1)}_i"> 페이지랭크 점수가 수렴하면 종료, 아니면 2로 돌아간다.

#### 문제점  
- 스파이더 트랩 (spider trap) : 들어오는 간선은 있지만, 나가는 간선은 없는 정점 집합이 있을 경우 수렴을 보장하지 않는다.  
- 막다른 정점 (dead end) : 들어오는 간선은 있지만, 나가는 간선은 없는 정점이 있을 경우 합리적인 점수를 보장하지 않는다.  

#### 순간이동(Teleport)
스파이더 트랩, 막다른 정점 문제를 해결하기 위해 사용한다.  
1. 현재 웹페이지에 하이퍼링크가 없으면 임의의 웹페이지로 순간이동
1. 현재 웹페이지에 하이퍼링크가 있으면 앞면이 나올 확률이 α인 동전을 던진다.
1. 동전이 앞면이면 하이퍼링크 중 하나를 균일한 확률로 선택
1. 뒷면이라면 임의의 웹페이지로 순간이동  
- <img src="https://render.githubusercontent.com/render/math?math=r_j=\sum_{i\in N_{in}(j)}(\alpha\frac{r_i}{d_{out}(i)})(1-\alpha)\frac{1}{|V|}">


## 그래프를 통한 전파
### 의사결정 기반의 전파 모형
주변의 의사결정이 자신의 의사결정에 영향을 주는 경우에 사용한다.  

의사결정 기반 전파 모형에는 선형 임계치 모형 (Linear Threshold Model)이 있다.
- 각 정점에는 선택지 A, B가 존재
- 각 정점은 이웃 중 A를 선택한 비율이 임계치 q를 넘을 때만 A를 선택

### 확률적 전파 모형 
확률적 과정인 경우에 사용한다.  

확률적 전파 모형에는 독립 전파 모형 (Independent Cascade Model)이 있다.  
- 간선 (u,v) : 정점 u의 정점 v로의 전파
- 가중치 p_uv : 간선(u,v)의 가중치 (전파할 확률)
- 서로 다른 이웃이 전파될 확률은 독립


### 전파 최대화
- 시드 집합 (Seed set) : 초기 전파자
- 전파 최대화 (influence maximazation) 문제 : 그래프, 전파 모형, 시드 집합의 크기가 주어졌을 때, 전파를 최대화하는 시드집합을 찾는 문제
- 최고의 시드 집합을 찾는것은 불가능하기 때문에 근사치를 사용한다.
- 정점 중심성 휴리스틱 : 정점의 중심성(페이지랭크, 연결중심성, 근접중심성, 매개중심성)이 높은 순서로 정점을 선택하는 방법
- 탐욕 알고리즘


## Team
- 각각의 학습 방법 이야기

