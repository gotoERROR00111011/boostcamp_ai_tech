# Stage 4 - Day 13

## Opinion

구현

1. input size 64, 256
1. augmentation

## Reason

모델 자체와 연결된 부분이 아니라서 간단하게 구현 가능하기 때문이 우선적으로 구현한다.

기존의 input size 128*128 의 경우 가로 길이가 긴 dataset에 맞지 않아서 문자가 일부 뭉개진다.  
따라서 64 * 256 으로 변경한다. flatten 해서 사용하기 때문에 pixel 수만 맞춰주면 된다.

augmentation 은 문자-검은색, 종이-흰색 으로 단순하기 때문에 rotate만 적용시킨다.  
rotate로 생기는 빈 공간은 테두리 복제를 사용했다. (미러링의 경우 문자 형태로 복사되는 경우도 있기 때문)

## Example

```python
albumentations.Resize()
albumentations.SafeRotate()
```

## Opinion / Offer

input size 의 경우 성능 향상이 예상되지만, 시간 관계상 다음 구현까지 합쳐서 리더보드에 제출한다.
