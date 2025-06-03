---
title: 'Denoising Diffusion Probabilistic Models Explained'
date: 2025-06-03
permalink: /posts/ddpm_explained/
tags:
  - Generative AI
---

There are so many resources on the internet which make an attempt to explain Denoising Diffusion Probabilistic Models (DDPM). However I feel that many of these resources do not go into detail on the derivation of the algorithm. In this post I will explain every part of the DDPM algorithm so that you understand how the final simple regression objective is obtained.


The core idea of diffusion is to structure the process of sampling as a dynamical system. Generating a sample from a prior noise distribution $p_T(x_T) := \mathcal{N}(x_T; \mathbf{0}, \mathbf{I})$ is done by iteratively sampling a learned probabilistic model $p_\theta(x_{t-1} | x_t)$.


To learn this reverse process model a forward process is defined. A requirement of the forward process is to convert any distribution into a standard normal distribution. Fortunately this is not too difficult because according to the central limit theorem the convolution of a number of density functions tends towards the normal distribution. 

## Simple Forward Process
Consider a forward process:

$$x_t = x_{t-1} + \epsilon_t, \qquad \epsilon_t \sim\mathcal{N}(\mathbf{0}, \sigma\mathbf{I}).$$

Assume the initial distribution of $x_0 \sim p(x_0)$ where $\mathbb{E}[x_0] = \mu$ and $\textrm{Cov}(x_0) = \Sigma_{x_0}$. Even if $p(x_0)$ is not gaussian, $x_T$ will be gaussian with some mean and covariance.

$$x_T = x_0 + \sum_{t=1}^T \epsilon_t$$

The mean of $x_T$:

$$\mathbb{E}[x_T] = \mathbb{E}[x_0] + \mathbb{E}[\sum_{t=1}^T \epsilon_t]$$

$$\mathbb{E}[x_T] = \mu$$

Assuming $\textrm{Cov}(x_0, \epsilon_t) = 0,\quad \forall t\in[1,T]$. Also assuming $\textrm{Cov}(\epsilon_a, \epsilon_b) = 0,\quad \forall a, b\in[1,T]$. The covariance of $x_T$:

$$\textrm{Cov}(x_T) = \Sigma_{x_0} + T\sigma^2\mathbf{I}.$$

So under the simple forward process that I have shown here we can convert any distribution over $x_0$ into a gaussian distribution over $x_T$ where:

$$x_T \sim \mathcal{N}(\mu, \Sigma_{x_0}+T\sigma^2\mathbf{I}).$$

The issue with this forward process is that we would like to transform any distribution into an isotropic gaussian with zero mean and identity covariance matrix.

## DDPM Forward Process

