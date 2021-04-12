# Stage 1 - Day 10

## Introduction
### Lecture


## Wrap Up

### Transfer Learning
18 class, 18900 image  
image 수가 적어서 pre-trained 가 좋은 성과를 얻을 수 있을것이라 예상했다.  
결과는 동일 epoch에서 fine-tune이 좋은 결과를 보여주었다.  

| pre-trained | middle | fine-tune |
| --- | --- | --- |
| 50% | 60% | 70% |

### Multi Model
18 class 를 3 model (3 * 3 * 2 class) 로 나누어 실험  
3개의 model 중 한개의 model만 학습률이 정체되었는데, 18 class를 1 model로 사용하는 경우와 비슷한 수치인것을 확인할 수 있었다.  

### Colab Pro

| model | env | epoch | batch size | input image | time(s) |
| --- | --- | --- | --- | --- | --- |
| EfficientNet b7 | Tesla P40 (24451MiB) | 1 (16384 image) | 32 | 3 * 228 * 228 | 671.688 |
| EfficientNet b7 | Tesla P40 (24451MiB) | 1 (16384 image) | 16 | 3 * 228 * 228 | 718.866 |
| EfficientNet b7 | Tesla P100 (16280MiB) | 1 (16384 image) | 16 | 3 * 228 * 228 | 587.277 |
| EfficientNet b7 | Tesla V100 (32480MiB) | 1 (16384 image) | 16 | 3 * 228 * 228 | 320.569 |
| EfficientNet b7 | Tesla V100 (32480MiB) | 1 (16384 image) | 32 | 3 * 228 * 228 | 284.785 |

