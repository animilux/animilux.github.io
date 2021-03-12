---
layout: post
title: "Autoencoder"
date: 2021-03-11 17:00:00 +0300
description: # Add post description (optional)
img: post6/post6_thumbs.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Autoencoder, Variational Autoencoder, Convolutional Autoencoder, VQ-VAE, Reconstruction, Generative]
---
이번 포스트는 Autoencoder 입니다. 데이터 압축을 목적으로 사용되기 시작해서 생성, 변환 등 다양한 목적에 활용되고 있는 Autoencoder의 종류에 대해 정리해보았습니다.

## Autoencoder 
Autoencoder는 high-dimensional data를 보다 저차원으로 압축하기 위한 모델입니다. 

![autoencoder]({{site.baseurl}}/assets/img/post6/post6_thumbs.jpg)

압축을 위한 구조로 neural network를 사용하고 학습을 위한 target을 설정하기 위해
reconstruction을 수행하는 decoder 구조를 bottleneck layer 뒤에 추가하게 됩니다. 
데이터 압축, 주요 feature 추출을 위한 방법으로 PCA가 많이 알려져 있는데, Autoencoder의 neural network 구조에서 non-linearlity를 학습할 수 있게하는 
activation function(ex. relu, sigmoid)부분을 제외하면 실제로 PCA와 비슷한 결과를 보여준다고 합니다.

## Denoising Autoencoder
Identity function을 학습하는 Autoencoder는 overfitting의 우려가 크기에 제안된 것이 Denoising Autoencoder 입니다. 

![dae]({{site.baseurl}}/assets/img/post6/dae.jpg)

Denoising Autoencoder는 input의 임의의 영역을 noise로 바꾸고, reconstruction은 noise의 영역까지 원본처럼 복원할 수 있도록 학습합니다.
일부 노드를 지우는 것으로 생각하면 dropout과 같은 개념으로 생각할 수 있지만 dropout paper보다 4년이나 먼저 나온 연구라고 하네요.

## Sparse Autoencoder
Sparse Autoencoder는 autoencoder의 hidden layer에 sparsity 조건을 추가한 것으로 생각할 수 있습니다.
sparsity 조건이란 hidden unit의 activation을 제한하는 것인데, 이를 통해 hidden unit의 수가 커져도 좀 더 의미 있는 feature를 학습하는 것이 가능해집니다.
Sparse Autoencoder 중 대표격인 k-Sparse Autoencoder의 결과를 보겠습니다.

![sae]({{site.baseurl}}/assets/img/post6/sae.jpg)

k-Sparse Autoencoder는 hidden layer의 activation 값 중 가장 큰 k개의 값만 사용합니다.  
k 값이 작아질수록 적은 정보로 reconstruction을 수행해야 하기에 hidden layer에서는 점점 high level feature를 학습하게 됩니다.

## Convolutional Autoencoder
Autoencoder는 정형, 비정형(언어, 이미지 등) 등의 모든 데이터에 대해 사용할 수 있지만, 이미지 데이터에 대해 Autoencoder를 사용할 땐 
보통 Convolutional Autoencoder를 기본으로 생각합니다. CAE는 이전까지 input을 flatten해서 사용하던 방식에 CNN을 추가한 것입니다.
이로써 parameter 수를 줄여 좀 더 큰 이미지에도 사용할 수 있고, convolution 단위로 좀 더 의미있는 feature를 학습할 수 있다는 점 등 CNN의 기본적인 장점을 얻게되는 효과가 있습니다. 

## Variational Autoencoder 
![vae]({{site.baseurl}}/assets/img/post6/vae.jpg)

Variational Autoencoder는 Autoencoder 구조에서 latent variable z를 얻기위한 trick과 loss에 KL divergence가 추가된 것인데요. 
이렇게 표면적으로는 Autoencoder에 일부 개념이 추가된 것으로 보이지만 목적 자체가 Autoencoder와는 다르기에 전혀 다른 모델로 구분되곤 합니다.
앞서 언급했던 것처럼 Autoencoder는 데이터 압축, 즉 특정 maniflod를 학습하기 위한 모델인 반면, VAE는 GAN처럼 Generative model로 분류됩니다.

< ------------------------ 작성중 ------------------------>
<!-- latent variable z를 다루기 쉬운 normal distribution으로 가정하고 encoder의 output을 z에 근사시키는 방법으로 모델 학습을 진행합니다.
이 방법으로 인해 VAE는 단순히 input을 외울 수 없게되고 latent variable의 수가 변해도 안정적인 성능을 보여준다고 합니다. -->




## Reference 
<a href="https://lilianweng.github.io/lil-log/2018/08/12/from-autoencoder-to-beta-vae.html">Lil'log : From Autoencoder to Beta-VAE</a>  
<a href="https://blog.naver.com/laonple/220943887634">라온피플 : 머신러닝 학습 방법(part 14) - AutoEncoder(5)</a>  
<a href="https://blog.naver.com/laonple/220949087243">라온피플 : 머신러닝 학습 방법(part 14) - AutoEncoder(6)</a>  
<a href="https://www.jeremyjordan.me/variational-autoencoders/">Jeremy Jordan : Variational autoencoders</a>  

<!-- paper :  
<a href="https://arxiv.org/abs/2006.07733​">Bootstrap Your Own Latent A New Approach to Self-Supervised Learning</a>

etc :   
<a href="https://hoya012.github.io/blog/byol/">HOYA012'S RESEARCH BLOG : Bootstrap Your Own Latent： A New Approach to Self-Supervised Learning 리뷰</a>  
<a href="https://2-chae.github.io/category/2.papers/26">https://2-chae.github.io/category/2.papers/26</a>  
<a href="https://cool24151.tistory.com/85">https://cool24151.tistory.com/85</a> 
<a href="https://www.youtube.com/watch?v=BuyWUSPJicM">딥러닝논문읽기모임 : 조용민 - Bootstrap Your Own Latent(BYOL)</a>  -->
  







