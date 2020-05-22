---
layout: post
title:  Get started with Selenium
author: Bruce Liu
# last update date
date:   2020-05-23 00:50:00 +0200
# first published date
published: 2020-05-23 00:50:00 +0200
categories: [post]
tags: [selenium, webdriver, python, chrome, wsl]
description: 
header-image: 
permalink: /selenium_guide/
---
There are ways to access a web page in python, such as [requests](https://requests.readthedocs.io/en/latest/), [mechanize](https://mechanize.readthedocs.io/en/latest/), [urllib](https://docs.python.org/3/library/urllib.request.html) and Selenium. This post will give a simple introduction to Selenium.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# Prerequisites

- A browser is a must. One of Chrome, Firefox, Edge, Safari, Opera, IE, etc.

- Driver for your browser.

	- [ChromeDriver](https://chromedriver.chromium.org/)
	
	- [geckodriver](https://github.com/mozilla/geckodriver) for Firefox
	
	- and ...

Further more, there are [chromedriver-autoinstaller](https://pypi.org/project/chromedriver-autoinstaller/) and [geckodriver-autoinstaller](https://pypi.org/project/geckodriver-autoinstaller/) to download and install a suitable driver from python.

Although WSL doesn't support GUI directly, there are still ways to use WebDrivers/Selenium. Here is a proven method. [https://github.com/lackovic/notes/tree/master/Windows/Windows%20Subsystem%20for%20Linux#use-chromedriver-on-wsl](https://github.com/lackovic/notes/tree/master/Windows/Windows%20Subsystem%20for%20Linux#use-chromedriver-on-wsl). In short, just place [ChromeDriver](https://chromedriver.chromium.org/) in some system directory in windows for example **C:\Windows\System32**, and remove **.exe** extension. After that, your can use from wsl directly.

# Common usages

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys #provide special keys in the keywords

#open a new Chrome browser
browser = webdriver.Chrome()

#load Yahoo homepage
browser.get('http://www.yahoo.com')
assert 'Yahoo' in browser.title

#find the search box
elem = browser.find_element_by_name('p')

#input 'seleniumhq' and type 'ENTER'
elem.send_keys('seleniumhq' + Keys.RETURN)
#elem.send_keys('seleniumhq')
#elem.send_keys(Keys.RETURN)

#close the browser
browser.quit()
```

Notes! There is a list of chromium command line arguments and a very nice guide of XPath in references.

A case test is to submit the daily report to server automatically, see [source code](https://github.com/longavailable/practices/blob/master/python/selenium/001selenium.py).

# Reference
- [Selenium](https://www.selenium.dev/)
- [Selenium - github](https://github.com/SeleniumHQ/selenium)
- [Selenium python API](https://www.selenium.dev/selenium/docs/api/py/index.html)
- [List of Chromium Command Line Switches](https://peter.sh/experiments/chromium-command-line-switches/)
- [XPath in Selenium WebDriver: Complete Tutorial](https://www.guru99.com/xpath-selenium.html)
