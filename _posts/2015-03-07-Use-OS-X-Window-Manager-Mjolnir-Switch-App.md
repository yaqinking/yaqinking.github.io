---
layout: post
title:  "OS X 下使用 Mjolnir 来快速切换 App"
date:   2015-03-07 12:10:00
categories: 软件
---
效果
![](/assets/images/osx-use-mjolnir-effect.jpg)

[Mjolnir 官网](http://mjolnir.io/)

[我看的教程](http://thume.ca/howto/2014/12/02/using-mjolnir-an-extensible-osx-window-manager/)

[我的配置](https://github.com/yaqink/SoftwarePreference/blob/master/Mjolnir/init.lua)

快速配置：

- 從官網下載安裝 Mjolnir
- 安裝依賴(首先你需要安裝過 brew)
{% highlight bash %}
brew install lua
brew install luarocks

echo 'rocks_servers = { "http://rocks.moonscript.org" }' > ~/.luarocks/config.lua

luarocks install mjolnir.hotkey
luarocks install mjolnir.application
luarocks install mjolnir.bg.grid
luarocks install mjolnir.th.hints
luarocks install mjolnir.cmsj.appfinder
luarocks install mjolnir.tiling
luarocks install mjolnir.sd.grid
luarocks install mjolnir.lb.itunes
luarocks install mjolnir._asm.ui.sound

mkdir ~/.mjolnir/
{% endhighlight %}
- 把我的配置文件放到 ~/.mjolnir/ 下（完成後是：~/.mjolnir/init.lua）

PS: ~ 代表用戶文件夾

此 App 可用来作为一个 Window Manager 用，不过我已经买了 Divvy 了，不想花时间配置，所以現在只用來切換應用，并且 OS X 这个系统，很多组合键都已经预先分配好了，自定義組合鍵很痛苦。