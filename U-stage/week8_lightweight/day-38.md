# Week 8 - Day 38

## Introduction

### Lecture

## Deep Learning Compiler

구현된 model을 target platforms (HW)에 맞게 compile 해야한다.

- XLA (google)
- TVM (amazon)
- GLOW (facebook)
- ONNC (ONNC)
- etc...

## Pruning

- model에서 중요한 parameter(weight)만 남기고 나머지는 제거하는 방법
- 중요성 낮은 parameter : 영향이 적은 weight, 0에 가까운 weight
- dropout과 유사하다.
