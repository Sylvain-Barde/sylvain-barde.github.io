---
layout: page
permalink: /publications/
title: publications
description: Here are my main publications
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

- [Working papers](#working-papers)
- [Peer-reviewed papers](#peer-reviewed-papers)

<!-- Bibsearch Feature -->

{% include bib_search.liquid %}

* * *

#### Working papers

<div class="publications">

{% bibliography --query @*[wp=true] %}

</div>

 * * *

#### Peer-reviewed papers

<div class="publications">

{% bibliography --query @*[mine=true] %}

</div>
