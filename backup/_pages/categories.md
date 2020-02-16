---
layout: page
title: "Categories"
# description:
permalink: /categories/
---

<hr>
<div>
	{% for category in site.categories %}
		<a style="text-decoration: underline; background-color: rgb(210,210,210)" href="#{{ category[0] }}" title="{{ category[0] }}" rel="{{ category[1].size }}"> {{ category[0] }} </a>
		&nbsp;
	{% endfor %}
</div>
<hr>

<ul class="listing">
	{% for category in site.categories %}
	<li class="listing-seperator" id="{{ category[0] }}">{{ category[0] }}</li>
	<ul>
		{% for post in category[1] %}
			<li><a href="{{ post.url }}">{{ post.title }}</a></li>
		{% endfor %}
	</ul>
	{% endfor %}
</ul>