# Stage 4 - Day 04

## Opinion

model에 input 하기 전에 histogram equalization 처리

## Reason

초기에 EDA를 하면서 생각했던 text image의 특성을 살린 고려사항  
어두운 영역과 밝은 영역이 비교적 뚜렷한 형태와 비율을 갖추고 있어서 적합하다.  
밝기의 분포가 다른 dataset 에서 효과를 얻을 것으로 예상한다.

## Example

histogram equalization을 적용시킨 결과 육안으로 보기에 text가 선명해지고, dataset 간의 밝기 차이도 줄었다.

다만 하나의 이미지 내에서 그림자가 존재하는 경우, 그림자가 짙어지는 문제가 발생한다.
이미지를 여러 grid로 나누어 적용하는 adaptive histogram equalization으로 이런 문제를 해결한다.

## Opinion / Offer

아직 몇가지 실험이 필요해서 당장에 적용은 하지 않고 있다.  
그래도 어느정도의 성능 향상을 얻을 것이라 기대하고 있다.
