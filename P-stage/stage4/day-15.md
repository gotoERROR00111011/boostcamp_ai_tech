# Stage 4 - Day 15

## Opinion

beam search 갈아엎고 재시작  
k개의 선택지에서 선택하는 과정에 batch 단위로 적용 방식 설계

## Reason

batch size 32, beam k 3 한번에 50초 정도...  
for loop 구조로는 속도면에서 도저히 불가능하다고 판단했다.

## Example

numpy의 index select 방식 활용 예정

## Opinion / Offer

제대로 설계부터 하고 코드 구현
