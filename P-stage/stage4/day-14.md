# Stage 4 - Day 14

## Opinion

SATRN 논문의 locality-aware feedforward 을 적용한다.

## Reason

fc 방식과 다르게, image의 2D 특성을 활용할 수 있다.

학습에는 input size 변경과, augmentation을 함께 적용한다.

|         | score  | sent_acc | wer    |
| ------- | ------ | -------- | ------ |
| default | 0.7077 | 0.6838   | 0.0776 |
| new     | 0.7474 | 0.7268   | 0.0672 |

## Example

decoder의 layer를 6개로 추가하는 것보다 높은 성능을 얻었다.  
decoder를 더 깊게 만드는것과 함께하면 더 높은 성능을 얻을 수 있겠지만, 제한이 있는것이 아쉬운 점이다.

albumentations-numpy 버전이 inference-numpy와 달라서 꼬였다.  
결국 albumentations 학습 후 requirements 재설치로 해결

## Opinion / Offer

자원 문제로 실험에 제한이 있어서 각 요소들의 영향 정도를 파악하지는 못했다.  
여유가 생기면 이후 실험해 볼 필요도 있어보인다.
