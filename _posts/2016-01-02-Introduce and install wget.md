---
layout: post
title: Introduce and install wget
categories: [Mac]
tags: [Mac, wget]
fullview: true
---
###Introduction
GNU Wget is used to retrieves content from web servers.

* Command line only
* Part of the GNU project
* Supports only GnuTLS or OpenSSL for SSL/TLS support
* No SOCKS support

###Install

#### 1. Download
{% highlight Bash shell scripts %}

	curl -O http://ftp.gnu.org/gnu/wget/wget-1.15.tar.gz
	
#### 2. Extract and Enter
{% highlight Bash shell scripts %}

	tar -zxvf wget-1.15.tar.gz
	
	cd wget-1.15/
{% endhighlight %}		
	
#### 3. Configure
{% highlight Bash shell scripts %}

	./configure --with-ssl=openssl
{% endhighlight %}		
#### 4. Install
{% highlight Bash shell scripts %}

	make

	sudo make install		
{% endhighlight %}	

###Reference
1. [Install and Configure wget on OS X Yosemite 10.10 and fix SSL GNUTLS error](http://coolestguidesontheplanet.com/install-and-configure-wget-on-os-x/)

2. [curl vs Wget](http://daniel.haxx.se/docs/curl-vs-wget.html)