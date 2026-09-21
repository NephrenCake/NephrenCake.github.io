---
layout: default
permalink: /publications/
title: Publications
nav: true
nav_order: 2
---

<div class="publications">

<h2>Published Conference/Journal Papers</h2>

{% bibliography --group_by none --query @*[category=published] %}

<h2>Technical Reports</h2>

{% bibliography --group_by none --query @*[category=technical-report] %}

<h2>Unpublished High-Impact Papers</h2>

{% bibliography --group_by none --query @*[category=unpublished-high-impact] %}

</div>
