---
layout: page
title: Tags
permalink: /tags/
---

<hr>
<div id='tag_cloud'>
	{% for tag in site.tags %}
	<a style="text-decoration: underline; background-color: rgb(210,210,210)" href="#{{ tag[0] }}" title="{{ tag[0] }}" rel="{{ tag[1].size }}">{{ tag[0] }}</a>
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

<script src="/js/jquery.tagcloud.js" type="text/javascript" charset="utf-8"></script> 
<script language="javascript">
	<div id="whatever">
	  <a href="/path" rel="7">peace</a>
	  <a href="/path" rel="3">unity</a>
	  <a href="/path" rel="10">love</a>
	  <a href="/path" rel="5">having fun</a>
	</div>
	$.fn.tagcloud.defaults = {
	  size: {start: 14, end: 18, unit: 'pt'},
	  color: {start: '#cde', end: '#f52'}
	};

	$(function () {
	  $('#whatever a').tagcloud();
	});
</script>