---
layout: page
title: Publications
permalink: /publications/
---

<div class="list-group">
	{% for publication in site.publications reversed %}	<!--order by date and default "reversed"-->
	<div class="list-group-item">
	
		<!-- title -->
		<a href="{{ publication.url }}">
			<h4 class="list-group-item-heading">{{ publication.title }}</h4>
		</a>
		
		<!-- date and journal -->
		<p>
			<font size="3" color="#0000ee"><i>{{publication.journal}}</i> &nbsp; </font>
			{% if publication.published %}
				<font size="3" color="#0000ee">{{ publication.published | date: '%B %d %Y' }}</font>
			{% else %}
				<font size="3" color="#0000ee">{{ publication.date | date: '%B %d %Y' }}</font>
			{% endif %}
		</p>
		
		<!-- excerpt -->
		<p>{{ publication.excerpt | strip_html}} <a href="{{ publication.url }}"> 🔗 Read more...</a></p>
	</div>
	{% endfor %}
</div>