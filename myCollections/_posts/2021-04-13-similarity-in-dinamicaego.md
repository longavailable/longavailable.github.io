---
layout: post
title:  Comparison of three functors on similarity in DinamicaEGO
author: Bruce Liu
#last update date
date:   2021-04-13 15:50:00 +0800
#first published date
published: 2021-04-13 15:50:00 +0800
categories: [post]
tags: [DinamicaEGO, similarity, land use change]
description: 
header-image: 
permalink: /similarity-dinamicaego/
---

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

| functor | inputs | outputs | Window size | Decay function |
| ---------------------------|----------------------------|-----|
| [Calc Reciprocal Similarity Map] | First map or simulated map, | Two reciprocal similarity maps, | Single window | Constant or exponential |
| ^^ | ^^ second map or observed map | ^^ mean similarities of similarity map | ^^ | ^^ |
| [Calc Similarity of Differences] | Initial map, | Minimun similarity map of two reciprocal similarity maps, | Single window | Constant or exponential |
| ^^ | ^^ simulated map, | ^^ minimum of mean similarities of two reciprocal similarity maps [**] | ^^ | ^^ |
| ^^ | ^^ observed map | ^^ | ^^ | ^^ |
| [Calc Multi Window Similarity of Differences] | Initial map, | Minimun of mean similarities of two reciprocal similarity maps [**], | Multi windows | Constant |
| ^^ | ^^ simulated map, | ^^ maximum of mean similarities of two reciprocal similarity maps | ^^ | ^^ |
| ^^ | ^^ observed map | ^^ | ^^ | ^^ |

Note that the items of [**] would return same result for a specific window size.

<!--links-->
[Calc Reciprocal Similarity Map]: http://www.csr.ufmg.br/dinamica/dokuwiki/doku.php?id=calc_reciprocal_similarity_map
[Calc Similarity of Differences]: https://www.csr.ufmg.br/dinamica/dokuwiki/doku.php?id=calc_similarity_of_differences
[Calc Multi Window Similarity of Differences]: https://www.csr.ufmg.br/dinamica/dokuwiki/doku.php?id=calc_multi_window_similarity_of_differences
