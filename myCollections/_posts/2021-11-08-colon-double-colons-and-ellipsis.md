---
layout: post
title:  Colon, double colon and ellipsis
author: Bruce Liu
#last update date
date:   2021-11-08 15:50:00 +0800
#first published date
published:  2021-11-08 15:50:00 +0800
categories: [post]
tags: [python]
description: 
header-image: 
permalink: /colon-ellipsis/
---

Experiences of slicing operation `:`, `::`, and `...`.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# List

```Python
a = list(range(10))
a[:]
a[::]
a[...]
```

`a[:]` is equivalent to `a[::]`. `a[...]` was not working.

# numpy.array

```Python
import numpy as np

a = np.arange(10)
a[:]
a[::]
a[...]
```

`a[:]`, `a[::]`, and `a[...]` are equivalent for a numpy.array object. For `s[start:end:step]` operation, the default value of start, end, and step is 0, -1, and 1 separately. 

<!--links-->
[The Ellipsis Object]: https://docs.python.org/3/library/stdtypes.html#the-ellipsis-object
[Sequence Types — list, tuple, range]: https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range
