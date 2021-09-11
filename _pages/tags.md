---
layout: page
title: Tags
permalink: /tags/
---

<hr>
<div>
	{% for tag in site.tags %}
		<a style="text-decoration: underline; background-color: rgb(210,210,210)" href="#{{ tag[0] }}" title="{{ tag[0] }}" rel="{{ tag[1].size }}">{{ tag[0] }}</a>
		&nbsp;
	{% endfor %}
</div>
<hr>

<ul class="listing">
	{% for tag in site.tags %}
		<li class="listing-seperator" id="{{ tag[0] }}">{{ tag[0] }}</li>
		<ul>
			{% for post in tag[1] %}
				<li class="listing-item">
					<time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
					<a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
				</li>
			{% endfor %}
		</ul>
	{% endfor %}
</ul>

<!-- back to top button -->
<script src="/js/vanilla-back-to-top.min.js"></script>
<script>addBackToTop()</script>