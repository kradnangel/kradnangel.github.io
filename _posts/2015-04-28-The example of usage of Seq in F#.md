---
layout: post
title: The example of usage of Seq in F#
categories: [F#]
tags: [F#, Seq, example]
fullview: true
---
##Seq.map

	let a = seq{for i in 0..4 do yield i}
	Seq.map (fun value -> value * value) a
	
###output
	
	val it : seq<int> = seq [0; 1; 4; 9; 16]
	