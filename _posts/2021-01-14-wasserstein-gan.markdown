---
layout: post
title: "논문 리뷰 : Wasserstein GAN"
date: 2021-01-13 17:00:00 +0300
description: # Add post description (optional)
img: w-gan.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [GAN, Loss]
---
GAN의 학습은 Generator와 Discriminator를 반복하여 학습해야 되기에 각각의 학습 횟수에 따라 mode collapse가 발생하기 쉽다는 불안정성을 가지고 있습니다. 
이 논문은 cost function을 변경하는 것으로 이러한 GAN 학습의 불안정성을 개선하였다는 점에서 GAN 발전에 기여도가 높다고 볼 수 있습니다.

## Introdunction
확률분포를 학습한다는 것은 확률밀도를 정의하고 real data에 대해 확률 값을 최대화하는 문제를 푸는 것으로 접근할 수 있고, 확률 값을 최대화 하는 문제는 식으로 나타내면 다음과 같습니다.

<img src="https://latex.codecogs.com/svg.latex?\; \underset{\theta\in \mathbb{R}^{d}}{max}\frac{1}{m}\sum_{i=1}^{m}\log P_{\theta}(x^{(i)})" />

이 식은 실제 데이터의 분포 <img src="https://latex.codecogs.com/svg.latex?\; P_{r}" />이 확률밀도함수 <img src="https://latex.codecogs.com/svg.latex?\; P_{\theta}" />를 따른 다고 가정하면 Kullback-Leibler divergence 를 최소화 하는 것으로 풀 수 있습니다.

<img src="https://latex.codecogs.com/svg.latex?\; \min KL(\mathbb{P}_{r}||\mathbb{P}_{\theta})" />

GAN의 학습을 위해 항상 KL divergence를 사용해야하는 것은 아니지만 일반적인 GAN의 loss함수는 아래와 같은 형태입니다.

![GAN_loss]({{site.baseurl}}/assets/img/GAN_loss.jpg)

이 식은 최적의 discriminator에 대한 generator의 식으로 바꾸면 Jensen-Shannon distance를 최소화하는 식이 됩니다. (식 유도는 GAN paper 참조)

![GAN_loss2]({{site.baseurl}}/assets/img/GAN_loss_2.jpg)

위와 같이 GAN loss는 JS distance를 포함하고 있기에 mode collapse나 adversarial training 과정에서 오는 학습의 불안정성 등 여러가지 단점을 가지고 있습니다.
이 논문에선 실제 데이터와 생성 데이터의 분포 사이의 새로운 distance metric, EM distance를 제안함으로써 이러한 문제들을 해결했다고 합니다.


## Different Distances
두 확률분포 사이의 거리 metric은 다음과 같은 것들이 있습니다.

![Different_Distances]({{site.baseurl}}/assets/img/distance_metric.jpg)

먼저, TV는 두 분포의 측정값의 거리 중 최대값을 의미합니다.

![TV]({{site.baseurl}}/assets/img/tv.jpg)

KL divergence는 두 분포의 차이를 계산할 때 많이 사용되는 metric이지만, input으로 들어가는 두 분포의 순서에 따라 값이 달라지기에 distance를 나타내기엔 적절하지 않습니다.
그래서 KL divergence를 응용한 것이 Jensen-Shannon distance 입니다.

![KL_JS]({{site.baseurl}}/assets/img/kl_js.jpg)

하지만, 이러한 기존의 distance들은 다음과 같은 문제점을 가지고 있습니다.
* Saturated gradients
* 비교하는 두 분포에 의미 있는 intersection이 없을 경우 학습이 잘 되지 않는다.
* Mode collapse : discriminator를 속일 수 있는 특정 이미지만 generator에서 생성하게 됨
* Unstable : generator, discriminator의 adversarial training이 어려움 

그리고 이러한 문제점을 보완한 것이 바로 이 논문에서 제시한 EM(Earth Mover) distance 입니다.

![EM_dist]({{site.baseurl}}/assets/img/em_dist.jpg)

식은 복잡하게 되어 있지만 위 식은 <img src="https://latex.codecogs.com/svg.latex?\; P_{r}" />을 <img src="https://latex.codecogs.com/svg.latex?\; P_{g}" />로 옮길 때 드는 최소한의 비용을 의미합니다.

![EM_dist_example]({{site.baseurl}}/assets/img/em_dist_example.jpg)

그럼, EM distance가 기존과 어떤 차이가 있는지 보겠습니다.

<------------- 작성중 ------------->

## Reference
paper :  
https://arxiv.org/abs/1406.2661  
https://arxiv.org/abs/1701.07875  
https://arxiv.org/abs/1704.00028  

etc :  
https://www.slideshare.net/ssuser7e10e4/wasserstein-gan-i  
https://www.youtube.com/watch?v=tKQwlf-DAl0  
https://jonathan-hui.medium.com/gan-wasserstein-gan-wgan-gp-6a1a2aa1b490  






