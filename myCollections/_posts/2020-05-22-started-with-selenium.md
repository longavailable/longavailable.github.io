---
layout: post
title:  Get started with Selenium
author: Bruce Liu
# last update date
date:   2020-05-24 02:25:00 +0200
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

Further more, there are some nice tools such as [webdriver-manager](https://pypi.org/project/webdriver-manager/), [chromedriver-autoinstaller](https://pypi.org/project/chromedriver-autoinstaller/) and [geckodriver-autoinstaller](https://pypi.org/project/geckodriver-autoinstaller/) to check, download and install a suitable driver from python automatically.

Although WSL doesn't support GUI directly, there are still ways to use WebDrivers/Selenium. Here is a proven method. [https://github.com/lackovic/notes/tree/master/Windows/Windows%20Subsystem%20for%20Linux#use-chromedriver-on-wsl](https://github.com/lackovic/notes/tree/master/Windows/Windows%20Subsystem%20for%20Linux#use-chromedriver-on-wsl). In short, just place [ChromeDriver](https://chromedriver.chromium.org/) in some system directory in windows for example **C:\Windows\System32**, and remove **.exe** extension. After that, your can use from wsl directly.

# Common usages

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys #provide special keys in the keywords
from webdriver_manager.chrome import ChromeDriverManager

#check ChromeDriver and open a new Chrome browser
browser = webdriver.Chrome(ChromeDriverManager().install())

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

# ChromeOptions

`selenium.webdriver.ChromeOptions()` is equivalent to `selenium.webdriver.chrome.options.Options()`.

```python
#open a new ChromeOptions object
options = webdriver.ChromeOptions()

#add agruments
options.add_argument('--headless')
options.add_argument('--disable-gpu')

#open a new Chrome browser
driver = Chrome(options=options)
```

Further more arguments for Chrome, go after [here](https://peter.sh/experiments/chromium-command-line-switches/).

# XPath

There is a fantastic blog to guide the usage of XPath. Click [here](https://www.guru99.com/xpath-selenium.html)

And you can test a XPath in Chrome Console. F12 --> Console --> Type your XPath like `$x(“.//*[@id='id']”)` --> ENTER.

<div align="center"><img width="365" height="205" src="/assets/pics/xpath-console.png"/></div>

# Cases

- submit the daily report to server, see [source code](https://github.com/longavailable/practices/blob/master/python/selenium/001daily_report_selenium.py).

- require **cookies** from Google Earth Engine, see [source code](https://github.com/longavailable/practices/blob/master/python/selenium/002gee_cookies_selenium.py).


# Reference
- [Selenium](https://www.selenium.dev/)
- [Selenium - github](https://github.com/SeleniumHQ/selenium)
- [Selenium python API](https://www.selenium.dev/selenium/docs/api/py/index.html)
- [List of Chromium Command Line Switches](https://peter.sh/experiments/chromium-command-line-switches/)
- [XPath in Selenium WebDriver: Complete Tutorial](https://www.guru99.com/xpath-selenium.html)
