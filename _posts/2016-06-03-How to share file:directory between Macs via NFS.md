---
layout: post
title: How to share file/directory between Macs via NFS
categories: [Network]
tags: [Network, OS, NFS]
fullview: true
---

###Steps
Let's say that we have Mac1 and Mac2. The Mac2 will be the NFS server and the Mac1 will be the client.

The first step is making the Mac2 as a NFS Server.

1. sudo vim /etc/exports 
2. Add the full path of the directory you want to share, one on its own line. 
	
	"\Users\Mac2\Sharing"
	
   where we put our test file -- "LargeTestfile". (Here, you can add "-alldirs" if you want to share all the directories under this directory.) 
	
3. sudo nfsd enable 
   
   it's better to disable it first if it was already enabled.)


Secondly, we need to mount the directory shared by Mac2 on Mac1.


1. make a directory on Mac1 used to map the corresponding share directory in Mac2
	
	mkdir "\Users\Mac1\FromSharing" 

2. mount the directory on Mac1

	sudo mount -o rsize=32768,wsize=32768,intr,noatime -t nfs IPofMac2:/Users/Mac2/Sharing /Users/Mac1/FromSharing


After those, we could asscess the file shared by Mac2 through the mounted directory "\Users\Mac1\FromSharing\"      

###Reference
1. [How to Share Directories over NFS with Mac OS X](http://www.behanna.org/osx/nfs/howto1.html)

2. [How to create an NFS share on MAC OS X (Snow Leopard) and mount (automatically during startup) from another MAC](https://community.spiceworks.com/how_to/61136-how-to-create-an-nfs-share-on-mac-os-x-snow-leopard-and-mount-automatically-during-startup-from-another-mac)