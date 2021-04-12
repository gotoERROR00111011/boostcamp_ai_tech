# Week 4 - Day 16

## Introduction
### Lecture
- Week4 Overview
- Intro to NLP, Bag-of-Words
- Word Embedding
- Naive Bayes classifier 구현
- Word2Vec 구현

## Natural Language
### Natural Language Processing
- conferences : ACL, EMNLP, NAACL
### Text Mining
- conferences : KDD, The WebConf, WSDM, CIKM, ICWSM
### Information Retrieval
- conferences : SIGIR, WSDM, CIKM, RecSys

## Bag-of-Words
word 들의 출현 빈도를 표현하는 방법  
1. input sentence의 vocabulary를 만든다.
1. vocabulary를 one-hot encoding
1. sentence의 각 words(one-hot vector)를 더한다. 

one-hot vector에서는 모든 단어 사이의 거리가 <img src="https://render.githubusercontent.com/render/math?math=\sqrt 2">이고, 유사도는 0이다.  

### NaiveBayes Classfier
- <img src="https://render.githubusercontent.com/render/math?math=c"> : class
- <img src="https://render.githubusercontent.com/render/math?math=d"> : document
- <img src="https://render.githubusercontent.com/render/math?math=w"> : word

<img src="https://render.githubusercontent.com/render/math?math=C_{MAP}=\underbrace{\text{argmax}}_{c\in C}P(c|d)=\underbrace{\text{argmax}}_{c\in C}\frac{P(d|c)P(c)}{P(d)}=\underbrace{\text{argmax}}_{c\in C}P(d|c)P(c)"><br>
<img src="https://render.githubusercontent.com/render/math?math=P(d|c)P(c)=P(w_1,w_2,\dots,w_n|c)P(c)\rightarrow P(c)\prod_{w_i\in W}P(w_i|c)"> 값이 가장 큰 class로 분류한다.  
<img src="https://render.githubusercontent.com/render/math?math=P(w_i|c_j)">는 i번째 단어가 해당 sentence에 나온 count를, class j로 분류된 sentence 전체의 단어 count로 나눈 값이다.  


## Word Embedding
word들을 특정 차원의 공간에 한점 혹은 점을 나타내는 vector로 변환해주는 방법  
유사한 의미의 단어를, 유사한 위치의 좌표로 mapping해서 word들의 의미상의 유사도를 반영한 vector 표현이다.  

### Word2Vec
같은 sentence 안에서 인접한 word 사이에 연관성이 있을것이라 가정한 방법  

1. input sentence로 vocabulary 생성
1. one-hot encoding
1. sliding window 방식으로 input(word), output(input에 인접한 word) 학습 데이터를 만든다.
1. neural network 학습

실제 사용에서는 학습된 network의 weight를 사용한다.

Word2Vec의 구현은 CBOW, Skip-gram으로 가능하다.  

- CBOW : 주변 단어로 중심 단어를 예측한다.  
- Skip-gram : 중심 단어로 주변 단어를 예측한다.  

### GloVe
input, output 쌍이 한 window 내에서 몇번 나왔는지 사전에 count 하여, input, output vector의 내적과 유사하게 되도록 loss를 설정하는 방법  
<img src="https://render.githubusercontent.com/render/math?math=J(\theta)=\frac{1}{2}\sum^W_{i,j=1}f(P_{ij})(u^T_iv_j-\log P_{ij})^2"><br>


## Team
- 취업에 관한 이야기
- 딥러닝 분야에 대한 이야기
