---
layout: page
title: Post Date
permalink: /postdate/
---

<hr>
<div>
	{% for post in site.posts %}
		{% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
		{% if year != y %}
			{% assign year = y %}
			<a style="text-decoration: underline; background-color: rgb(210,210,210)" href="#{{ y }}" title="{{ y }}"> {{ y }} </a>
			&nbsp;
		{% endif %}
	{% endfor %}
</div>
<hr>

<ul class="listing">
{% for post in site.posts %}
  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
  {% if year != y %}
    {% assign year = y %}
    <li class="listing-seperator" id="{{ y }}">{{ y }}</li>
  {% endif %}
	<ul>
		<li class="listing-item">
			<time datetime="{{ post.date | date:"%Y-%m-%d" }}"> {{ post.date | date:"%Y-%m-%d" }} </time>
			<a href="{{ post.url }}" title="{{ post.title }}"> {{ post.title }} </a>
		</li>
	</ul>
{% endfor %}
</ul>