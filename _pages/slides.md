---
layout: page
title: Slides
permalink: /slides/
---

<div class="list-group">
	{% for slide in site.slides reversed %}	<!--order by date and default "reversed"-->
	<div class="list-group-item">
	
		<!-- title -->
		<a href="{{ slide.url }}">
			<h4 class="list-group-item-heading">{{ slide.title }}</h4>
		</a>
		
		<!-- author and date -->
		<p>
			🧑 
			<font size="3" color="#0000ee"><i>{{ slide.author }}</i> &nbsp; </font>
			📅 
			{% if slide.published %}
				<font size="3" color="#0000ee">{{ slide.published | date: '%B %d %Y' }}</font>
			{% else %}
				<font size="3" color="#0000ee">{{ slide.date | date: '%B %d %Y' }}</font>
			{% endif %}
		</p>
				
		<!-- tags -->
		<div class="tags"><div class="spacing-2x"><p>
			🏷️ Keywords:
			{% for tag in slide.tags %}
				<a class="tag" href="/tags/#{{ tag }}" title="{{tag}}">{{tag}}</a>
				{% if tag != slide.tags.last %},{% endif %}	<!-- split with ',' -->
			{% endfor %}
		</p></div></div>
		
		<!-- excerpt -->
		<p>{{ slide.excerpt | strip_html}} <a href="{{ slide.url }}"> ▶️ Show now</a></p>
	</div>
	{% endfor %}
</div>

<!-- back to top button -->
<script src="/js/vanilla-back-to-top.min.js"></script>
<script>addBackToTop()</script>