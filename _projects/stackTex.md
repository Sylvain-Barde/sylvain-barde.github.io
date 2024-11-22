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

As explained in the [econWidgets](https://sylvain-barde.github.io/projects/econwidgets/) project, when I took over the first year *Mathematics for Economics* and *Statistics for Economics* modules in 2019, we had problems stemming from a combination of poor student engagement with the material and a great heterogeneity in the range of student abilities. The latter problem in turn came from the fact that Kent doesn't have a requirements to have an A-level in maths to study economics. This is great in terms of accessibility, offering the benefits of an economics degree to students who might not otherwise be able to go down that route. But it's challenging in terms of delivering the teaching. The conundrum here is that becoming proficient in mathematics or statistics requires regular practice, for example, solving a lot of problem sets. Students, however, often don't engage with material unless it is assessed and carries a mark, and regular marking of assessments requires a lot of resources. Needless to say, multiple problem sets a week for a cohort of around 250 students was a non starter.

The solution to this is of course automated marking, but I wanted something that was more flexible than the standard multiple-choice quiz which is often the only option in these situations. Having played around with ways of implementing maths quizzes as part of a 'technology in learning' module I took while doing my [PGCHE](https://www.postgrad.com/subjects/teaching_education/pgche/), I knew of the existence of the [STACK](https://stack-assessment.org/) plugin, which extends the popular [Moodle](https://moodle.org/) virtual learning environment and allows symbolic algebra questions to be integrated into the maths quiz using [Maxima](https://maxima.sourceforge.io/) under the hood. Because my University already ran Moodle, implementing STACK questions was not that complicated. The main problems I was facing were:
- The sunk cost of taking the **hundreds** of excellent problem sets that had been gathered by the previous professors over decades, and writing them up in STACK. Most of these were in old Microsoft Word files and needed updating anyway.
- Having to maintain two parallel question banks containing the same problem sets: one in text files (Word or Latex) and one in STACK/Moodle. Inevitably, divergences would appear...

This is where I had the idea for stackTex, a python toolkit for parsing Mathematics and Statistics exercises written in Latex (using a flexible template), saving a **single** question bank than can then be used to generate a range of outputs: PDF worksheets for seminar practice, PDF exam papers for final assessments, and XML outputs compatible with Moodle/STACK quizzes. What spurred me into action was the COVID pandemic, where online teaching and assessment became the norm, and the ability to randomise numerical assessments at the student-level to avoid cheating was invaluable. While developing stackTex was time-consuming, in practice it saved even more time!

The sections below provides an overview of the stackTex toolbox functionality. A full description is available on the [stackTex](https://github.com/Sylvain-Barde/stackTex) repo, which includes an entire demonstration folder containing a working example of a question bank and quizzes.

#### Latex exercise template

The Latex exercises need to be written using a standard template in order to ensure that all the fields are correctly imported. The simple example below is provided as an illustration, and more are available in the GitHub repo.

A key aspect of the template is the ability to declare (random) and variables for the exercises. Essentially, this provides the numerical 'backbone' for the exercise, linking the exercise solutions and any student feedback to the deep settings of the random number generator. These variables and parameters then directly enter the latex text in the questions and solutions, and when implemented in STACK, the solution provided by a student can be checked against the exercise solution.

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

Once imported, two types of output are possible: PDF and XML (for importing to Moodle/STACK). The figure below shows how the Latex exercise example above looks in both formats. Note the role of the randomisation: the exercise structure is the same in both cases, but the equation and its derivatives are clearly different.

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

The template allows for question-specific feedback and solutions to be included, so that:
- PDF solution documents can be generated, destined either for students themselves, for example at the end of a seminar, or for anyone in a marking team who might have to grade an formal exam.
- Moodle/STACK quizzes can provide feedback to students once their assessment is submitted.
solutions.

The figure below again shows what this looks like for the Latex example. Importantly, Note the way the STACK auto-grading is able to assess the arithmetic equivalence of the student input, in particular $$y^{-n} = \frac{1}{y^n}$$. This is a feature of STACK, not stackTex itself, but is one of the things that make it appealing for setting more challenging mathematics exercises, where the solution can legitimately be written in several ways.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/quiz_pdf_sol.png" title="PDF solutions for stackTex question" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/stacktex/quiz_stack_sol.png" title="Moodle/STACK auto-grading of stackTex question" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The solutions of the example question. On the left the PDF, on the right the Moodle version.
</div>

#### More complex behaviour is possible

The example used in this post only showcases the basic functionality. In particular, tables and figures can be integrated in the exercises, generating more complex exercises. Here are some examples of figures from my existing question banks:

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
    Some illustrations of the question bank figures Clockwise from top left: the solution to a system of two equations and two unknowns, the maximisation of a quadratic, test statistics and critical values in hypothesis testing and a histogram for a table of frequencies.
</div>

Here are two examples of tables:

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
- The **key** feature is that it handles **both** pdf and online outputs, which is really important when delivering a university module. It's great to use online quizzes, but you also have to run tutorials, seminars and provide revision resources, often as PDF documents, and being able to manage both formats with a single tool is a time saver.
- An attractive aspect is that stackTex supports the 'out-of-the-box' randomisation of the exercises provided by the STACK plugin. This is not a requirement, exercises can be written with fixed parameters, but is nice to have for online assessment.
- Similarly, the ability to use a pretty clever [CAS](https://en.wikipedia.org/wiki/Computer_algebra_system) for automated grading is a force multiplier for teaching mathematics. I can give my 250 students weekly practice quizzes, essentially ensuring that they practice maths regularly, without incurring the massive marking cost. Clearly, this provided by STACK itself, not by stackTex, but the toolkit lowers the entry cost of accessing these systems.
- Finally, this provides an open-source way of gaining the benefits of automated grading. I regularly get visits from various agents representing publishers, who all at this point offer variations of online platforms providing the same service. Most of them are great, but require licenses or lock you into a specific textbook. This does not...

### Areas of improvement

Things I'm not that happy about right now.

- First, the flipside of the coin I mentioned above. This is not as slick as a publisher platform. I particular, the examples above show that answers need to be inputted using latex syntax, while a lot of paid-for platforms will offer more user-friendly GUIs. Figuring out how to input answers can be challenging for undergraduate students, so a lot of care has to be taken to explain this.
- STACK offers a pretty sophisticated feedback tree system, where an answer that is incorrect can be passed to a series of secondary checks, so that a range of feedback can be provided based on the severity of the error. Currently, stackTex does not support the feedback tree, only the initial true/false assessment. Should a user want to provide this, they would have to extend the feedback tree by hand, and stackTex would only provide a stating point.
- Finally, there is the problem of the accessibility of the PDFs produced from the Latex input. This is a wider issue that affects all Latex documents in general. Progress is being made, for example the `accessibility` and `axessibility` packages for tagging text and maths respectively. Currently, these can be added to the Latex output of the stackTex package ,but at some point I will investigate if this can be included as part of the output generation.
