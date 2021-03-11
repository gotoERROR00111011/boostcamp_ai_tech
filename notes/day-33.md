# Week 7 - Day 33

## Introduction
### Lecture
- Object detection
- CNN visualization


## Object Detection
- classification + box localization (Pclass, Xmin, Ymin, Xmax, Ymax)

### Two-Stage Detector
- R-CNN
- Fast R-CNN
- Faster R-CNN

### Single-Stage Detector
- YOLO
- SSD (Single Shot MultiBox Detector)

### Focal Loss
- <img src="https://render.githubusercontent.com/render/math?math=CE=-\log(p_t)">
- <img src="https://render.githubusercontent.com/render/math?math=FL=-(1-p_t)^\gamma\log(p_t)">

### RetinaNet
- U-Net 과 유사
- Feature Pyramid Networks (FPN) + class/box prediction branches

### DETR
1. backbone CNN + positional encoding ->
1. transformer encoder
1. object queries(positoinal encoding) ->
1. transformer decoder
1. prediction heads (class, box or no object)


## CNN Visualization
- black box

### Filter Visualization
- low level feature
- 1st layer의 filter를 사용해 convolution을 하여 visualization

### Embedding Feature Analysis 1
- high level feature
- embedding feature을 nearest neighbors 으로 유사한 이미지 탐색

### Embedding Feature Analysis 2
- high level feature
- dimentionality reduction, 고차원을 사람이 이해 가능한 차원으로 변환
- t-SNE

### Activation Investigation 1
- mid, high level featrue
- layer의 activaion 분석
- layer의 특정 channel의 acitvation을 thresholding하고 영상에 적용

### Activation Investigation 2
- mid level featrue
- layer의 activaion 분석
- layer의 특정 channel의 activation이 가장 큰 값을 가지는 위치의 patch를 crop

### Activation Investigation 3
- high level featrue
- class visualization
- <img src="https://render.githubusercontent.com/render/math?math=I^*=\arg\max f(I)-Reg(I)">
- <img src="https://render.githubusercontent.com/render/math?math=I^*=\arg\max f(I)-\lambda||I||^2_2">

1. 분석할 CNN model에 임의의 영상(random, blank)을 input, class prediction
1. input 까지 backpropagation
1. 2.로 update 된 영상을 input으로 다시 1.을 반복


## Model Decision Explanation
### Saliency Test 1
- occlusion map
- 일부 영역을 가리고 예측한 결과의 정확도를 사용
- 모든 영역에서 테스트한 결과를 heatmap 으로 visualization

### Saliency Test 2
- backpropagation 사용
- 특정 class의 이미지를 classification 후에 backpropagation 으로 영향을 끼친 부분을 visualization

1. 분석할 CNN model에 영상을 input, prediction
1. input 까지 backpropagation
1. input layer의 gradient visualization (절대값 or 제곱)
1. (option) 반복

### Backpropagation-Based Saliency

### Class Activation Mapping
- CNN 의 최종 layer에 GAP(global average pooling) -> FC layer 방식 사용, 재학습
- GAP의 weight를 GAP 이전의 feature map과 곱한다.
- (S:score, c:class, k:channel, f(x,y):feature map before GAP)
- <img src="https://render.githubusercontent.com/render/math?math=S_c=\sum_k w^c_k F_k=\sum_k w^c_k \sum_{(x,y)}f_k(x,y)=\sum_{(x,y)}\sum_k w^c_k f_k(x,y)">

### Grad-CAM
- 기존의 model을 GAP->FC 구조로 바꾸지 않고 사용 가능
- (A:activation map, S:score, c:class, k:channel, f(x,y):feature map before GAP)
- <img src="https://render.githubusercontent.com/render/math?math=\alpha^c_k =\frac{1}{Z}\sum_i\sum_j \frac{\partial y^c}{\partial A^k_{ij}}"> : backpropagation gradient를 GAP
- <img src="https://render.githubusercontent.com/render/math?math=L^c_{Grad-CAM}=ReLU(\sum_k \alpha^c_k A^k)">




## Team
- 이번 강의가 어렵다는 이야기

