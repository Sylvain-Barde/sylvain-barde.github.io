---
layout: page
title: Fast MCS
description: A fast Model Confidence Set algorithm
img: assets/img/benchmark_mcs.jpg
importance: 1
category: research
related_publications: true
pretty_table: true
---

### Table of contents
- [Overview](#overview)
- [Project contributions](#project-contributions)
- [Areas of improvement](#areas-of-improvement)

### Overview

Fast updating implementation of the Model Confidence Set (MCS) algorithm {% cite Hansen_et_al_2011 %}. Given a candidate collection of $$M$$ models, the elimination implementation has a $$\mathcal{O}(M^3)$$ time complexity and a $$\mathcal{O}(M^2)$$ memory requirement. The fastMCS updating implementation reduces this down to a $$\mathcal{O}(M^2)$$ time complexity and a $$\mathcal{O}(M)$$ memory requirement.

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

The practical implication of these improved scaling characteristics are illustrated by the following table. This extrapolate the benchmarking results obtained for the elimination MCS to larger collections. The last row indicates that establishing the MCS of a collection of 10,000 models would require 579 hours (~24 days) and require 2.4 TB of RAM in doing so. The fastMCS algorithm can achieve the same task in 40 minutes with 423 MB.

|            | **Elimination** |             | | **Two-pass**   |             |
|------------|----------------:|------------:|-|---------------:|------------:|
|            |    Time (sec)   | Memory (MB) | |   Time (sec)   | Memory (MB) |
| M = 500    |          295    |      6,017  | |         3      |      23     |
| M = 1,000  |        2,318    |     24,055  | |        11      |      44     |
| M = 2,000  |       17,735    |     96,219  | |        67      |      86     |
| M = 5,000  |      265,314    |    601,399  | |       557      |     212     |
| M = 10,000 |    2,084,924    |  2,405,669  | |     2,441      |     423     |

<div class="caption">
    Benchmarking performance in 'human' units for collections of size M. The performance gains are huge, especially for larger collections.
</div>

### Project contributions
#### What bits does this project reach that others don't?

- Well, clearly, the performance gains on large collections are valuable in themselves, as it unlocks types of large-scale forecasting evaluations that were not tractable before. Combine this with today's big data world and incentives to provide better forecasts (of financial volatility, of commodity prices, of the weather, etc.) and it is not hard to see potential benefits. Of course, most of the academic literature using the MCS tends to use small collections to test novel methods against a handful of benchmarks, in such cases the elimination MCS will be perfectly adequate.
- A second benefit, even for small comparisons, is that by updating the MCS as models are added, rather than shrinking the MCS as models are eliminated, allows for a comparison exercise to be updated *ex-post*. Suppose you have access to an HPC service and pay the cost involved in running an M=10,000 collection, as in the table above. 24 days later, you have your MCS. If at that point you realise that you forgot to include 100 models from an obscure corner of the forecasting literature, you have no choice than to re-run the whole thing. With fastMCS, you can just update your MCS with these 100 models at a fraction of the compute cost. This re-introduces the possibility of collaborative research in the spirit of {% cite White_2000 %}, where researchers post their model losses, bootstrap indices and MCS results (elimination statistics and P-values) so that subsequent researchers can build on them at a later date.


### Areas of improvement
#### Things I'm not that happy about right now.

- A first consideration, as mentioned above, is that most uses of the MCS have small collections (less than 10 models), where this performance improvement will not matter. So fastMCS might not necessarily displace the elimination approach in practice. I'm fine with that personally!
- Right now, this works for the 'R' (range) elimination rule only. I've not looked at the other rule proposed by {% cite Hansen_et_al_2011 %}, the 'max' rule, where candidates for elimination are selected based on their deviation from average performance in the collection. So this means that fastMCS is not currently as flexible as the elimination approach. I suspect that this is harder, as the average needs to be re-calculated in between iterations. It should be possible to re-calculate the average and the elimination statistics of existing models when a model is added, but whether the same can be done for the bootstrapped statistics is an open question. However, this is an interesting area for other research.
