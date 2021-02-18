# Week 4 - Day 18

## Introduction
### Lecture
- Sequence to Sequence with Attention
- Beam Search and BLEU
- Seq2Seq 구현
- Seq2Seq with Attention 구현

## Attention
encoder, decoder 구조에서 RNN(LSTM, GRU)은 hidden state vector에 모든 정보를 저장해야 한다.  
하지만 sequence가 길어지면 오래된 정보는 변질, 소실의 가능성이 있다.  

이러한 문제를 해결해기 위해서 attention mechanism을 사용한다.  
attention mechanism은 encoder를 만드는 과정에서의 hidden state vector 전체를 decoder에 input으로 제공하고 time step 마다 사용한다.  

attention model은 encoder의 hidden state vector들과 decoder의 hidden state vector의 유사도를 구하여 가중치로 사용한다.  
유사도를 구하는 방법은 내적, concat->neural network 등이 있다.  
<img src="https://render.githubusercontent.com/render/math?math=\text{score}(h_t,\bar{h}_s)=\begin{cases}h^T_t \bar{h}_s %26 dot\\h^T_t W_a \bar{h}_s %26 general\\v^T_a \tanh(W_a[h^T_t %3B \bar{h}_s]) %26 concat\end{cases}">

attention model은 backpropagation 과정에서 time step 전체를 거치지 않고 attention 경로를 사용하기 때문에 gradient vanishing, exploding 문제가 발생하지 않는다.  


## Beam Search
### Greedy Decoding
time step 마다 하나의 단어만 고려하는 방법  

### Exhaustive Search
time step 마다 가능한 모든 조합을 고려하는 방법  
<img src="https://render.githubusercontent.com/render/math?math=P(y|x)=P(y_1|x)P(y_2|y_1,x)P(y_3|y_2,y_1,x)\dots P(y_T|y_{T-1},\dots,y_1,x)=\prod_1^TP(y_T|y_{T-1},\dots,y_1,x)">

### Beam Search
greedy decoding과 exhaustive search 중간의 방법  
time step 마다 k개의 경우의 수를 고려하고 가장 확률이 높은 것을 선택한다.  

<img src="https://render.githubusercontent.com/render/math?math=score(y_1,\dots,y_t)=\log P_{LM}(y_1,\dots,y_t|x)=\sum^t_{i=1}\log P_{LM}(y_i|y_1,\dots,y_{i-1},x)"><br>
beam search 과정에서 step이 길어질수록 score가 낮게 나오기 때문에 균형을 맞추기 위해 step(단어 수) 만큼 나누어 준다.  
<img src="https://render.githubusercontent.com/render/math?math=score(y_1,\dots,y_t)=\frac{1}{t}\sum^t_{i=1}\log P_{LM}(y_i|y_1,\dots,y_{i-1},x)">


## BLEU Score
자연어 생성 모델의 품질, 결과의 정확도를 평가하는 척도  
softmax 방식으로 평가하면 단어의 위치 같은 작은 차이에도 큰 오차가 생긴다.  
BLEU score는 생성한 sequence 문장과 ground truth 문장을 비교하는 방법이다.  

- reference : ground truth 문장
- prediction : 생성 문장
- \# correct words : prediction에서 맞춘 단어 수
- precision : 정밀도 
- recall : 재현율

<img src="https://render.githubusercontent.com/render/math?math=precision=\frac{\text{%23(correct words)}}{\text{length of prediction}}"><br>

<img src="https://render.githubusercontent.com/render/math?math=recall=\frac{\text{%23(correct words)}}{\text{length of reference}}"><br>

- 산술평균 : <img src="https://render.githubusercontent.com/render/math?math=\frac{a%2Bb}{2}">
- 기하평균 : <img src="https://render.githubusercontent.com/render/math?math=\sqrt{ab}">
- 조화평균 : <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{\frac{\frac{1}{a}%2B\frac{1}{b}}{2}}">


<img src="https://render.githubusercontent.com/render/math?math=F-measure=\frac{precision\times recall}{\frac{1}{2}(precision%2Brecall)}">

평균 방식만으로는 문법적으로 맞지 않는 문장이라도 단어만 같으면 score가 높게 나오는 문제가 있다.  

BLEU score는 N-gram과 brevity penalty를 사용한다.  
- N-gram : 연속된 n개의 단어의 일치율 평가 (BLEU score는 1-gram ~ 4-gram 기하평균을 사용)  
- brevity penalty : ground truth 보다 짧은 단어를 예측했을 경우 값을 낮춘다. 

<img src="https://render.githubusercontent.com/render/math?math=BLEU=\min(1, \frac{\text{length of predictoin}}{\text{length of reference}})(\prod_{i=1}^4precision_i)^{\frac{1}{4}}">

## Team
- 과제 이야기
- 이후 피어세션 진행 방식 이야기
