---
layout: post
title: How to read audio file by F# 
categories: [Fsharp]
tags: [audio, Fsharp]
fullview: true
---

Here, I will show how to read WAV file by F#.

First of all, we need to know the file header of WAV.

Every WAV file will have a file header. The general form is like this:

偏移地址	|十进制	|字节数	|类型	|内容
----|------|----
00H~03H	|0-3	|4	|字符	|资源交换文件标志（RIFF）|
04H~07H	|4-7	|4	|长整数	|从下个地址开始到文件尾的总字节数
08H~0BH	|8-11	|4	|字符	|WAV文件标志（WAVE）
0CH~0FH	|12-15	|4	|字符	|波形格式标志（FMT）
10H~13H	|16-19	|4	|整数	|过滤字节（一般为00000010H）
14H~15H	|20-21	|2	|整数	|格式种类（值为1，表示数据PCMμ律编码的数据）
16H~17H	|22-23	|2	|整数	|通道数，单声道为1，双声道为2
18H~1BH	|24-27	|4	|长整数	|采样频率
1CH~1FH	|28-31	|4	|长整数	|波形数据传输速率（每秒平均字节数）
20H~21H	|32-33	|2	|整数	|数据的调整数（按字节计算）
22H~23H	|34-35	|2	|整数	|样本数据位数

16H~17H处记录通道数，当值为1时，表示文件为单声道；当值为2时，表示文件为双声道。

18H~1BH处记录采样频率。它的取值与声卡的支持情况有关。常见的有8000、11025、22050、44100、48000、96000等。其中，44100是大多数歌曲文件采用的标准采样频率。

22H~23H处记录样本数据位数。即每一个采样的长度。常见的有8位和16位。这里还包含了另外一个信息：若样本的数据位数为n，对于双声道文件，则低n/2位用于存放左声道；高n/2位用于存放右声道。

The real data begins at 44.

