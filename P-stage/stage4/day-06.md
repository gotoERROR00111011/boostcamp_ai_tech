# Stage 4 - Day 06

## Opinion

1. 배경-흰색-255, 문자-검은색-0
1. 배경-검은색-0, 문자-흰색-255

2의 경우가 문자를 인식하는데 더 효과적이라 생각하여 색반전 후에 학습을 진행해본다.

## Reason

activate function은 낮은 값 보다는 높은 값이 잘 전달되기 때문에 영향이 있을지도 모른다는 추측을 했다.

## Example

결과

|         | score  | sent_acc | wer    |
| ------- | ------ | -------- | ------ |
| default | 0.7077 | 0.6838   | 0.0776 |
| invert  | 0.7077 | 0.6840   | 0.0792 |

## Opinion / Offer

안타깝게도 결과에 영향은 없었다.
아마도, 충분히 복잡하고 깊은 구조인 network 에서는 배경과 물체를 구분에 아무런 문제가 없는 듯 하다.
