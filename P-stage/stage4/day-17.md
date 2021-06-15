# Stage 4 - Day 17

## Opinion

최종 리더보드

beam search 완성

## Reason

beam search 의 결과 return 부분의 select 오류 수정

리더보드의 숨겨진 부분이 특수했는지 20% 정도 하락했다.  
다른 팀들의 점수도 비슷한 정도로 떨어지는 결과를 보였다.

## Example

|                                    | score  | sent_acc | wer    |
| ---------------------------------- | ------ | -------- | ------ |
| histogram                          | 0.6701 | 0.6437   | 0.0923 |
| invert                             | 0.7077 | 0.6840   | 0.0792 |
| default                            | 0.7077 | 0.6838   | 0.0776 |
| 6 layer                            | 0.7350 | 0.7135   | 0.0711 |
| locality, input size, augmentation | 0.7474 | 0.7268   | 0.0672 |
| final                              | 0.5337 | 0.5027   | 0.1872 |

beam search의 속도는 k초 전후로, 기존 beam search 미적용의 1초 이하의 \*k와 차이는 있지만, 만족할 만큼의 속도는 달성했다.  
하지만 beam search의 정확도는 그다지 긍정적이지는 못했다.  
자연어와 다르게 각 step 마다 단 하나의 답만이 존재하기 때문으로 보인다.  
각 step 에서 최고의 정확도를 선택하는것, 즉 beam search를 사용하지 않는것이 적절하다고 추측한다.

## Opinion / Offer

이번 beam search 구현은 경험 측면에서 해본것이지만, 이후에는 이번 경우와 같이 무작정 적용해보는 것은 피하고, 일단 가설부터 세울 필요성이 보인다.
