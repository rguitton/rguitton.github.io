---
layout: page
permalink: /inverse-transform-sampling/
title: Inverse Transform Sampling
description: An introduction to Inverse Transform Sampling
nav: false
nav_order: 8
---

## Inverse Transform Sampling

For example, to compute an integral like:

$$I = \int_a^b f(x) dx$$

Monte Carlo approximates it by taking **random samples $x_i$ in [a,b]** and computing:

$$I \approx \frac{b-a}{N} \sum_{i=1}^{N} f(x_i)$$

But how do you choose the $x_i$?

At first glance, we might choose $x_i$ from a uniform distribution along $[a,b]$. However, this method is not optimal, as it may lead to inaccurate integral approximations. This is where Inverse Transform Sampling becomes useful.

### The Role of the CDF

Inverse Transform Sampling relies on the cumulative distribution function (CDF):

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

Using the CDF instead of the PDF provides a **bijective** relationship between $[0,1]$ and $[a,b]$. Without the CDF, a value like 0.2 could correspond to multiple values in $[a,b]$, making transformation ambiguous.

### How Inverse Transform Sampling Works

In Inverse Transform Sampling, we generate a random number $U$ uniformly distributed over $[0,1]$ and apply the inverse CDF ($F^{-1}$) to obtain a corresponding value $X$ in the target interval $[a,b]$:

$$X = F^{-1}(U)$$

The key insight is that the CDF increases when the PDF is nonzero and remains constant when the PDF is zero. If we sample uniformly along the y-axis from $[0,1]$, we are more likely to land in a region where the CDF is increasing rather than where it is flat. This ensures that our samples are more frequently drawn from regions where the PDF is nonzero, improving the efficiency of sampling.

If we were to use the PDF directly, we would not have a unique mapping between $U$ and $X$ because the PDF represents density rather than a one-to-one correspondence. However, since the CDF is strictly increasing for a continuous distribution, each $U$ in $[0,1]$ corresponds uniquely to a single $X$ in $[a,b]$, ensuring invertibility.

Thus, without the CDF, multiple values of $X$ could correspond to the same $U$, making the transformation ambiguous. The CDF guarantees a well-defined inverse mapping, allowing us to efficiently sample from the target distribution.

