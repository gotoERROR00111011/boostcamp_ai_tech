# Stage 1 - Day 8

## Introduction
### Lecture


## Opinion
FaceNet을 사용해 transfer learning에 대한 몇가지 실험을 진행  
pre-traing 와 fine-tuning 차이를 중점적으로 분석  

## Reason
현실적으로 실제 학습에서 pre-trained model을 사용하는 경우가 많을것이다.  
개인적으로도 1%의 정확도 상승 보다는 application 영역에 관심이 많기 때문에 transfer learning에 주목하고 있다.    

## Example
transfer learning의 freeze 영향에 대한 실험  
18 class, 18900개의 학습 데이터(image)  
FaceNet이 (마스크 정보는 없지만) 사람 얼굴에 특화된 학습 모델이라서 pre-train 의 성능을 기대했으나, fine-tuning에는 미치지 못했다.  
- pre-train에 classifier 만 추가한 경우
- 전체 layer 일부만 학습
- 전체 layer 학습
  
| freeze | epoch | accuracy | train time |
| --- | --- | --- | --- |
| pre-train | 30 | 50% | 0:38 |
| middle    | 30 | 60% |      |
| fine-tune | 30 | 70% | 1:38 |

## Opinion / Offer
pre-trained model 으로 fine-tuning 하는것이 (데이터가 많지 않아도) 좋은 선택지라는 것을 확인했다.  
2만개의 사진이면 힘들것이라 생각했으나, 어느정도 유의미한 결과는 확인 가능한 듯하다.  
