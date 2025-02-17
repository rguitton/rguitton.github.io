---
layout: page
permalink: /inverse-transform-sampling/
title: Inverse Transform Sampling
description: An introduction to Inverse Transform Sampling
nav: false
nav_order: 8
---

Inverse Transform Sampling


For example, to compute an integral like:

$I = \int_a^b f(x) dx$

Monte Carlo approximates it by taking **random samples $x_i$  in [a,b]** and computing:

$I \approx \frac{b-a}{N} \sum_{i=1}^{N} f(x_i)$

But how to you choose the $x_i$ ?