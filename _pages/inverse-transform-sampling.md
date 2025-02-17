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

$$I = \int_a^b f(x) dx$$

Monte Carlo approximates it by taking **random samples $x_i$  in [a,b]** and computing:

$$I \approx \frac{b-a}{N} \sum_{i=1}^{N} f(x_i)$$

But how to you choose the $x_i$ ?

At first glance we might choose to choose $x_i$ from an uniform distribution along $[a,b]$.

However this way of thinking is not optimal at all, as it might lead to inacuarate integral approximation. 

That is where Inverse Transform Sampling can be helpful. 


$$F_X(x) = \int_{-\infty}^{x} f_X(t) \, dt$$

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/statistics.ITS/cdf-pdf.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Relation between CDF and PDF.
</div>

$$\lim_{x \to +\infty} F_X(x)=1$$


$$f_X(x) = \frac{d}{dx} F_X(x)$$