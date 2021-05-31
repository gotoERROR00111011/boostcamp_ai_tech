# Stage 1 - Day 6

## Introduction

### Lecture

## Opinion

VGG-19 를 backbone으로 여러가지 실험을 하려고 한다.  
hyperparameter는 한번에 1개씩 바꾸며 실험할 예정이다.

## Reason

이론적으로는 어느정도 hyperparameter의 의미를 알지만, 실제 적용에서 영향을 모르는 상황이다.  
이런 상황에서 hyperparameter를 동시에 여러개를 바꾸면 원인 파악이 어려울것이라 예상된다.  
최대 score 보다, 빠른 학습을 여러번 반복하여 hyperparameter에 따른 변화를 실험하는 것이 장기적으로 좋다고 판단했다.

## Example

VGG-19의 classifier를 class 수에 맞게 변경하고 SGD, cross entropy, lr 1e-3 등을 사용하여 정상 동작을 테스트하였다.  
augmentation 이나, 다른 hyperparameter 실험은 테스트 하지 않은 상황이다.

## Opinion / Offer

시간과 장비가 한정되어 있기 때문에 이후 테스트 범위를 제한하는것이 좋아보인다.  
learning rate, optimizer 등의 세부조정 보다는 model, augmentation, transfer learning 위주로 진행하려고 한다.
