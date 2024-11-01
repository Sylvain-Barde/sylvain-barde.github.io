---
layout: page
title: econWidgets
description: Jupyter visualisations for Maths & Stats
img: assets/img/ecnwdg/scatter_plot_widget.png
importance: 1
category: teaching
related_publications: Falst
---


Just a placeholder for the moment, whilst I figure out the best way of organising the information!

### Table of contents
- [Overview](#overview)
- [Project contributions](#project-contributions)
- [Areas of improvement](#areas-of-improvement)

### Overview

Used in my slides, using the RISE plugin, and also in interactive notebooks for students.

#### Mathematics widgets

The first set of widgets applies to Mathematics. Our typical student cohort does not have a strong mathematical background, therefore I had to find inuitive ways of presenting and illustreating key maths concepts such as matrices, derivatives, etc. to an audience with limited backgrounds in mathematics. This is where the widgets provide a great visual tool.

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
    Placeholder caption.
</div>

#### Statistics widgets

The great aspect here is the possibility of running Monte-Carlo exercises in the background of a presentation or notebook, which really helps to present key statistical concepts in an intuitive way. Explaining the central limit theorem, the $$\sqrt{N}$$ convergence of sample estimates to population parameters, or the bias/variance trade-off is much easier when you can actually **show** it!

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
    Placeholder caption.
</div>

#### Application widgets

Finally, because the main modules I teach are called 'Mathamatics for Economics' and 'Statistics for Economics', I guess I feel compelled to add some economics as well... So I also have a range of application widgets, which show how the relevant mathematical/statistical concept is used in the context of economics.

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
    Placeholder caption.
</div>


### Project contributions

What bits does this project reach that others don't?
- Integrates with RISE and decktape
- Provides incredibly valuable tools for explaining core concepts in an intuitive and flexible way.

### Areas of improvement

Things I'm not that happy about right now.

- These work in the classic Jupyter notebook, and have been tested in version 7 of notebooks. However, they do not (yet?) work in JupyterLab, and given that this seems to be the main direction Jupyter is going in, more work is needed to move these to that platform.
