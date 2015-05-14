---
layout: post
title: How to build Github Pages by Hexo
categories: [Github]
tags: [Github, Pages, Hexo]
fullview: true
---
###1. Start (On Github)

1. Login your Github account
2. Create a new Repository
3. Name it as "yourGithubName.github.io" (exclude the quotation mark)
4. Click "Set up in Desktop" and pull it down to your computer


###2. Generate(On Local)


1. Open terminal 
2. Install node & npm
3. Install Nexo

		npm install -g hexo

4. Enter the directory where the github pages repository locates in.
5. Create hexo project in the github pages repository

		hexo init yourGithubName.github.io
		cd yourGithubName.github.io
		
6. Generate and run the server

		npm install
		hexo g
		hexo s
	
7. Then you can find your demo in localhost:4000


###3. Deploy

1. Stop the server

		Control + C

2. Open _config.yml to set the address of your github 

		deploy:
			type: git
			repo: git@github.com:yourGithubName/yourGithubName.github.io.git
			
3. Deploy

		npm install hexo-deployer-git --save
		hexo d
		
4. Then Hexo will upload your website demo to your Github automatically and then you can browse your Github pages "yourGithubName.github.io" in your browser.


###4. New pages

1. Write your article in Markdown and save it in source/_posts/
2. Generate your website again
		
		hexo g
		
3. After that, you can run "hexo s" to see the changes in local.
4. Deploy your website again and hexo will upload the changes to your Github automatically.

		hexo d
		
				




		