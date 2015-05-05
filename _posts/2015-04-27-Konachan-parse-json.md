---
layout: post
title: Konachan 收圖工具
date: 2015-04-27  16:10:34
categories: 開發
---
解析從 Konachan 收到的 JSON 數據，提取出圖片的下載地址，核心代碼不到 30 行，重要的是思路 >_Q
![](/assets/images/konachan-json.jpg)

思路:

- 從 [Konachan API Documentation](http://konachan.com/help/api) 中得知 JSON 地址
- 目測出原文件下載地址的 Key 是 `file_url`(題圖的 poi)
- 將返回的 JSON 數據放入到一個 NSArray 中
- 從 NSArray 中提取出每一個 picture 的 NSDictionary 對象
- 從 NSDictionary 中根據 Key(`file_url`) 取出 Value(`http://xxx.jpg`)
- 將 取出的 Value(`http://xxx.jpg`) 放入到一個 NSArray 中
- 遍歷包含網址的 NSArray ，將每一個元素轉換成 NSURL 對象，之後下載到本地 Downloads 文件夾下


[源碼](https://github.com/yaqink/Konachan)