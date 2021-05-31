# Week 3 - Day 15 - Generative Model

## Introduction

### Lecture

- Generative Models 1
- Generative Models 2

## Generative Model

> what i cannot create i do not understand  
> _richard feynman_

generative model은 이미지, 문장 생성만을 포함하는 더 큰 개념이다.

### Generation

generative model은 이름처럼 sampling 기능이 있다.

### Density Estimation

generative model은 discriminate model을 포함한다.  
sampling 할 수 있다는 것은 distribution를 알고 있다는 것이기 때문에 분류가 가능하고, anomaly detection에 활용할 수 있다.  
분류 가능한 model을 explicit model, generation 기능만 있는 model을 implicit model 이라 부른다.

## Conditional Independence

<img src="https://render.githubusercontent.com/render/math?math=P(x)">의 modeling이 중요하다.

### Discrete Distributions

discrete distributions(bernoulli, categorical)에서 m개의 변수의 distribution를 표현하기 위해서는 m-1개의 parameter가 필요하다.

n개의 pixel을 가진 binary image는 <img src="https://render.githubusercontent.com/render/math?math=2^n">개의 경우의 수가 존재한다.  
여기서 각 pixel은 dependent하기 때문에 <img src="https://render.githubusercontent.com/render/math?math=2^n-1"> 이라는 많은 수의 parameter가 필요하다.  
만약 각 pixel이 independent하다고 가정하면 <img src="https://render.githubusercontent.com/render/math?math=n">개의 적은 수의 parameter만 있으면 되지만, 각 pixel이 독립적이기 때문에 주변 pixel과 무관하게 생성될 것이다.

fully dependent와 independent 사이의 적절한 model을 찾기 위해 다음 규칙들을 조합하여 활용한다.

- chain rule : <img src="https://render.githubusercontent.com/render/math?math=P(x_1,\cdots,x_n)=p(x_1)p(x_2|x_1)p(x_3|x_1,x_2)\cdots,p(x_n|x_1,\cdots,x_{n-1})">
- bayes' rule : <img src="https://render.githubusercontent.com/render/math?math=P(x|y)=\frac{P(x,y)}{P(y)}=\frac{P(y|x)P(x)}{P(y)}">
- conditional independence : <img src="https://render.githubusercontent.com/render/math?math=\text{if } x\perp y\ |\ z, \text{then }P(x|y,z)=P(x|z)">

### Markov Assumption

i+1번째는 i번째에만 dependent 하다고 가정하는 방식  
<img src="https://render.githubusercontent.com/render/math?math=P(x_1,\cdots,x_n)=P(x_1)P(x_2|x_1)\cdots P(x_n|x_{n-1})">  
binary image에서의 parameter 수는 <img src="https://render.githubusercontent.com/render/math?math=2^n-1">으로 independent 보다는 많고, fully dependenty 보다는 적다.

### Auto-Regressive Model

AR(n) model  
이전 n개 까지 dependent 하다고 가정하는 방식

### NADE : Neural Autoregressive Density Estimator

i번째가 1~i-1번째와 dependent 하다고 가정하는 방식  
<img src="https://render.githubusercontent.com/render/math?math=PP(x_1,\cdots,x_n)=P(x_1)P(x_2|x_1)P(x_3|x_{1:2})\cdots P(x_n|x_{1:n-1})">

### Pixel-RNN

RNN을 사용하는 방식

## Latent Variable Models

### Variational Auto-Encoder

#### variational inference

posterior distribution에 근사하는 variational distribution을 찾는 과정

- posterior distribution : <img src="https://render.githubusercontent.com/render/math?math=p_{\theta}(z|x)"> observation이 주어졌을때 관심있어 하는 random variable의 확률 분포
- variational distribution : <img src="https://render.githubusercontent.com/render/math?math=q_{\phi}(z|x)"> posterior에 근사하는 확률 분포

posterior distribution을 모르는 상태에서 variational distribution을 찾아야 한다.  
posterior distribution과 variational distribution 사이의 KL divergence를 줄이는 것이 목적이지만 불가능하다.  
그래서 ELBO를 maximize해서 반대급부로 원하는 object를 얻는다.

