---
layout: page
permalink: /publications/
title: publications
description: Here are my main publications
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

<!-- Bibsearch Feature -->

{% include bib_search.liquid %}

<div class="publications">

{% bibliography --query @*[mine=true] %}

</div>