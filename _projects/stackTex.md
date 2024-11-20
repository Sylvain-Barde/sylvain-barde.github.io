---
layout: page
title: stackTex
description: Build and manage STACK question banks from Latex templates
img: assets/img/stacktex/quiz_pdf.png
importance: 1
category: teaching
related_publications: False
---

### Table of contents
- [Overview](#overview)
- [Project contributions](#project-contributions)
- [Areas of improvement](#areas-of-improvement)

### Overview

When I took over the first year *Mathematics for Economics* and *Statistics for Economics* modules in 2019, we had poor engagement with the material and a range of student abilities. Needed regular practice, which only happens if given carrots. But the marking load implied was impossible. Automation was the key!

This became invaluable during covid, where online assessment was the only option.

[STACK](https://stack-assessment.org/)

[Moodle](https://moodle.org/)

[stackTex](https://github.com/Sylvain-Barde/stackTex)

The sections below provide an overview of the stackTex toolbox functionality. A full description is available on the [stackTex](https://github.com/Sylvain-Barde/stackTex) repo, which includes an entire demonstration folder containing a working example of a question bank and quizzes.

#### Latex exercise template

Illustrate with a simple example, more a provided in the GitHub repo

{% raw %}
```Latex
%-------------------------------------------------------------------------------
% This section contains the randomised exercise parameters
\fieldname{exerciseParameters}
[r1,r2,r3,r4,r5]:[2+rand(9),3+rand(5),2+rand(9),2+rand(9),2+rand(4)]

% Question A
[qAp1,qAp2]:[r1*r2,r2-1]

% Question B
[qBp1,qBp2]:[2*r4,r5+1]

% Question C
[qCp1,qCp2]:[qAp1*qAp2,qAp2-1]

% Question D
[qDp1,qDp2]:[r5*qBp2,qBp2+1]

\fieldname{questionBlurb}
A multivariate function is given by:
\[
z = {r1}x^{r2} + {r3}xy + {r4}xy^2 - \frac{x}{y^{r5}}
\]

%-------------------------------------------------------------------------------
% This section contains the individual question information
\fieldname{questionType}
Algebraic

\fieldname{questionText}
Find the first-order partial derivative with respect to $x$.

\fieldname{prompt}
$\frac{\partial z}{\partial x}$

\fieldname{solution}
${qAp1}x^{qAp2} + {r3}y + {r4}y^2 - \frac{1}{y^{r5}}$

\fieldname{mark}
2

%-------------------------------------------------------------------------------
% This section contains the individual question information
\fieldname{questionType}
Algebraic

\fieldname{questionText}
Find the first-order partial derivative with respect to $y$.

\fieldname{prompt}
$\frac{\partial z}{\partial y}$

\fieldname{solution}
${r3}x + {qBp1}xy + \frac{{r5}x}{y^{qBp2}}$

\fieldname{mark}
2

%-------------------------------------------------------------------------------
% This section contains the individual question information
\fieldname{questionType}
Algebraic

\fieldname{questionText}
Find the second-order partial derivative with respect to $x$.

\fieldname{prompt}
$\frac{\partial^2 z}{\partial x^2}$

\fieldname{solution}
${qCp1}x^{qCp2}$

\fieldname{mark}
3

%------------------------------------------------------------------------------
% This section contains the individual question information
\fieldname{questionType}
Algebraic

\fieldname{questionText}
Find the second-order partial derivative with respect to $y$.

\fieldname{prompt}
$\frac{\partial^2 z}{\partial y^2}$

\fieldname{solution}
${qBp1}x - \frac{{qDp1}x}{y^{qDp2}}$

\fieldname{mark}
3
%-------------------------------------------------------------------------------
% This section contains the individual question information
\fieldname{questionType}
Algebraic

\fieldname{questionText}
Find the second-order partial derivative with respect to $x$ and $y$.

\fieldname{prompt}
$\frac{\partial^2 z}{\partial x \partial y}$

\fieldname{solution}
${r3} + {qBp1}y + \frac{{r5}}{y^{qBp2}}$

\fieldname{tolerance}

\fieldname{mark}
4

```
{% endraw %}

### PDF and STACK outputs

Note the randomisation

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/quiz_pdf.png" title="PDF output of stackTex question" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/quiz_stack.png" title="Moodle/STACK output of stackTex question" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The output of the example question. on the left the PDF, on the right the Moodle version.
</div>

solutions. Note the auto-grading

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/quiz_pdf_sol.png" title="PDF solutions for stackTex question" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/quiz_stack_sol.png" title="Moodle/STACK auto-grading of stackTex question" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The solutions of the example question. on the left the PDF, on the right the Moodle version.
</div>

#### More complex behaviour is possible

Illustrations

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/system.png" title="System of equations plot" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/quadratic.png" title="quadratic plot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/histogram.png" title="Histogram plot" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/hypothesis.png" title="Hypothesis test plot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Some illustrations of the possible plots. Clockwise from top left: the CLT in practice, probabilities as areas under a distribution, type I and type II errors, the logic behind hypothesis testing.
</div>

Tables

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/table1.png" title="A frequency table" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/table2.png" title="A least squares regression" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Some illustrations of possible tables from statistics exercises. On the left is an example of a frequency table, on the right is 'OLS by hand' for a bivariate regression. Bold entries represent randomised values.
</div>

### Project contributions

What bits does this project reach that others don't?
- Randomisation
- Handles BOTH pdf and online outputs
- Automated grading
- Platform independent as based on open-source resources. Not linked to any specific publisher.


### Areas of improvement

Things I'm not that happy about right now.

- Not as slick as a publisher platform. Inputting answers using latex syntax can be challenging for undergraduate students, so a lot of care has to be taken to explain this
- Doesn't support the feedback tree, only a true/false assessment. Could in principle be extended by hand, thus providing a stating points
- Accessibility of PDFs produced. This is a wider issue with Latex documents, but as progress is made, the various solutions might be worth investigated.
