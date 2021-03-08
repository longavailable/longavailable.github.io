---
layout: post
title:  Debugging in Python
author: Bruce Liu
#last update date
date:   2021-03-08 16:20:00 +0800
#first published date
published: 2021-03-08 16:20:00 +0800
categories: [post]
tags: [Python, pdb, pudb]
description: 
header-image: 
permalink: /debugging-in-python/
---

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

## [pdb] - the Python Debugger

- Invoke **[pbd]** from terminal to debug the entire script.

    ```bash
python -m pdb mytest.py
    ```

- Insert `import pdb; pdb.set_trace()` in a specific line of the script.

- Insert `breakpoint()` in the script. The built-in [breakpoint()] is a equivalent way of `import pdb; pdb.set_trace()`.

- Commands: c(ontinue), s(tep), n(ext), r(eturn), j(ump), q(uit) .. [more](https://docs.python.org/3/library/pdb.html#debugger-commands).

## [PuDB] - a console-based visual debugger for Python

### Installing

Install [PuDB] by `pip install pudb` or `conda install -c conda-forge pudb`.

### Usage

Similar to [pdb],

- Debug the entire script with:

    ```bash
pudb mytest.py
    ```

    or

    ```bash
python -m pudb mytest.py
    ```

- Insert in a specific line with:

    ```python
from pudb import set_trace; set_trace()
    ```

    or

    ```python
import pudb; pu.db
    ```

- Integrate [pudb] with [breakpoint()] function. Add:

    ```bash
export PYTHONBREAKPOINT="pudb.set_trace"
    ```

    in your **.bashrc** or **.zshrc**. Then use `breakpoint()` in your script.

- Commands: tyep '?' in the console to check the conmand list.


## References

- [pdb — The Python Debugger](https://docs.python.org/3/library/pdb.html)
- [Getting Started: pudb 2020.1 dicumentation](https://documen.tician.de/pudb/starting.html)
- [Python 3.7’s new builtin breakpoint — a quick tour](https://hackernoon.com/python-3-7s-new-builtin-breakpoint-a-quick-tour-4f1aebc444c)

<!--links-->
[pdb]: https://docs.python.org/3/library/pdb.html
[breakpoint()]: https://docs.python.org/3/library/functions.html#breakpoint
[PuDB]: https://documen.tician.de/pudb/index.html

