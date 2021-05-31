# Week 8 - Day 39

## Introduction

### Lecture

## Quantization

- fixed point
- floating point

## Knowledge Distillation

- teacher model & student model
- knowledge distillation 으로 학습시킨 student model의 정확도 > 스스로 학습한 student model의 정확도
- loss : distillation loss, student loss
- distillation loss : loss fn(teacher output(soft labels), student output(soft prediction))
- student loss : loss fn(ground truth, student output(hard prediction))
- <img src="https://render.githubusercontent.com/render/math?math=\frac{\exp(\frac{z_j}{T})}{\sum_j\exp(\frac{z_j}{T})}"> : soft prediction
- <img src="https://render.githubusercontent.com/render/math?math=\frac{\exp({z_j})}{\sum_j\exp({z_j})}"> : hard prediction
