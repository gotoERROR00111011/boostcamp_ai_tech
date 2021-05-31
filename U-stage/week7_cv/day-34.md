# Week 7 - Day 34

## Introduction

### Lecture

- Instance/Panoptic segmentation
- Conditional generative model

## Instance Segmentation

### Mask R-CNN

- Mask R-CNN = Faster R-CNN + Mask branch
- RoiAlign

### YOLACT (You Only Look At CoefficienTs)

### YolactEdge

- YOLACT 경량화

## Panoptic Segmentation

### UPSNet

### VPSNet

## Landmark Localization

- keypoint 사용

### coordinate regression

### heatmap classification

- landmark location to gaussian heatmap
- <img src="https://render.githubusercontent.com/render/math?math=G_\sigma(x,y)=\exp\left(-\frac{(x-x_c)^2%2B(y-y_c)^2}{2\sigma^2}\right)">, (xc, yc : center location)

### Hourglass Network

- UNet 구조 반복
- skip-connection add 형태 (UNet은 concat 형태)
- skip-connection도 별도의 network 처리후에 add

### DensePose

- DensePose R-CNN = Faster R-CNN + 3D surface regression branch
- UV map

### RetinaFace

- RetinaFace = FPN + Multi-task branches

## Object Detection as Keypoints

### CornerNet

### CenterNet

- bounding box {top-left, bottom-right, center}
- bounding box {width, height, center}

## Conditional Generative Model

- P(high resolution audio | low resolution audio)
- P(english sentence | chinese sentence)
- P(a full article | an article's title and subtitle)

### Super Resolution GAN

- MAE, MSE 로 구한 결과는 blur 경향
- GAN은 discriminator가 있기 때문에 위의 문제가 해결된다.

## Image Translation

### Pix2Pix

- supervised learning
- image를 다른 style의 image 로 변환
- total loss = GAN loss + L1 loss
- <img src="https://render.githubusercontent.com/render/math?math=G^*=\arg\min_G\max_D\mathcal{L}_{cGAN}(G,D) %2B \lambda \mathcal{L}_{L1}(G)">
- <img src="https://render.githubusercontent.com/render/math?math=\mathcal{L}_{cGAN}(G,D)=\mathbb{E}_{x,y}[\log D(x,y)] %2B \mathbb{E}_{x,z}[\log(1-D(x,G(x,z))]">
- <img src="https://render.githubusercontent.com/render/math?math=\mathcal{L}_{L1}(G)=\mathbb{E}_{x,y,z}[||y-G(x,z)||_1]">

### CycleGAN

- non-pairwise datasets

### Perceptual Loss

## Team

- 강의가 어렵다는 이야기
- 마스터클래스 질문 선정
