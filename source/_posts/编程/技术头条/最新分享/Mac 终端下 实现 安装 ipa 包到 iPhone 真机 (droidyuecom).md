
---
title: 'Mac 终端下 实现 安装 ipa 包到 iPhone 真机 (droidyue.com)'
categories: 
 - 编程
 - 技术头条
 - 最新分享
headimg: 'https://picsum.photos/400/300?random=6009'
author: 技术头条
comments: false
date: 2022-02-03 05:20:21
thumbnail: 'https://picsum.photos/400/300?random=6009'
---

<div>   
最近处理 Flutter 的开发工作，开始尝试使用 iOS 作为日常的真机调试工作。对于一个原技术栈为 Android的人来说，发现 iOS 有很多不太方便的地方。比如如何在 Mac 电脑上安装 ipa包到 iPhone 上。

相比来说，Android 提供了adb 可以很快捷的在 终端上执行安装。而iOS 我也希望有一个可以在终端上实现安装ipa的方式，摸索了一下，终于发现了一个可行的技术方案。






这个可行的技术方案就是 ideviceinstaller，它是一个终端管理 iOS 设备上app 和存档的工具。

进行安装

Mac 下使用 HomeBrew 安装

1
brew install ideviceinstaller


安装一个app

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
ideviceinstaller -i
    
</div>
            