---
layout: page
permalink: /monte-carlo/
title: Monte Carlo Simulation
description: An introduction to the Monte Carlo method
nav: false
---

## Monte Carlo 

To simulate events in physics one has to perfom a lot of integral. 
#TODO trouver un evenement et une fonction à integrer pour illustrer le principe de Monte carlo 

For exemple we might need to integrate the function $f(x)$ over [a,b]: 
$$I=\int_a^bf(x)\,dx$$
To do this we could use the basic numerical method such as the trapzeoidale rule, the simpson rule, etc...
Those methode are efficient for a integral at low dimension, and converge with $\propto \frac{1}{N^2}$ for the trapzeoidale method and $\propto \frac{1}{N^4}$ for the simpson rule for a one dimension integral. However, for a integral over $d$ dimensions, the convergence is goes to $\propto \frac{1}{N^{2/d}}$ and $\propto \frac{1}{N^{4/d}}$.

On the other hand, a Monce Carlo method converge $\propto \frac{1}{\sqrt{N}}=\frac{1}{N^{\frac{1}{2}}}$ for any dimensions integral. 
For a 4 (8) dimensional integral the MC method converge as fast as the trapezoidale (simpson) rule, and faster for higher dimension.

A Monte Carlo method is any method that make use of Random numbers and probability statistics to solve a problem.
The law of Large number  tells us that if we take a sequence of independent and identically distributed (iid) random variables $X_i$ with an expectation $\mathbb{E}[X]$, then the empirical mean converges almost surely to the expectation:
$$\frac{1}{N} \sum_{i=1}^{N} X_i \quad \xrightarrow{N \to \infty} \quad \mathbb{E}[X]$$



$$I = \int_a^b f(x) dx$$

T approximates it by taking **random samples $x_i$ in [a,b]** and computing:

$$I \approx \frac{b-a}{N} \sum_{i=1}^{N} f(x_i)$$

But how do you choose the $x_i$?

At first glance, we might choose $x_i$ from a uniform distribution along $[a,b]$. However, this method is not optimal, as it may lead to inaccurate integral approximations. This is where Inverse Transform Sampling becomes useful.

### The Role of the CDF

Inverse Transform Sampling relies on the cumulative distribution function (CDF):

$$F_X(x) = \int_{-\infty}^{x} f_X(t) \, dt$$

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/statistics/ITS/cdf-pdf.png" title="example image" class="img-fluid rounded z-depth-1" %}
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

From the law of large number we know that the integral $I=\int f(x)$

[!NOTE]
<div id="markdown-container">
<details>
<summary>Law of large numbers</summary>

> The law of large numbers tells us that if we take a sequence of independent and identically distributed (iid) random variables $X_i$ with an expectation $\mathbb{E}[X]$, then the empirical mean converges almost surely to the expectation:
> $\frac{1}{N} \sum_{i=1}^{N} X_i \quad \xrightarrow{N \to \infty} \quad \mathbb{E}[X]$

</details>
</div>
