---
layout: page
title: "Categories"
# description:
permalink: /categories/
---

<hr>
<div>
	<!-- post -->
	{% for category in site.categories %}
		<a style="text-decoration: underline; background-color: rgb(210,210,210)" href="#{{ category[0] }}" title="{{ category[0] }}" rel="{{ category[1].size }}"> {{ category[0] }} </a>
		&nbsp;
	{% endfor %}
	
	<!-- publication -->
	<a style="text-decoration: underline; background-color: rgb(210,210,210)" href="#category_publication" title="publication"> publication </a>
		&nbsp;
</div>
<hr>

<ul class="listing">
	<!-- post -->
	{% for category in site.categories %}
	<li class="listing-seperator" id="{{ category[0] }}">{{ category[0] }}</li>
	<ul>
		{% for post in category[1] %}
			<li><a href="{{ post.url }}">{{ post.title }}</a></li>
		{% endfor %}
	</ul>
	{% endfor %}
	
	<!-- for publication -->
	<li class="listing-seperator" id="category_publication"> publication </li>
	<ul>
		{% for publication in site.publications %}
			<li><a href="{{ publication.url }}">{{ publication.title }}</a></li>
		{% endfor %}
	</ul>
</ul>

<!-- back to top button -->
<script src="/js/vanilla-back-to-top.min.js"></script>
<script>addBackToTop()</script>