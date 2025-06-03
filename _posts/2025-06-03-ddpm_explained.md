---
title: 'Denoising Diffusion Probabilistic Models Explained'
date: 2025-06-03
permalink: /posts/ddpm_explained/
tags:
  - Generative AI
---

In progress...

Forward process:

$$x_t \sim q(x_t | x_{t-1}) := \mathcal{N}(x_t ; \sqrt{1-\beta_t} x_{t-1}, \beta_t\mathbf{I} )$$