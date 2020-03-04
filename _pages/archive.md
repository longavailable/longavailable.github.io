---
layout: page
title: "Archive"
# description:
permalink: /archive/
---

Archived by [Post Date](#TIME), [Categories](#CATEGORIES) and [Tags](#TAGS).

Archived by:
- [Post Date](/postdate)
- [Categories](/categories)
- [Tags](/tags)

# Post Date {#TIME}

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

# Categories {#CATEGORIES}

<hr>
<div>
	<!-- post -->
	{% for category in site.categories %}
		<a style="text-decoration: underline; background-color: rgb(210,210,210)" href="#{{ category[0] }}" title="{{ category[0] }}" rel="{{ category[1].size }}"> {{ category[0] }} </a>
		&nbsp;
	{% endfor %}
	
	<!-- publication -->
	<a style="text-decoration: underline; background-color: rgb(210,210,210)" href="#category_publication" title="Publication"> Publication </a>
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
	<li class="listing-seperator" id="category_publication"> Publication </li>
	<ul>
		{% for publication in site.publications %}
			<li><a href="{{ publication.url }}">{{ publication.title }}</a></li>
		{% endfor %}
	</ul>
</ul>

# Tags {#TAGS}

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