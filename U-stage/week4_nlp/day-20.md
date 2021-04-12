# Week 4 - Day 20

## Introduction
### Lecture
- Self-supervised Pre-training Models
- Advanced Self-supervised Pre-training Models
- HuggingFace's Transformers 1
- HuggingFace's Transformers 2


## Self-Supervised Pre-Training Models

## GPT-1
1. input : text & position embed
1. attention block * 12
    1. masked multi self attention
    1. residual connection
    1. layer norm
    1. feed forward  
    1. residual connection
    1. layer norm
1. output
    - text prediction
    - task classifier

### Special Tokens
GPT-1은 token을 활용한다.  
- exract token : EOS 기능 + 최종 output task의 input으로 사용
- delim token : 목적에 따라 문장 사이에서 문장 구분 역할을 한다.

### Pre-Training Task
```
Classification
[Start] [Text] [Extract] [Transformer] [Linear]

Entailment
[Start] [premise] [Delim] [hypothesis] [Extract] [Transformer] [Linear]

Similarity
[Start] [Text 1] [Delim] [Text 2] [Extract] [Transformer] [Linear]
[Start] [Text 2] [Delim] [Text 1] [Extract] [Transformer]

Multiple choice
[Start] [Context] [Delim] [Answer 1] [Extract] [Transformer]
[Start] [Context] [Delim] [Answer 2] [Extract] [Transformer] [Linear]
[Start] [Context] [Delim] [Answer N] [Extract] [Transformer]
```

## GPT-2
- GPT-1 보다 많은 transformer layer 사용
- GPT-1 보다 많은 data, quality가 높은 data를 사용


## GPT-3
GPT-3는 GPT-2 보다여러 요소를 증가시켜 개선한 model 이다.  
- 더 많은 데이터
- 더 많은 parameters
- 더 많은 attention layer
- 더 큰 batch size

### Few-Shot Learning
GPT-3는 task에 대한 별도의 fine-tuning 없이, 혹은 예제만 가지고도 성능을 보여준다.  
- zero-shot : 예제가 없는 경우
- one-shot : 예제를 하나만 주는 경우
- few-shot : 예제를 몇개만 주는 경우


## BERT
### Input
- CLS toekn : classification embedding
- SEP token : packed sentence embedding
- wordpiece embedding (sub-word)
- learned positional embedding
- segement embedding : 문장 구분에 사용

### Pre-Training Task : Masked-Language Model
sentence의 단어의 일정 비율(15%)을 random하게 mask하고 단어를 예측하는 방식으로 학습한다.  

실제 적용 시 항상 mask가 주어지지는 않으므로 다른 방식도 사용한다.  
- 80% : mask
- 10% : random word
- 10% : 원래의 단어 그대로 사용 (잘못된 처리 테스트)

### Pre-Training Task : Next Sentence Prediction
두 sentence의 순서가 맞는지 학습한다.  
```
Intput:
[CLS]
the man went to [MASK] store [SEP] 
he bought a gallon [MASK] milk [SEP]

Label:
IsNext
```


## ALBERT (A Lite BERT)
### Factorized Embedding Parameterization
input에 사용되는 word embedding의 dim을 줄이는 방법  
1. embedding dim을 BERT보다 작게 설정한다.
1. 원래 크기로 선형변환하는 W를 사용한다.
- BERT : (vocab_size * hidden_size) 
- ALBERT : (vocab_size * embed_size + embed_size hidden_size)

### Cross-Layer Parameter Sharing
반복적으로 사용하는 구조의 network의 parameter를 공유해도 큰 성능저하는 없다.  
- shared-FFN : feed-forward network parameter
- shared-attention : attention parameter
- all-shared : both

### Pre-Training Task : Sentence Order Prediction
next sentence prediction는 두 문장이 별도의 문서의 정보일 경우 true, false 구분이 쉬워서 학습이 잘 진행되지 않는다.  
이러한 문제를 해결하기위해 동일 문서의, 연속된 sentence의 순서를 바꾸어 true, false를 구분하는 sentence order prediction 을 사용한다.  


## ELECTRA
GAN의 아이디어를 사용했다.  
- generator : 단어를 복원하는 모델 (ex BERT:masked language)  
- discriminator (ELECTRA) : 복원한 단어가 원본과 일치하는지 판별  

최종 discriminator를 사용한다.  


## Light-Weight Models
model의 성능을 유지하면서 크기와 연산을 빠르게 경량화하는 연구  

knowledge distillation을 사용하는 방법이 있다.  
teacher network의 결과를 비교적 경랑화된 student network가 배우는 방식을 사용한다.  

- DistillBERT : teacher의 최종 softmax 결과를 student의 ground truth로 사용
- TinyBERT : teacher의 전체 parameter를 student가 배우도록 한다. (teacher->student : linear network)

## Team
- 과제 관련 이야기

