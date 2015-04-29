---
layout: post
title: Tips of Java
categories: [Java]
tags: [java, tips]
fullview: true
---

1. Java Math Library (Do not need to import)

		b = Math.sqrt(a);
	
2. How to keep several decimal places

		java.text.DecimalFormat decf = new java.text.DecimalFormat("#.##");   
		double d = 1.23456;   
		System.out.println(decf.format(d)); 
		
		
3. String to Double

		double d = Double.parseDouble(s);