<img src="https://render.githubusercontent.com/render/math?math=\ln p_\theta(D)"><br>
<img src="https://render.githubusercontent.com/render/math?math==\mathbb{E}_{q\phi(z|x)}\left[\ln p_{\theta}(x)\right]"><br>
<img src="https://render.githubusercontent.com/render/math?math==\mathbb{E}_{q\phi(z|x)}\left[\ln \frac{p_{\theta}(x,z)}{p_{\theta}(x|z)}\right]"><br>
<img src="https://render.githubusercontent.com/render/math?math==\mathbb{E}_{q\phi(z|x)}\left[\ln \frac{p_{\theta}(x,z)q_{\phi}(z|x)}{q_{\phi}(z|x)p_{\theta}(x|z)}\right]"><br>
<img src="https://render.githubusercontent.com/render/math?math==\mathbb{E}_{q\phi(z|x)}\left[\ln \frac{p_\theta(x,z)}{q_\phi(z|x)} \right] %2B \mathbb{E}_{q\phi(z|x)}\left[\ln \frac{q_\phi(z|x)}{p_\theta(z|x)} \right]"><br>
<img src="https://render.githubusercontent.com/render/math?math==\underbrace{\mathbb{E}_{q\phi(z|x)}\left[\ln \frac{p_\theta(x,z)}{q_\phi(z|x)} \right]}_{\text{ELBO}\uparrow} %2B \underbrace{D_{KL}(q_\phi(z|x)||p_\theta(z|x))}_{\text{Objective}\downarrow}"><br>

#### ELBO (Evidence Lower Bound)

ELBO는 reconstruction term과 prior fitting term 으로 나눌 수 있다.

- reconstruction term : auto-encoder의 loss를 minimize 한다.
- prior fitting term : latent distribution을 prior distribution과 비슷하게 만든다.

<img src="https://render.githubusercontent.com/render/math?math=\underbrace{\mathbb{E}q_{\phi}(z|x)\left[\ln \frac{p_\theta(x,z)}{q_\phi(z|x)}\right]}_{\text{ELBO}\uparrow}"><br>
<img src="https://render.githubusercontent.com/render/math?math==\int\ln\frac{p_\theta(x|z)p(z)}{q_\phi(z|x)}q_\phi(z|x)dz"><br>
<img src="https://render.githubusercontent.com/render/math?math==\underbrace{\mathbb{E}q_{\phi}(z|x)\left[\ln p_\theta(x|z)\right]}_\text{Reconstruction Term}-\underbrace{D_{KL}(q_\phi(z|x)||p(z))}_\text{Prior Fitting Term}">

### Adversarial Auto-Encoder

Variational Auto-Encoder의 KL divergence에 있는 prior fitting term을 GAN으로 구한 것

## Generative Adversarial Network

<img src="https://render.githubusercontent.com/render/math?math=\underbrace{\text{min}}_{G}\,\underbrace{\text{max}}_{D}\,V(D,G)=\mathbb{E}_{x\sim p_{data}(x)}[\log D(x)] %2B \mathbb{E}_{z\sim p_z(z)}[\log(1-D(G(z)))]">

### Discriminator

<img src="https://render.githubusercontent.com/render/math?math=\underbrace{\text{max}}_{D}\,V(G,D)=\mathbb{E}_{x\sim p_{data}}[\log D(x)] %2B \mathbb{E}_{x\sim p_{G}}[\log(1-D(x))]">

optimal discriminator : <img src="https://render.githubusercontent.com/render/math?math=D^*_G(x)=\frac{p_{data}(x)}{p_{data}(x) %2B p_G(x)}">

### Generator

<img src="https://render.githubusercontent.com/render/math?math=\underbrace{\text{min}}_{G}\,V(G,D)=\mathbb{E}_{x\sim p_{data}}[\log D(x)]+\mathbb{E}_{x\sim p_{G}}[\log(1-D(x))]">

optimal discriminator 대입 : <img src="https://render.githubusercontent.com/render/math?math=V(G,D^*_G(x))"><br>
<img src="https://render.githubusercontent.com/render/math?math==\mathbb{E}_{x\sim p_{data}}\left[\log\frac{p_{data}(x)}{p_{data}(x) %2B p_G(x)}\right] %2B \mathbb{E}_{x\sim p_{G}}\left[\log\frac{p_{G}(x)}{p_{data}(x) %2B p_G(x)}\right]"><br>
<img src="https://render.githubusercontent.com/render/math?math==\mathbb{E}_{x\sim p_{data}}\left[\log\frac{p_{data}(x)}{\frac{p_{data}(x) %2B p_G(x)}{2}}\right] %2B \mathbb{E}_{x\sim p_{G}}\left[\log\frac{p_{G}(x)}{\frac{p_{data}(x) %2B p_G(x)}{2}}\right]-\log4"><br>
<img src="https://render.githubusercontent.com/render/math?math==\underbrace{D_{KL}\left[p_{data}, \frac{p_{data} %2B p_G}{2}\right] %2B D_{KL}\left[p_G, \frac{p_{data} %2B p_G}{2}\right]}_\text{2xJenson-Shannon Divergence (JSD)}-\log4"><br>
<img src="https://render.githubusercontent.com/render/math?math==2D_{JSD}[p_{data},p_G]-\log4"><br>

## Team

- 연휴 관련 잡담
