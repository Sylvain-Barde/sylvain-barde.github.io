---
layout: page
title: Fast MCS
description: A fast Model Confidence Set algorithm
img: assets/img/benchmark_mcs.jpg
importance: 1
category: research
related_publications: true
---

### Table of contents
- [Overview](#overview)
- [Project contributions](#project-contributions)
- [Areas of improvement](#areas-of-improvement)

### Overview

Fast updating implementation of the Model Confidence Set (MCS) algorithm {% cite Hansen_et_al_2011 %}. Given a candidate collection of $$M$$ models, the elimination implementation has a $$\mathcal{O}(M^3)$$ time complexity and a $$\mathcal{O}(M^2)$$ memory requirement. The fastMCS updating implementation reduces this down to  a $$\mathcal{O}(M^2)$$ time complexity and a $$\mathcal{O}(M)$$ memory requirement.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/fastMCS/benchmark_time_N_250.jpg" title="Time benchmarking for N=250" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/fastMCS/benchmark_mem_N_250.jpg" title="Memory benchmarking for N=250" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    These plots show the time (left plot) and memory (right plot) benchmarking exercises in log units for an empirical sample of N=250 observations. The trajectories confirm the cubic time complexity and quadratic memory requirement for the elimination algorithm. The equivalent requirements for the updating algorithm are quadratic and linear respectively.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/fastMCS/benchmark_time_N_30.jpg" title="Time benchmarking for N=30" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/fastMCS/benchmark_mem_N_30.jpg" title="Memory benchmarking for N=30" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    These are equivalent benchmarking plots for the N=30 case. Crucially, even for such a small evaluation sample, in every case the model rankings and p-values outputed by the updating algorithm exactly match those of the elimination algorithm.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0", markdown="block">

    |------------+-------------+-------------+-+------------+-------------|
    |            | Elimination |             | | Two-pass   |             |
    |------------|------------:|------------:|-|-----------:|------------:|
    |            |  Time (sec) | Memory (MB) | | Time (sec) | Memory (MB) |
    |------------+-------------+-------------+-+------------+-------------|
    | M = 500    |        295  |      6,017  | |       3    |      23     |
    | M = 1,000  |      2,318  |     24,055  | |      11    |      44     |
    | M = 2,000  |     17,735  |     96,219  | |      67    |      86     |
    | M = 5,000  |    265,314  |    601,399  | |     557    |     212     |
    | M = 10,000 |  2,084,924  |  2,405,669  | |   2,441    |     423     |
    |------------+-------------+-------------+-+------------+-------------|

    </div>
</div>

|------------+-------------+-------------+-+------------+-------------|
|            | Elimination |             | | Two-pass   |             |
|------------|------------:|------------:|-|-----------:|------------:|
|            |  Time (sec) | Memory (MB) | | Time (sec) | Memory (MB) |
|------------+-------------+-------------+-+------------+-------------|
| M = 500    |        295  |      6,017  | |       3    |      23     |
| M = 1,000  |      2,318  |     24,055  | |      11    |      44     |
| M = 2,000  |     17,735  |     96,219  | |      67    |      86     |
| M = 5,000  |    265,314  |    601,399  | |     557    |     212     |
| M = 10,000 |  2,084,924  |  2,405,669  | |   2,441    |     423     |
|------------+-------------+-------------+-+------------+-------------|

<div class="caption">
    Benchmarking table in 'human' units for collections of size M. The performance gains are huge, especially for larger collections.
</div>




### Project contributions
#### What bits does this project reach that others don't?

- Potentially re-introduces the possibility of collaborative research in the spirit of {% cite White_2000 %}


### Areas of improvement
#### Things I'm not that happy about right now.

- Right now, this works for the R rule, it would be interesting to investigate whether similar updating algorithms also work for other equivalence rules (i.e. the max rule)
