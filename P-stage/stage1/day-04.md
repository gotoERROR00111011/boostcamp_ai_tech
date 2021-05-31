# Stage 1 - Day 4

## Introduction

### Lecture

- Training & Inference
  - Loss, Optimizer, Metric
  - Process

## Opinion

competition를 1회 제출을 우선하기로 정했다.

## Reason

많은 사람들이 제출한 상황에서 한번도 제출하지 않은것이 불안하기 때문이다.  
따라서 score 보다는 pipeline을 한번 통과한다는 의미로 진행한다.

## Example

cross entropy, SGD 등으로 적당한 hyperparameter를 선택하였다.  
augmentation은 적용하지 않은채 type 변환만 하였다.  
epoch도 몇번 안하고 제출해서 44%, 대충한것에 비해서는 만족스러운 결과였다.

## Opinion / Offer

이제 pipeline 한번은 되었으니 jupyter 환경의 난잡한 상황을 .py 파일로 정리하는 것이 좋아보인다.
