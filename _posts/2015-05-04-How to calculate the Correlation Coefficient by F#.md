---
layout: post
title: How to calculate the Correlation Coefficient by F#
categories: [Fsharp]
tags: [Fsharp, Correlation Coefficient]
fullview: true
---
###Formula
![](/images/CorrelationCoefficient.GIF)


###Code
	let CorrelationCoefficient x y = 
	    let mul (x:float[]) (y:float[]) 
	        = Array.mapi (fun i z -> z * y.[i]) x
	    let xy = mul x y
	    let xx = mul x x
	    let yy = mul y y
	    let n = float x.Length
	    let numerator = (Array.sum xy - Array.sum x * Array.sum y / n)
    	let denominator = sqrt((Array.sum xx - Array.sum x * Array.sum x/n) * (Array.sum yy - Array.sum y * Array.sum y/n))
    	numerator / denominator


	let x = [|6.9; 6.7; 6.9; 5.8; 6.8|]
	let y = [|3.1; 3.1; 3.1; 2.7; 3.2|]
	let ans = CorrelationCoefficient x y