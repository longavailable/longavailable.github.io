---
layout: post
title:  Execute Javascript code in Python
author: Bruce Liu
#last update date
date:   2023-02-15 10:00:00 +0800
#first published date
published: 2023-02-15 10:00:00 +0800
categories: [post]
tags: [Python, Javascript]
description: 
header-image: 
permalink: /execute-javascript-in-python/
---

Python packages and implementation ways to execute JavaScript code in Python.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

## Python packages

### [Js2Py]


### [PyExecJS] - unmaintained.

## Ways to implement

Firstly, install [Js2Py] then import js2py module:

    ```python
import js2py
    ```

### js code in place

    ```python
js_code = '''
function add(a, b) {
  return a + b;
}
'''
add = js2py.eval_js(js_code)
add(1,2) + 3
    ```

### js code in a file

Create a js file nameed with `add.js`:

    ```javascript
function add(a, b) {
  return a + b;
}
    ```

Then,

    ```python
with open('add.js') as f:
	add = js2py.eval_js(f.read())
add(1,2) + 3
    ```

### online js code

There is a public link for the `add` function

<https://raw.githubusercontent.com/longavailable/datarepo02/main/code/javascript/add.js>

    ```python
import requests
js_link = 'https://raw.githubusercontent.com/longavailable/datarepo02/main/code/javascript/add.js'
add = js2py.eval_js(requests.get(js_link).text)
add(1,2) + 3
    ```

<!--links-->
[Js2Py]: https://github.com/PiotrDabkowski/Js2Py
[PyExecJS]: https://github.com/doloopwhile/PyExecJS

