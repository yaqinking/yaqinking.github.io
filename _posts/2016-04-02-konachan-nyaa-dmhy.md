---
layout: post
title: 对 Konachan Nyaa DMHY 这几个工具的一些说明
date: 2016-04-01 23:59
categories: life
---

用起来顺不顺手，知道 creator 的设想操作方法的话，就好办了。于是，窝来说说自己为什么会让这几个工具成现在这样子。

[Konachan](https://github.com/yaqinking/Konachan)（Mac）这个原因很简单，要收 uncensored 的图，于是想办法动手了，听说 [AFNetworking](https://github.com/AFNetworking/AFNetworking) 很好用，看着 repo 的 README 跟着做，把单个图片下载到本地之后，接下来的就是细节上的处理，核心代码不超过 50 行，所以有心的话（很快就出来的感觉，不过估计因为用途太小众，也没人写，毕竟这个年代先把图片下到本地，然后看的估计很少。）

[Nyaa](https://github.com/yaqinking/Nyaa)（Mac）依然 Picture 分类下和偶然间知道的 sukebei 里站里的 ゲイムCG 关键字的，因为在浏览器里打开新页面查看，或者查看之后后退感觉不方便，于是就搞了这个，不过因为各种自身原因，坑掉了，虽然还可以用，然而就是在写这个应用时折腾的解析 HTML 在接下来的工具中有用到。

[Konachan-iOS](https://github.com/yaqinking/Konachan-iOS) 原本我是先下载到本地，然后用 [ComicGlass](http://comicglass.net/) 通过 SMB 看下载的图的，不过一天晚上在宿舍床上感觉还是写个 iOS 版本的会更方便点，至于理念：

1. 基于 tag 关键字
2. 点进 tag 显示预览小图（其实这个有没有都无所谓，窝是每张图都会看的）
3. 点进小图显示大图，点击大图界面的屏幕上半部分显示上一张，下半部分显示下一张（方便单手操作）
4. 预加载图片来减少看图所需要等待的时间。（这个最近想起来折腾一番之后基本搞定。）

嗯，非常基础而又必需的功能需求点 🌚，至于更进一步的收藏 balabala 的，有人需要，不过我还不想让自己成为一个收藏癖的用户 🙈

[DMHY](https://github.com/yaqinking/DMHY) （Mac）还是因为[花园](https://share.dmhy.org)主页里只有 magnet 不像 [nyaa](http://www.nyaa.se/) 直接有个 download 按钮，还要进详情页才能下到种子，至于我为什么不用 magnet，窝这边 uTorrent 从添加 magnet 链接成功到文件开始下载的间隔难以忍受的长，所以还是直接下种子完事。于是最初的版本就是一个简化获取种子下载链接的工具，附带着整理每天要看的新番关键字到左侧栏里，直到最近把自动下载订阅关键字的新种子功能实现后才感觉到，好吧，让我追番的操作过程简化了好多好多好多。

原本是因为昨晚试用了下看图的同类型的工具，感觉它们的用法和自己想象中的还是有点不同，于是想说下 Konachan-iOS 为什么更方便来着 _(:3 」∠ )_