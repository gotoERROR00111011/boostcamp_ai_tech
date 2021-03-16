# Week 8 - Day 37

## Introduction
### Lecture

## Hyperparameter
- Parameter search
- Hyperparameter search 
- Neural Architecture Search (NAS)
- NAS for edge devices
    - MnasNet
    - PROXYLESSNAS
    - ONCE-FOR-ALL


## Entropy
- high entropy : 무질서
- low entropy : 질서
- Q(i) : predicted
- P(i) : label
- <img src="https://render.githubusercontent.com/render/math?math=\sum^n_{i=1}{-P(i)}\ln{Q(i)}"> : cross entropy
- <img src="https://render.githubusercontent.com/render/math?math=\sum^n_{i=1}{-P(i)}\ln{P(i)}"> : entropy
- 
- <img src="https://render.githubusercontent.com/render/math?math=H(X)=-\sum^n_{i=1}P(x_i)\log_{base}P(x_i)=\sum^n_{i=1}P(x_i)\log_{base}\frac{1}{P(x_i)}">


## Compression
- TFLite
- google의 TFLite를 사용하면 간단하게 모델 경량화가 가능하다.


## Team
- NAS 이야기
- TFLite 이야기
