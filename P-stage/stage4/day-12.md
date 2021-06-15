# Stage 4 - Day 12

## Opinion

decoder 6 layer 결과 확인  
예상대로 더 깊게 만들면 더 높은 성능이 나왔다.  
하지만 더이상의 hyperparameter tuning, 단순 layer 추가 등은 하지 않을 예정이다.

## Reason

확실히 점수는 높아지지만 시간이 너무 많이 소모된다.  
팀원들이 참여하지 못해서 사실상 혼자 진행하는데, 학습도 오래걸려서 점수 경쟁은 힘들어 보인다.  
따라서, 기능 구현에 집중할 예정이다.

|         | score  | sent_acc | wer    |
| ------- | ------ | -------- | ------ |
| default | 0.7077 | 0.6838   | 0.0776 |
| 6 layer | 0.7350 | 0.7135   | 0.0711 |

## Example

1. input size
1. augmentation
1. baseline code 에서 SATRN 논문과 다르게 구현된 부분 수정
1. beam search 구현

## Opinion / Offer

완성하지 못할 가능성도 있으니 구현이 간단해 보이는것 부터 하는것이 좋을 듯 하다.
