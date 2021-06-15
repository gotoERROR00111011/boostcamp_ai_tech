# Stage 4 - Day 10

## Opinion

beam search 구현 실패 원인 분석

오류 이외에도 k=3, batch size 32 에서 한번의 batch 처리가 50초 정도 걸리는 심각한 문제가 발생했다.

## Reason

batch 단위의 데이터 구조에 익숙치 않음, 행렬에 특화된 연산 방법 활용 부족으로 많은 문제가 발생했다.

beam search 구현은 계속 시도할 생각이지만, 현재의 코드는 실패라고 생각하여 갈아엎는것이 좋아보인다.

## Example

1. for loop 방식의 데이터 접근
1. class, array 로 합치면 편할 변수들을 별개로 사용하여 코드 난독화

이로 인해 심각한 속도 저하, 오류가 발생했다.

## Opinion / Offer

일단 다른 모델을 돌려놓고 구조 설계부터 할 예정이다.
