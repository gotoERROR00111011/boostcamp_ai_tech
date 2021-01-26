# U-Stage Week1(Python) - Day 07

## Introduction

## 미분 (Differentiation)
변수의 움직임에 따른 함수값의 변화를 측정하기 위한 도구  

<img src="https://render.githubusercontent.com/render/math?math=f^\prime(x)=\lim_{h\rightarrow x}\frac{f(x+h)-f(x)}{h}">  

### Gradient
미분은 함수 <img src="https://render.githubusercontent.com/render/math?math=f">의 주어진 점 <img src="https://render.githubusercontent.com/render/math?math=(x,f(x))">에서의 접선의 기울기를 구한다.  

미분값을 더하면 경사상승법(gradient ascent) (극대값의 위치를 찾을때 사용)  
미분값을 빼면 경사하강법(gradient descent) (극소값의 위치를 찾을때 사용)
  
경사상승법, 경사하강법은 극값 <img src="https://render.githubusercontent.com/render/math?math=f^\prime(x)=0">에 도달하면 멈춘다.  


### 편미분 (Partial Differentiation)
벡터가 입력인 다변수 함수의 경우 편미분을 사용한다.  

<img src="https://render.githubusercontent.com/render/math?math=f(x, y)=x^2 %2B 2xy %2B y^2"><br>
<img src="https://render.githubusercontent.com/render/math?math=\partial_{x_i}f(x)=2x %2B 2y">

<img src="https://render.githubusercontent.com/render/math?math=\partial_{x_i} f(x)=\lim_{h\rightarrow x}\frac{f(x+he_i)-f(x)}{h}">
(<img src="https://render.githubusercontent.com/render/math?math=e_i">는 i번쨰 값만 1이고 나머지는 0인 단위벡터)  

### Gradient Vector
각 변수별로 편미분을 계산한 그레디언트 벡터를 이용하여 경사하강법에 사용한다.  
<img src="https://render.githubusercontent.com/render/math?math=\nabla f=(\partial x_1f, \partial x_2f, \dots , \partial x_df)">

### 선형회귀
선형회귀의 목적식은 <img src="https://render.githubusercontent.com/render/math?math=\beta{\lVert}y-X\beta{\rVert}_2">이고 이를 최소화하는 <img src="https://render.githubusercontent.com/render/math?math=\beta">를 찾아야 하므로 다음과 같은 그레디언트 벡터를 구해야 한다.  

<img src="https://render.githubusercontent.com/render/math?math=\nabla_\beta{\lVert}y-X\beta{\rVert}_2=(\partial_{\beta_1}{\lVert}y-X\beta{\rVert}_2, \dots,\partial_{\beta_d}{\lVert}y-X\beta{\rVert}_2)=\left(-\frac{X^T_1(y-X\beta)}{n{\lVert}y-X\beta{\rVert}_2}, -\frac{X^T_d(y-X\beta)}{n{\lVert}y-X\beta{\rVert}_2}, \dots , \right)">
<br>
<img src="https://render.githubusercontent.com/render/math?math=\partial_{\beta_k}{\lVert}y-X\beta{\rVert}_2=\partial_{\beta_k}\left\{\frac{1}{n} \sum^n_{i=1}\left(y_i-\sum^d_{j=1}X_{ij}\beta_{j} \right)^2\right\}^{\frac{1}{2}}=-\frac{X^T_k(y-X\beta)}{n{\lVert}y-X\beta{\rVert}_2}">

### 확률적 경사하강법 (Stochastic Gradient Descent)
데이터를 일부를 활용하여 업데이트 하는 방법  
미니배치 방식이기 때문에 목적식의 모양이 바뀌게 된다.  
비선형회귀 문제의 경우 목적식이 볼록하지 않을 수 있으므로 경사하강법으로는 수렴이 항상 보장되지는 않지만 확률적 경사하강법은 볼록하지 않은(non-convex) 목적식도 최적화할 수 있다.  


## Team
- 강의 중 수식 논의


