---
layout: post
title: How to make Github Pages
categories: [Git, artical]
tags: [github, pages, how]
fullview: true
---



####Install Ruby
Generally speaking, the Mac OS will have installed Ruby by default.
To check, open Terminal and run command 'ruby --version'

####Install Bundler
{% highlight yaml %}
$ gem install bundler
{% endhighlight %}

####Install Jekyll
Create a file in repository called **'Gemfile'** and add *gem 'github-pages'*.

Before run the next line, check whether you have installed **'xcode-select'** or not.
If not, please install The command line tool for Xcode first by run 

{% highlight yaml %}
$ xcode-select --install
{% endhighlight %}


Run 

{% highlight yaml %}
$ bundle install
{% endhighlight %}


####Run Jekyll
Run 'bundle exec jekyll serve' in Terminal
Now, you can try to open http://localhost:4000/index.html to see your Github page.




###Ref:
http://cnfeat.com/2014/05/10/2014-05-11-how-to-build-a-blog/

https://help.github.com/articles/using-jekyll-with-pages/
