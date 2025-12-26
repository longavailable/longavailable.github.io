---
layout: page
title: Team
permalink: /team/
---

<style>
  .team-member {
    display: flex;
    align-items: flex-start;
    gap: 15px;
    margin-bottom: 25px;
}

  .team-member img.avatar {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    flex-shrink: 0;
}

  .team-text {
    line-height: 1.5;
}

  .team-links img {
    vertical-align: middle;
    margin-right: 2px;
}
</style>

<!--
Carefuly using spaces in Liquid lines
0 spaces → treated as raw HTML / Liquid
1–3 spaces → treated as part of a paragraph
4 spaces → treated as a code block
-->

{% for member in site.data.team %} 
  {% include team-member.html 
    name=member.name 
    photo=member.photo 
    title=member.title 
    description=member.description 
    links=member.links 
  %} 
{% endfor %}

<!-- back to top button -->
<script src="/js/vanilla-back-to-top.min.js"></script>
<script>addBackToTop()</script>



