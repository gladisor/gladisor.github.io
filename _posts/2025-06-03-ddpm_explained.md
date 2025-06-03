---
title: 'Denoising Diffusion Probabilistic Models Explained'
date: 2025-06-03
permalink: /posts/ddpm_explained/
tags:
  - Generative AI
---

Draft in progress...

There are so many resources on the internet which make an attempt to explain Denoising Diffusion Probibalistic Models (DDPM). However I feel that many of these resources do not go into detail on the derivation of the algorithm. In this post I will explain every part of the DDPM algorithm so that you understand how the final simple regression objective is obtained.

Forward process:

$$x_t \sim q(x_t | x_{t-1}) := \mathcal{N}(x_t ; \sqrt{1-\beta_t} x_{t-1}, \beta_t\mathbf{I} )$$