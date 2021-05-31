# Stage 1 - Day 9

## Introduction

### Lecture

## Opinion

18 class 분류를 3 class _ 3 class _ 2 class 3개의 model 학습 후 18 class로 변환하는 실험 진행  
Colab Pro와 현재 환경 성능 비교

## Reason

3가지 분류를 합쳐서 18 class로 통합한 model 이라서 각각의 분류는 class 수가 적기 때문에 더 높은 정확도를 얻을 수 있다는 가정

지금은 server를 지원받고 있지만, 그 이후에 Colab 으로 어느정도 커버할 수 있는지 테스트

## Example

A model, B model, C model 3 분류로 나누어 학습한 결과, A < B <<< C 정도로 학습 score 확인  
전체 18 class 의 score와 C model의 score가 큰 차이가 없는것으로 보아 C model의 개선이 전체 성능 향상으로 이어짐을 알 수 있다.

colab pro (Tesla P100) 성능 비교  
P100의 memory가 작아서 batch size가 16인데, 32인 P40 보다 더 빠르게 학습된 것을 확인할 수 있다.

| model           | env                   | epoch           | batch size | input image   | time(s) |
| --------------- | --------------------- | --------------- | ---------- | ------------- | ------- |
| EfficientNet b7 | Tesla P40 (24451MiB)  | 1 (16384 image) | 32         | 3 _ 228 _ 228 | 671.688 |
| EfficientNet b7 | Tesla P40 (24451MiB)  | 1 (16384 image) | 16         | 3 _ 228 _ 228 | 718.866 |
| EfficientNet b7 | Tesla P100 (16280MiB) | 1 (16384 image) | 16         | 3 _ 228 _ 228 | 587.277 |

## Opinion / Offer

시간, 자원의 한계로 score를 개선하지는 못했지만, 문제를 분리하면 관심 영역을 특정할 수 있다.

개발 환경이 제한적이긴 하지만 colab pro도 잘 활용하면 충분히 사용 가능하다. 자원이 부족하다면 추천
