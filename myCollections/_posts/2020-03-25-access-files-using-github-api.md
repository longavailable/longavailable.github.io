---
layout: post
title:  Access files using github api
author: Bruce Liu
# last update date
date:   2020-03-26 16:54:00 +0200
# first published date
published: 2020-03-26 16:54:00 +0200
categories: [post]
tags: [github, python, PyGithub, GitHub REST API v3]
description: 
header-image: 
permalink: /githubapi/
---
Upload a file to github repository, and request it. Yes, it is normal. This blog make it more smoothly.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# Create, update and delete a file

You can do all of them via [Contents API](https://developer.github.com/v3/repos/contents).

- `get_contents` in [API v3](https://developer.github.com/v3/repos/contents/#get-contents), [PyGithub](https://pygithub.readthedocs.io/en/latest/github_objects/Repository.html#github.Repository.Repository.get_contents)
	
	Python script as follows:
	
	```python
from github import Github
g = Github().get_user()
g.get_repo(repoName).get_contents(filePath)
	```
	
	Here the filePath can be a path for file or directory. For a file, it will has its encoded content with `encoding` and `content` keywords. For a directory, it will return a list-like object contents all infomations of the files or subdirectories except content.
	
	Responce examples of GitHub API v3:
	
	The root directory of [cscbank](http://longlovemyu.tk/cscbank/): [https://api.github.com/repos/longavailable/cscbank/contents](https://api.github.com/repos/longavailable/cscbank/contents).
	
	`README.md` of [cscbank](http://longlovemyu.tk/cscbank/): [https://api.github.com/repos/longavailable/cscbank/contents/README.md](https://api.github.com/repos/longavailable/cscbank/contents/README.md).

	Important❗

	- It can be used for a directory and a file.
	
	- This API has an upper limit of 1,000 files for a **directory**. If you need to retrieve more files, use the [Git Trees API](https://developer.github.com/v3/git/trees).
	
	- This API supports **files** up to 1 megabyte in size.
	
	- `type` for a directory is **dir**, and for a file is **file**.
	
	Suggestion:
	
	If you do **NOT** want to access content of a file, then donot get_contents for a file. That is, `content` is the special of this way. In addition, 1MB seems a little small. My idea is using `get_contents` for a directory to request `sha` and `download_url` keywords, then use `requests.get()`. [Git Blobs API](https://developer.github.com/v3/git/blobs/) is another solution.
	
- `create_file` in [API v3](https://developer.github.com/v3/repos/contents/#create-or-update-a-file), [PyGithub](https://pygithub.readthedocs.io/en/latest/github_objects/Repository.html#github.Repository.Repository.create_file)
	
	Python script as follows:

	```python
g.get_repo(repoName).create_file(path=file,message= 'update '+file,content= dataBase64)
	```
	
- `update_file` in [API v3](https://developer.github.com/v3/repos/contents/#create-or-update-a-file), [PyGithub](https://pygithub.readthedocs.io/en/latest/github_objects/Repository.html#github.Repository.Repository.update_file)

	Python script as follows:

	```python
g.get_repo(repoName).update_file(path=file,message= 'update '+file,content= dataBase64,sha=sha)
	```
	
	Notice: `update_file` need `sha` parameter, you have to request `sha` before use it.

# [Git Trees API](https://developer.github.com/v3/git/trees) and [Git Blobs API](https://developer.github.com/v3/git/blobs/)

- get a tree in [API v3](https://developer.github.com/v3/git/trees/#get-a-tree), [PyGithub](https://pygithub.readthedocs.io/en/latest/github_objects/Repository.html#github.Repository.Repository.get_git_tree)

	If a directory has more than 1,000 files or you want to get the content of a over-1MB-while-below-100MB file directly using [Git Blobs API](https://developer.github.com/v3/git/blobs/).

	Responce examples of GitHub API v3:
		
	The root tree/directory of [cscbank](http://longlovemyu.tk/cscbank/): [https://api.github.com/repos/longavailable/cscbank/git/trees/master](https://api.github.com/repos/longavailable/cscbank/git/trees/master).

	Subtree/subdirectory `nl/delft` of [cscbank](http://longlovemyu.tk/cscbank/): [https://api.github.com/repos/longavailable/cscbank/git/trees/master:nl/delft](https://api.github.com/repos/longavailable/cscbank/git/trees/master:nl/delft).
	
	Notices:
	
	- `sha` is needed to use `get_git_tree` using PyGithub. Actually, treePath/directory likes `master:nl/delft` works as well.
	
	- `type` for a directory is **tree**, and for a file is **blob**.
	
- get a blob in [API v3](https://developer.github.com/v3/git/blobs/#get-a-blob), [PyGithub](https://pygithub.readthedocs.io/en/latest/github_objects/Repository.html#github.Repository.Repository.get_git_blob)

	Notices:
	
	- `sha` is needed to use `get_git_blob` using PyGithub.
	
	- This API supports blobs/files up to 100 megabytes in size.


# Reference
- [GitHub API v3](https://developer.github.com/v3/)
- [PyGithub](https://pygithub.readthedocs.io/en/latest/introduction.html)
