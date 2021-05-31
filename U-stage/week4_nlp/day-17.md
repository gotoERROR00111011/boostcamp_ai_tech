# Week 4 - Day 17

## Introduction

### Lecture

- Recurrent Neural Network and Language Modeling
- LSTM and GRU
- Basic RNN 실습
- LSTM, GRU 실습

## Recurrent Neural Network

<img src="https://render.githubusercontent.com/render/math?math=h_t=\tanh(W_{hh}h_{t-1}+W_{xh}x_t)"><br>
<img src="https://render.githubusercontent.com/render/math?math=y_t=W_{hy}h_t"><br>

## Types of RNN

- one to one
- one to many
- many to one
- many to many

## Long Short-Term Memory models

- cell state vector : 핵심적인 정보
- hidden state vector : cell state vector를 필터링한 정보

## Gated Recurrent Units

- LSTM 경량화
- hidden state vector만 사용

basic RNN에서 재귀적으로 곱하여 gradient vanishing, exploding이 발생하지만, LSTM과 GRU에서는 gate를 사용한 새로운 값을 곱하거나 더하기 때문에 문제가 발생하지 않는다.

## Team

- 조교님과 질문, 답변 + 조언
- 마스터 클래스 질문 선정
