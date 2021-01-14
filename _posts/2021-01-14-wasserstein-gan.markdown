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
확률분포를 학습한다는 것은 확률밀도를 정의하고 real data에 대해 확률 값을 최대화하는 문제를 푸는 것으로 접근할 수 있습니다.

