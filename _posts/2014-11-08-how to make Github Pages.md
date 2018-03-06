---
layout: post
title: How to make Github Pages
categories: [Git, artical]
tags: [github, pages, how]
fullview: true
---



#### Install Ruby
Generally speaking, the Mac OS will have installed Ruby by default.
To check, open Terminal and run command 'ruby --version'
	
  <br />	
  
#### Install Bundler

	$ gem install bundler
	
  <br />	
  
#### Install Jekyll
Create a file in repository called **'Gemfile'** and add *gem 'github-pages'*.

Before run the next line, check whether you have installed **'xcode-select'** or not.
If not, please install The command line tool for Xcode first by run 


	$ xcode-select --install

Run 

	$ bundle install

	
  <br />	
  
#### Run Jekyll
Run 'bundle exec jekyll serve' in Terminal
Now, you can try to open 

	http://localhost:4000/index.html 
	
to see your Github page.
	
  <br />	
  
#### Choose Theme
See here:

**[Jekyll Theme](http://jekyllthemes.org/)**

Fork the theme you like, unzip it and copy them to your repository folder.

	
  <br />	
  
#### Ref:
1. [一步步在GitHub上创建博客主页](http://www.pchou.info/web-build/2014/07/04/build-github-blog-page-08.html)

2. [Using Jekyll with Pages](
https://help.github.com/articles/using-jekyll-with-pages/)

3. [用Github Pages建独立博客](http://beiyuu.com/github-pages/)

4. [如何搭建一个独立博客——简明Github Pages与Hexo教程](
http://cnfeat.com/2014/05/10/2014-05-11-how-to-build-a-blog/)

