# Week 7 - Day 35

## Introduction

### Lecture

- Multi-modal: Captioning and speaking
- 3D understanding

## Multi-Modal Learning

- problem
  - 데이터 형태 차이
  - feature 언밸런스
  - model이 특정 데이터에 bias
- using
  - matching
  - translating
  - referencing

### Visual Data & Text Data

- text data : embedding
- matching : joint embedding (image와 text의 embedding을 유사하게 만든다.)
- translating : CNN feature map output -> RNN input
  - image captioning
  - text-to-image
- referencing :
  - visual question answering (intput(image, text-question))

### Visaul Data & Audio

- audio data (STFT) : waveform -> power spectrum -> spectrogram
  - waveform : amplitude, time
  - power spectrum : magnitude, frequency
  - spectrogram : frequency, timeframe
- matching : joint embedding (SoundNet)
- translating
  - Speech2Face : joint embedding(face, voice) -> face decoder
- referencing
  - sound source localization

## 3D Understanding

### 3D Data

- 3D data의 표현 방식은 다양하다.
  - multi-view image
  - volumetric
  - part assembly
  - point cloud
  - mash (graph)
  - implicit shape
- 3D datasets
  - ShapeNet
  - PartNet
  - SceneNet
  - ScanNet
  - KITTI
  - semantic KITTI
  - waymo open dataset

### 3D Tasks

- 3D recognition
- 3D detection
- 3D semantic segmentation
- Mesh R-CNN

## Team

- 과제 이야기
- 마스터클래스 이야기
