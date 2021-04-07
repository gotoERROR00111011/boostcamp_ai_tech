# Stage 1 - Day 7

## Introduction
### Lecture


## Opinion
model 단계에서 실험을 진행하려고 한다.  
간단하게 VGG, ResNet을 사용  

## Reason
테스트하고 있는 요소들이 특정 model에서만 효과를 보일 가능성도 있기 때문에 진행한다.  

## Example
center crop, flip 등의 간단한 처리와, epoch 수를 크게 설정하는 테스트를 진행하였다.  
결과적으로 학습 속도와 최종 score의 차이는 존재하지만, 사람의 시점에서도 쉽게 예상 가능한 변화에서는 비슷한 수준의 score 변화만 확인되었다.  
VGG <-> ResNet 테스트 과정에서 classifier layer의 이름을 확인하지 않고 학습하여 제출 실패등으로 많은 시간을 소모하였다.  
18개를 넘는 class로 분류하고 있었던 것 (학습으로 인해 대부분 18 class 범주 내에서 예측했기 때문에 문제 파악이 늦어졌다.)  

## Opinion / Offer
테스트 과정을 반복하면서 일부 요소만 변경하는 과정에서 단순 실수로 많은 시간을 소모했다.  
일단 최상의 결과보다는 실수를 줄이는 방향에도 주의를 기울여야 한다고 생각한다.  

