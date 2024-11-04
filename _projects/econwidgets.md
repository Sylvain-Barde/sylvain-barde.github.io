---
layout: page
title: econWidgets
description: Jupyter visualisations for Maths & Stats
img: assets/img/ecnwdg/scatter_plot_widget.png
importance: 1
category: teaching
related_publications: False
---

### Table of contents
- [Overview](#overview)
- [Project contributions](#project-contributions)
- [Areas of improvement](#areas-of-improvement)

### Overview

About 5 years ago I got tasked with taking over our first year *Mathematics for Economics* and *Statistics for Economics* modules. The context was one of poor student engagement, on topics that were seen as a bit dry, with a very wide range of student backgrounds. The key challenge here was to be able to present mathematical and statistical material in a clear and engaging manner. One of the solutions I came up with was to build on thje existing functionality of [Jupyter Widgets](https://ipywidgets.readthedocs.io/en/8.1.2/) to generate a set of fully interactive plots, which provide intuitive visualisations of key concepts, both at the point of delivery (i.e. a lecture), but also when students go back to the material in their own time. The parameters in the functions plotted in the widget diagrams can be adjusted using sliders or numerical input boxes, and variaous diagram/plot confirguration options can be adjusted using checkboxes or drop-down lists. This enables a very flexible environment for teaching, as the usually static plots shown in a traditional slideshow become dynamic and adjustable in realtime, based either on the story I want to tell in my teaching plan, or (even better) in response to student questions. For statistics in particular, the ability to run Monte Carlo simulations in real-time is invaluiable, as a way of getting students to visualise everything to do with sampling distributions.

I use these widgets everywhere: they form the basis of my lecture slides, using the [RISE](https://rise.readthedocs.io/en/latest/#disclaimer) plugin to convert a jupyter notebook into a slideshow, and also in interactive notebooks I provide to students as extra material. The notebooks are available in my [interactive teaching](https://github.com/Sylvain-Barde/interactive_teaching) github repo, which I make available to students using [binder](https://mybinder.org/), so that they don't have to worry about maintaining the appropriate python/jupyter environments.

The sections below provide an overview of the three main types of widgets I use. A full list is available on the [econWidgets](https://github.com/Sylvain-Barde/econWidgets) repo, as well as a demonstration jupyter notebook that provides a demonstration for each widget.

#### Mathematics widgets

The first set of widgets applies to Mathematics. Our typical student cohort does not have a strong mathematical background, therefore I had to find inuitive ways of presenting and illustrating key maths concepts such as matrices, derivatives, etc. to an audience with limited backgrounds in mathematics. This is where the widgets provide a great visual tool.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/matrix_widget.png" title="Output of the matrix widget" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/derivative_widget.png" title="Output of the univariate derivative widget" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/multivar_widget.png" title="Output of the multivariate derivative widget" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/taylor_widget.png" title="Output of the taylor series widget" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A few of my maths widets. Clockwise from top left: the geometry of matrices, derivatives and turning points, Taylor appxominations and mthe intuition behind partial derivates in a multivariate setting.
</div>

#### Statistics widgets

As already stated, the great benefit here is the possibility of running Monte-Carlo exercises in the background of a presentation or notebook, which really helps to present key statistical concepts in an intuitive way. Explaining the central limit theorem, the $$\sqrt{N}$$ convergence of sample estimates to population parameters, or the bias/variance trade-off is much easier when you can actually **show** it live!

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/clt_illustration_widget.png" title="Output of the CLT widget" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/norm_area_widget.png" title="Output of the normal distribution widget" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/hypothesis_test_widget.png" title="Output of the hypothesis test widget" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/error_type_widget.png" title="Output of the typeI/II error widget" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Some statistics widets. Clockwise from top left: the CLT in practice, probabilities as areas under a distribution, type I and type II errors, the logic behind hypothesis testing.
</div>

#### Application widgets

Finally, because the main modules I teach are called 'Mathamatics for Economics' and 'Statistics for Economics', I guess I feel compelled to add some economics content as well... So I also have a range of application widgets, which show how the relevant mathematical/statistical concept is used in the context of economics.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/plot_income_widget.png" title="Output of the income distribution widget" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/tax_widget.png" title="Output of the tax impact widget" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/profit_maximisation_widget.png" title="Output of the profit maximisation widget" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ecnwdg/utility_widget.png" title="Output of the utility maximisation widget" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A few Economic application widets. Clockwise from top left: the UK income distribution, or why average incomes might not be representative, why the impact of of a tax depends on elasticities, a visualisation of the Lagrange method in consumer choice and profit maximisation using margins.
</div>

### Project contributions

What bits does this project reach that others don't?
- The main contribution is the incredibly valuable toolkit this provides for explaining core mathematical/statistical/economic concepts in an intuitive and flexible way.
- Once the user gets their head around the logic of how to declare and link the juputer widgets to the main plot, it becomes really easy to create newwer widgets by re-purposing existing ones. The marginal cost of a new widget keeps falling the more of them you have.
- What makes this particularly useful is the fact that this integrates well with RISE and decktape plugins, creating interactive slideshows that can then be converted to PDF.

### Areas of improvement

Things I'm not that happy about right now.

- These work in the classic Jupyter notebook, and have been tested in version 7 of notebooks. However, they do not (yet?) work in JupyterLab, and given that this seems to be the main direction Jupyter is going in, more work is needed to move these to that platform. Work in progress here!

