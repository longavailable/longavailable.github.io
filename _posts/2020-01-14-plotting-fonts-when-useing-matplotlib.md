---
layout: post
title:  Plotting fonts when using matplotlib
author: Bruce Liu
# last update date
date:   2020-01-14 11:20:00 +0100
# first published date
published: 2020-01-14 11:20:00 +0100
categories: [blog, python, plotting]
tags: [python, matplotlib, font]
header-image: 
permalink: /matplotlib_font/
---
When you want to use a font when plotting using matplotlib in python, it returns 'not found'. The answer maybe here.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# How to set different font when plotting with matplotlib in python?
- Set locally, for example set font for title: 
	```
	tfont = {'fontname':'Times New Roman'}
	plt.title('title',**tfont)
	```
- Set globally:
	```
	import matplotlib.pyplot as plt
	plt.rcParams['font.family'] = 'Times New Roman'
	```
If it works fine, that's ok. If it return something like the following:
	```
	findfont: Font family ['.....'] not found. Falling back to DejaVu Sans.
	```
Then continue.<br>

# Check first:

- Precautiously check matplotlib font cache or let it go:
	```
	cd ~/.cache/matplotlib && ls
	```
There may have a json file as the matplotlib font cache file. Check if the expected font exists. <br>
	- If the font exists, this is **NOT** for you and you can **STOP** here.
	- If not, continue.<br>	
- Check if the expected font exists in the system:
	```
	fc-list : family | sort
	```
or
	```
	fc-list -f '%{file}\n' | sort
	```
or
	```
	fc-list : lang=zh
	```
If needed, install [fontconfig](https://www.freedesktop.org/wiki/Software/fontconfig/) first.
	- If the font exists, go [here](#IFIL).
	- If not, go [here](#UFCIL).

# How to install a font in Linux {#IFIL}
- Require preferred font. **NOTICE** truetype format (.ttc/.ttf)
- Copy it to the fonts directory
	```
	cp <font path> /usr/share/fonts/<somewhere>
	```

# Update the font cache in Linux {#UFCIL}
- re-generate font cache:
	```
	sudo fc-cache -fv
	```
If needed, install [fontconfig](https://www.freedesktop.org/wiki/Software/fontconfig/) first.

# Remove current matplotlib font cache
- Precautiously backup first:
	```
	cp -r ~/.cache/matplotlib <somewhere>
	```
- Remove it:
	```
	rm -fr ~/.cache/matplotlib
	```

# Re-run the plotting script
Normally, the matplotlib font cache will re-generate automatically. That's it.

<br>
# Reference:
- [How to change fonts in matplotlib (python)?](https://stackoverflow.com/questions/21321670/how-to-change-fonts-in-matplotlib-python)
- [matplotlib.pyplot other parameters - Other keyword arguments](https://matplotlib.org/3.1.1/api/text_api.html#matplotlib.text.Text)
- [Won't use a font although it can be found by the FontManager](https://github.com/matplotlib/matplotlib/issues/3590)
- [Add custom fonts to Matplotlib](https://scentellegher.github.io/visualization/2018/05/02/custom-fonts-matplotlib.html)


