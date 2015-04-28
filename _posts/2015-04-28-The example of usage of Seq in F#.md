---
layout: post
title: The example of usage of Seq in F#
categories: [F#]
tags: [F#, Seq, example]
fullview: true
---
The following code demonstrates the use of Seq.Function

##Seq.map

	let a = seq{for i in 0..4 do yield i}
	Seq.map (fun value -> value * value) a
	
###output
	
	val it : seq<int> = seq [0; 1; 4; 9; 16]
	

##Seq.mapi

	let a = seq{for i in 0..4 do yield i}
	Seq.map (fun index value -> (index, value * value)) a
	
###output
	
	val it : seq<int> = seq [(0,0); (1,1); (2,4); (3,9); (4,16)]
		

##Seq.mapi

	let a = seq{for i in 0..4 do yield i}
	Seq.map (fun index value -> (index, value * value)) a
	
###output
	
	val it : seq<int> = seq [(0,0); (1,1); (2,4); (3,9); (4,16)]
		
		
		
##Summary
Function	|Return	|Comments
----|------|----
Seq.choose( fun x -> if .. Then Some()) else None()) Seq	|Seq	|函数应用于每个元素，使用some和none|
Seq.collect( Function ) Seq	|Seq	|函数应用于每个元素，多用于生成新Seq|
Seq.map	|Seq	|函数应用于每个元素|
Seq.iter( Function ) Seq	|None	|函数应用于每个元素|
Seq.iteri(fun i x -> …) Seq	|None	|函数应用于每个元素|
Seq.sum()	|Value	|计算Seq元素和
Seq.sumBy()	|Value	|计算Seq元素在应用函数之后的和
Seq.fold()	|Value	|函数应用于每个元素，并使用一个累加器
Seq.unfold()|Seq	|函数应用与每个元素，并使用一个累加器
