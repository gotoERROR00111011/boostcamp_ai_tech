# Week 2 - Day 08 - Pandas I / 딥러닝 학습방법 이해하기

## Introduction
### Lecture
- pandas I
- 딥러닝 학습방법 이해하기


## Neural Network

### Softmax
softmax 함수는 모델의 출력을 확률로 해석할 수 있게 변환해주는 연산  
학습시에는 softmax를 사용하지만, 추론시에는 최댓값만 선택하면 되기에 사용하지 않는다.  
<br>
<img src="https://render.githubusercontent.com/render/math?math=\text{softmax(o)}=\left(\frac{\exp(o_1)}{\sum^p_{k=1}\exp(o_k)},\dots,\frac{\exp(o_p)}{\sum^p_{k=1}\exp(o_k)}\right)">

```python
def softmax(vec):
    denumerator = np.exp(vec - np.max(vec, axis=-1, keepdims=True))
    numerator = np.sum(denumerator, axis=-1, keepdims=True)
    val = denumerator / numerator
    return val
```

### Activation Function
활성함수는 비선형함수로서 딥러닝에서 매우 중요한 개념이다.  
활성함수를 사용하지 않으면 딥러닝은 선형모형과 차이가 없다.  

#### Sigmoid
<img src="https://render.githubusercontent.com/render/math?math=\sigma(x)=\frac{1}{1+e^{-x}}">

#### tanh
<img src="https://render.githubusercontent.com/render/math?math=\tanh(x)=\frac{e^{x}-e^{-x}}{e^{x}+e^{-x}}">

#### ReLU
<img src="https://render.githubusercontent.com/render/math?math=\text{ReLU}(x)=\max(0,x)">

### Backpropagation
딥러닝은 역전파 알고리즘을 이용해 각 layer의 parameter 를 학습한다.  


## Pandas
```python
from pandas import Series, DataFrame
import pandas as pd

path = "URL or PATH"
df = pd.read_csv(path, sep=',', header=None)

df.head()
```
구조화된 데이터의 처리를 지원하는 python 라이브러리  
panel data -> pandas  
numpy와 통합하여 강력한 기능 지원  

### Series
DataFrame 중 하나의 column에 해당하는 데이터의 모음 object  

### DataFrame
Data Table 전체를 포함하는 object  
Series 를 모아서 만든 Data Table (2차원)  

### Function
기본적으로 data frame 원본의 데이터는 변경하지 않도록 한다!  
numpy가 제공하는 indexing, slicing 등 편리한 기능들을 그대로 제공한다.  
데이터 표현, 추출, 정제, 분석, 연산 등 많은 기능을 제공한다.  
일반적으로 수학적으로 필요한 기능은 찾아보면 나올것이다.  

## Team
- 다음날 발표 pt 정리

