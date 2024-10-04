---
layout: page
title: BEGRS
description: Bayesian Estimation with Gaussian Process Regression Surrogates
img: assets/img/begrs/GPposterior.jpg
importance: 1
category: research
related_publications: true
---

### Table of contents
- [Overview](#overview)
- [Project contributions](#project-contributions)
- [Areas of improvement](#areas-of-improvement)

### Overview

This was one of my COVID projects. Like many, I found myself having more time than expected, stuck in closed quarters, and I needed something to channel the cabin fever... So I started scratching my head over the problem of estimating the large, computationally burdensome agent-based models that my colleagues had developed over the years. There are plenty of indirect inference methods out there for estimating the deep parameters of simulation models, but these often rely on in-the-loop or open-ended simulations of the model. With large agent-based models that take minutes to generate a single simulation run, these methods just don't scale... I needed to find a way to do more with less.

The full details for this are provided in {% citet barde2024bayesian %}, however, as a quick overview, the methodology uses a Gaussian process as a surrogate model for the one-step ahead prediction of the model given an observed state and some model parameters.

In many ways, this first pass at the problem is kind of low-tech: no Bayesian learning of the parameter space is carried out to acquire samples, no empirical data is used to generate deviations. All this is designed to reduce the compute burden involved in simulating the underling model. In practice, in order to keep the problem computationally tractable, the GP is trained using the variational methods of {% cite hensman2015scalable %} using the GPpytorch toolbox of { % cite gardner2018gpytorch % } to provide GPU acceleration.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/begrs/GPprior.jpg" title="GP prior" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/begrs/GPposterior.jpg" title="GP posterior" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The left plot shows the Gaussian process prior, which is a prior over the space of functions that could generate the data. The right shows the posterior, once the training data has been seen. Note that of course, convergence only occurs in the region of the parameter space for which we have simulation data...
</div>

Once the GP surrogate is trained, it can be used in a second stage to provide a surrogate likelihood in a standard Bayesian estimation for an observation $$y_t$$, given $$y_{t-1}$$ and a parameter vector $$\theta$$. The only requirement the methodology has relative to standard Bayesian methods is that the prior on the parameter vector must constrain the parameter space to the hypercube within which the training parameter samples were drawn. The reason for this requirement is illustrated below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/begrs/GPlikelihoodGood.jpg" title="good case plot" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/begrs/BegrsPlotGood.jpg" title="good case likelihood image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The left plot shows the case where the empirical observation (horizontal line) falls within the range of the training data. On the right, this leads to a well-behaved likelihood, with the parameter prior simply 'pinching off' the contribution of the GP prior.
</div>

One neat thing that I hadn't initially realized is that this setup actually provides a kind of 'fault-detection' for the training data used in the training of the GP surrogate. As illustrated below, if the empirical observation is inconsistent with the range used in the training, then the GP prior will dominate the GP posterior, and the likelihood's peak(s) will occur outside of the parameter range used for the training data. The parameter prior will pinch this off, resulting in a quasi-degenerate parameter posterior on the boundary.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/begrs/GPlikelihoodBad.jpg" title="bad case plot" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/begrs/BegrsPlotBad.jpg" title="bad case likelihood" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The empirical observation (horizontal line) now falls outside the range of the training data. In this case, the diffuse GP prior is actually a better predictor than the trained posterior. This leads the likelihood, on the right, to peak outside of the allowed parameter range, creating a degeneracy at the boundary.
</div>

As a practical example, I've applied the methodology to the {% cite caiani2016agent %} model. It can take the original model 40 minutes to produce a usable 200-300 long macro time series, so in-the-loop simulation is out of the question. 1000 simulations of 200 observations each, using parametrizations drawn from a Sobol sequence, are enough to produce a decent set of estimates for the 12 free parameters.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/begrs/dens_all.jpg" title="caiani model estimates" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The BEGRS posterior parameter densities for the two empirical datasets. Original parameter calibrations in black.
</div>

### Project contributions
#### What bits does this project reach that others don't?

The methodology as implemented has several nice characteristics:
- GP gradients are easy to compute, so gradient-based methods, such as BFGS for finding the mode of the posterior or Hamiltonian MCMC for drawing posterior samples, can be implemented out-of-the-box.
- Because the second stage parameter estimation (given the GP surrogate) is a standard Bayesian framework, a full Bayesian workflow can be followed, including posterior checks, for example {% cite cook2006validation %}, or {% cite talts2018validating %}.
- Finally, that the methodology seems to perform well with limited training data, so given all the compromises made on the surrogate model (see next section!) it's 'mission accomplished' for the central aim.
- This is improved by the fact that the surrogate does not require retraining before estimation on different datasets. For instance, the same surrogate is used in the US empirical estimation above.

As a sanity check, and an illustration of the last two points, I ran a simple Monte Carlo example, training a GP surrogate using 1000 simulations of VAR(1) models with 4 variables and 200 observations, where the 16 parameters of the autoregressive matrix were drawn from Sobol sequences. Both a parameter recovery exercise and a Simulated Bayesian Computing posterior check {% cite talts2018validating %} show that the methodology performs well.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/begrs/dens_var_uncorr_0.jpg" title="VAR estimation results" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/begrs/sbc_var_uncorr_0.jpg" title="VAR SBC results" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The left plot shows the parameter densities obtained in a parameter recovery exercise: BEGRS compares favourably to ABC-SMC for a fraction of the simulation calls. The right plot shows that the SBC analysis reveals no issues with the posterior.
</div>

### Areas of improvement
#### Things I'm not that happy about right now.

Well, a lot of nice things were sacrificed as part of the drive to make a simple model that generalises well with minimal training data.

- Vecchia approximation might not be appropriate for non-linear responses
- Will struggle with discontinuities in response. This will slow convergence with respect to the number of training samples
