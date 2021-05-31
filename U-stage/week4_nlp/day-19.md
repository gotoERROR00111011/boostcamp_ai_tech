# Week 4 - Day 19

## Introduction

### Lecture

- Transformer I
- Transformer II
- Multi-head Attention 구현
- Masked Multi-head Attention 구현

## Transformer

### Self-Attention

동일한 set vector들 내에서 attention을 적용해서 self-attention이라고 부른다.

self-attention에서 input vector들은 상황마다 서로 다른 역할을 한다.

- Queries : key vector와 내적하여 유사도를 측정할 vector
- Keys : query vector와 내적하여 측정한(softmax) 유사도로 value vector의 가중치 결정
- Values : 값 (query, key로 가중치 조정)

softmax는 값이 클수록 비중이 커지기 때문에, query와 key의 dim에 영향을 받지 않도록 <img src="https://render.githubusercontent.com/render/math?math=\sqrt{d_k}">로 나누어 분산을 1로 조정한다.  
<img src="https://render.githubusercontent.com/render/math?math=A(Q,K,V)=softmax(\frac{QK^T}{\sqrt{d_k}})V"><br>

### Long-Term Dependency

self-attention은 encoding vector를 만드는 과정에서 각 vector마다 모든 input을 고려하고, neural network로 가중치를 정한다.  
따라서 sequence의 길이가 길어져서 time step이 멀어져도 정보 손실의 문제가 없다.

### Block-Based Model

transformer는 같은 block이 반복되는 구조이다.

- blcok
  1. multi-head attention
     1. residual connection
     1. layer norm
  1. feed forward
     1. residual connection
     1. layer norm
- block
- ......

### Multi-Head Attention

attention을 여러개의 head로 만들고, 합치는 방법  
서로 다른 측면의 정보를 병렬적으로 추출하기 위해서 사용한다.  
<img src="https://render.githubusercontent.com/render/math?math=\text{MultiHead}(Q,K,V)=\text{Concat}(head_1,\dots,head_h)W^O"><br>
<img src="https://render.githubusercontent.com/render/math?math=head_i=Attention(QW^Q_i,KW^K_i,VW^V_i)"><br>

### Layer Normalization

1. nomalization : input의 각 word vector 마다 평균:0, 분산:1 로 만든다.
1. affine transformation : normalize된 전체 vector들을 node 단위로 a(분산)x + b(평균) 형태로 변환한다.

### Positional Encoding

transformer에서 sequence 정보를 고려하기 위해서 사용한다.  
각각의 주기가 다른 sin, cos을 dim의 수만큼 만들고 이것을 input vector에 더하는 상수로 사용한다.

### Decoder

SOS token을 시작으로 순차적으로 생성한다.

- loop
  1. masked multi-head attention
     1. residual connection
     1. layer norm
  1. multi-head attention (decoder:query, encoder:key,value)
     1. residual connection
     1. layer norm
  1. feed forward
     1. residual connection
     1. layer norm
  1. linear
  1. softmax

#### Multi-Head Attention

decoder에서 만들어진 hidden state vector가 query로 사용되고, encoder의 최종 vector가 key, value 로 사용된다.

#### Masked Self-Attention

실제 사용단계에서 이후의 입력을 미리 알 수 없기 때문에 사용하는 방법이다.

1. 전체를 입력으로 사용
1. 현재의 time step 이후의 정보를 제외하고, 남은 값을 nomalize

| example | \<SOS\> | key 1 | key 2 |
| ------- | ------- | ----- | ----- |
| \<SOS\> | 0.91    | 0.05  | 0.04  |
| query 1 | 0.60    | 0.20  | 0.20  |
| query 2 | 0.25    | 0.31  | 0.44  |

| masked  | \<SOS\> | key 1 | key 2 |
| ------- | ------- | ----- | ----- |
| \<SOS\> | 1       | X     | X     |
| query 1 | 0.75    | 0.25  | X     |
| query 2 | 0.25    | 0.31  | 0.44  |

## Team

- 강의 내용 질문 답변
