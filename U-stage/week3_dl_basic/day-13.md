# Week 3 - Day 13 - Convolutional Neural Networks

## Introduction

### Lecture

- CNN - Convolution은 무엇인가?
- Modern CNN - 1x1 convolution의 중요성
- Computer Vision Applications
- CNN - 강아지 종류 분류하기
- CNN - 나만의 데이터셋 만들기

## CNN

### ILSVRC (ImageNet Large-Scale Visual Recognition Challenge)

이 대회에서 나온 network, 논문들이 사용한 key idea들이 deep learning 발전에 큰 영향을 주었다.

점차 performance는 높이고, parameter size는 줄이는 경향으로 발전하고 있다.  
(2015년 부터는 사람의 정확도보다 높아졌다.)

| Year  | Network   | Error Rate |
| :---: | --------- | ---------- |
| 2010  |           | 28.2%      |
| 2011  |           | 25.8%      |
| 2012  | AlexNet   | 16.4%      |
| 2013  |           | 11.2%      |
| 2014  | VGG       | 6.7%       |
| 2015  | GoogLeNet | 3.5%       |
| Human | ResNet    | About 5.1% |

### AlexNet

ReLU, GPU, Data augmentation, Dropout 등 지금까지도 사용하는 많은 idea를 발명?하였다.

### VGGNet

3X3 filter를 사용하는 것이 핵심  
filter의 크기가 커질때 얻는 이점은 고려하는 input의 범위가 넓어지는 것이다.  
3X3 filter는 1-pixel, 5X5 filter는 2-pixel 거리까지 고려한다.  
3X3 filter를 여러번 사용하면 넓은 범위를 고려하면서도 parameter 수가 적어지는 장점이 있다.

### GoogLeNet

#### Inception Blocks

input에 대하여 다음 4가지 Layer를 수행 후, concatenation을 하는 block

- 1X1 Conv
- 1X1 Conv -> 3X3 Conv, pad 1
- 1X1 Conv -> 5X5 Conv, pad 2
- 3X3 MaxPool, pad 1 -> 1X1 Conv

#### 1X1 Conv

1X1 filter로 channel의 수를 줄여서 전체 parameters의 수를 줄일 수 있다.  
이로인해 AlexNet, VGGNet 에 비해 layer가 깊지만, parameters 수는 더 적게 하는 효과를 낸다.

- AlexNet(8-layers, 60M-param)
- VGGNet(19-layers, 110M-param)
- GoogLeNet(22-layers, 4M)

### ResNet

#### Residual Block

skip-connection  
convolution 하기 전 input x를 나중에 더해주는 방식

#### Bottleneck Architecture

1X1 Conv를 활용하여 전체 parameters와 연산량을 줄이는 구조

1. 1X1, 64
1. 3X3, 64
1. 1X1, 256

### DenseNet

ResNet과 비슷하지만, 값을 더하는것이 아닌, 연결하는 concatenation 방식이다.  
이 방식으로는 channel 이 계속 커지는데, 1X1 Conv로 줄여준다.  
(concatenation을 하는 Dense Block -> 1X1 Conv를 하는 Transition Block) 를 반복하는 구조다.

## Semantic Segmentation

pixel 단위의 이미지 인식

### Convolutionalization

기존 CNN의 Fully Connected Layer 대신, label을 channel로 가지는 N X M X channel 형태의 convolution output으로 사용하는 방식

### Deconvolution (conv transpose)

convolution의 반대로 크기를 키우는 연산

## Detection

### R-CNN

selective search로 찾은 모든 영역에 CNN 적용

### SPPNet

1. image에서 bounding box를 찾는다.
1. 이미지 전체에 한번만 CNN 적용
1. CNN을 거친 feature map에서 bounding box 영역을 추출해 사용한다.

### Fast R-CNN

SPPNet 처럼 feature map의 bounding box 영역을 ROI pooling을 사용하고, class와 bounding box 영역, 두개를 예측하여 출력한다.

### Faster R-CNN

Region Proposal Network + Fast R-CNN  
ROI(Region of Interest) 영역도 CNN으로 찾는 방식

output size : 9\*(4+2)

- 9개 : 사전 정의된 Anchor Box size(128, 256, 512), 비율(1:1, 1:2, 2:1)
- 4개 :bounding box x, y, w, h
- 2개 : classification, 유효성

### YOLO

input image를 S X S cell로 나누고 각 cell 영역마다 p, x, y, w, h, class 예측
