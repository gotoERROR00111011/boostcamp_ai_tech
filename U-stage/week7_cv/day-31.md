# Week 7 - Day 31

## Introduction

### Lecture

- Week7 Overview
- OT
- Image classification 1
- Annotation data efficient learning

## Data Augmentation

- brightness adjustment
- rotate
- flip
- crop
- affine transformation
- CutMix

## Pre-Trained

### Transfer Learning

- (Conv - fixed) (FC, softmax - new task)
- (Conv - low learning rate) (FC - high learning rate)

### Knowledge Distillation

- teacher model -> student model 방식의 학습
- label을 사용하지 않는 unsupervised learning
- input x에 대한 teacher model(pre-trained)과 student model(not trained)의 output을 KL div. loss로 student에 대해서만 backpropagation 하여 학습한다.
- hard label(one-hot vector), soft label(실수값, softmax output)
- <img src="https://render.githubusercontent.com/render/math?math=\frac{\exp(z_i)}{\sum_j\exp(z_j)}"> softmax는 값이 정답에 치우치기 때문에 <img src="https://render.githubusercontent.com/render/math?math=\frac{\exp(z_i/T)}{\sum_j\exp(z_j/T)}"> T(temperature) 로 나누어 사용한다.

#### Distillation Loss

- 다음 두 vector를 loss에 사용
- teacher model -> softmax -> soft label
- student model -> softmax -> soft predection

#### Student Loss

- 다음 두 vector를 loss에 사용
- ground truth (one-hot)
- student model -> softmax -> soft predection

## Unlabeled Dataset

### Semi-Supervised Learning

- 적은 labeled data, 많은 unlabeled data 를 사용하는 학습 방법

1. labeled data 로 training
1. 학습된 model으로 unlabeled data의 pseudo-label 생성
1. labeled data, pseudo-label 으로 새로운 model 학습 혹은 재학습

## Self-Training

semi-supervised learning, data-augmentation 등을 결합한 학습 방법

## Team

- 과제 이야기
- 출결 시스템 이야기
