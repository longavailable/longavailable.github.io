---
layout: post
title:  Add a search bar in Jekyll blogsite
author: Bruce Liu
# last update date
date:   2020-02-15 23:30:00 +0100
# first published date
date:   2020-02-15 23:30:00 +0100
categories: [post]
tags: [Jekyll, search, Lunr, Google Custom Search engine]
description: Hello, Jekyll!
header-image: 
permalink: /search_bar/
---

There are ways to add a search bar. This post shows my way.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# Lunr

- Add [Lunr.js] to your project.

- Add [search-lunr.html] to `_includes` of your project

- Add the following statement to your page

	```
{ % include search-lunr.html % }
	```

{% include search-lunr.html %}

# Google - invoke google.com

- Add [search-google.html] to `_includes` of your project

- Change the domain name with yours

- Add the following statement to your page

	```
{ % include search-google.html % }
	```

{% include search-google.html %}

# Google Custom Search Engine

- Create a new search engine for your site <https://cse.google.com/cse/create/new>.

- Add the following

	```html
<script async src="put your public url here"></script><div class="gcse-search"></div>
	```

<script async src="https://cse.google.com/cse.js?cx=013029827813215097911:1exidgxkr3n"></script>
<div class="gcse-search"></div>


<!-- a horizontal line -->

___
# Reference:
- [Search with Lunr.js](https://jekyllcodex.org/without-plugin/search-lunr/)
- [Search with Google](https://jekyllcodex.org/without-plugin/search-google/)
- [Google Custom Search engine](https://www.google.com/cse/)

[Lunr.js]: https://raw.githubusercontent.com/jhvanderschee/jekyllcodex/gh-pages/js/lunr.js
[search-lunr.html]: https://raw.githubusercontent.com/jhvanderschee/jekyllcodex/gh-pages/_includes/search-lunr.html
[search-google.html]: https://raw.githubusercontent.com/jhvanderschee/jekyllcodex/gh-pages/_includes/search-google.html

