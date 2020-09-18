---
layout: post
title:  Setup font size and other groups in matplotlib
author: Bruce Liu
# last update date
date:   2020-09-18 08:00:00 +0200
# first published date
published: 2020-09-18 08:00:00 +0200
categories: [post]
tags: [python, matplotlib, font]
header-image: 
permalink: /matplotlib-font-setup/
---
How to control the font size in your graph. By changing 'rcParams' globally. It also works for other rc groups.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

There are 3 equivalent ways to setup ***rc*** file.

## [matplotlib.pyplot.rc]

```python
import matplotlib.pyplot as plt
plt.rc('lines', linewidth=2, color='r')
```

## [matplotlib.rc]

```python
import matplotlib as mpl
mpl.rc('lines', linewidth=2, color='r')
```

## [matplotlib.rcParams]

```python
import matplotlib as mpl
mpl.rcParams['lines.linewidth'] = 2
mpl.rcParams['lines.color'] = 'r'
```

# setup font size

```python
import matplotlib.pyplot as plt
sfs, mfs, lfs = 8, 10, 12
plt.rc('font', size=sfs)
plt.rc('axes', titlesize=sfs, labelsize=mfs)
plt.rc('xtick', labelsize=sfs)
plt.rc('ytick', labelsize=sfs)
plt.rc('legend', fontsize=sfs)
plt.rc('figure', titlesize=lfs)
```

# my custom style

```python
import matplotlib.pyplot as plt
sfs, mfs, lfs = 8, 10, 12	#in points
plt.rc('figure', figsize=[7, 4], titlesize=lfs)	#width, height in inches
plt.rc('savefig', dpi=300)
plt.rc('lines', linewidth=1.0, markersize=5.0) #in points
plt.rc('font', family='Times New Roman', size=sfs)
plt.rc('axes', titlesize=sfs, labelsize=mfs)
plt.rc('xtick', labelsize=sfs)
plt.rc('ytick', labelsize=sfs)
plt.rc('legend', fontsize=sfs)
plt.rc('figure', titlesize=lfs)
```

<br>
# Reference:
- [How to change the font size on a matplotlib plot](https://stackoverflow.com/a/39566040/12371819)
- [matplotlib.pyplot.rc]
- [matplotlib.rc]
- [matplotlib.rcParams]

[matplotlib.pyplot.rc]: https://matplotlib.org/api/_as_gen/matplotlib.pyplot.rc.html?highlight=pyplot%20rc#matplotlib.pyplot.rc
[matplotlib.rc]: https://matplotlib.org/3.3.1/api/matplotlib_configuration_api.html?highlight=matplotlib%20rc#matplotlib.rc
[matplotlib.rcParams]: https://matplotlib.org/3.3.1/api/matplotlib_configuration_api.html?highlight=matplotlib%20rc#matplotlib.rcParams


