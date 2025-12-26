---
layout: page
title: 
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
		margin-right: 5px;
	}
</style>

<h1>Our Team</h1>

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



