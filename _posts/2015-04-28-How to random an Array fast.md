---
layout: post
title: How to random an Array fast
categories: [fsharp]
tags: [fsharp, random, array]
fullview: true
---
###Step
1. Pick up a random integer j in range [0,n-1]
2. Swap a[j] and a[n-1]
3. Then pick up a random integer j in range [0,n-2]
4. Swap a[j] and a[n-2]
5. ...
6. Swap a[j] and a[1]


###Code

	let a = [|0; 1; 2; 3; 4; 5; 6; 7; 8; 9|]
	let rd = Random()
	for i = 9 downto 1 do
    	let j = int (rd.NextDouble() * (float i))
    	printfn "%d" j
    	let t = a.[i]
    	a.[i] <- a.[j]
    	a.[j] <- t
	printfn "%A" a