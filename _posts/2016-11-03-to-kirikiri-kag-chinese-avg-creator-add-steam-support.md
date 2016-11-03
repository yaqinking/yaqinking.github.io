---
layout: "post"
title: "献给使用 Kirikiri+KAG 引擎想要上 Steam 的中文 AVG 创作者的一份指南 - 从零开始的编译 krkrsteam 插件到集成到 KAG 脚本里再到发布 alpha 版到 Steam 供内部测试"
date: "2016-11-03 09:25"
---
![](http://i.imgur.com/q5HO7Db.png)

# 最初的最初

这篇教程中会出现以下软件、工具、关键字：

编译 krkrsteam 插件时：

krkrsteam、Visual Studio 2012、系统环境变量设置，命令提示符、premake4、ncbind、tp_stub

上传发布内容到 Steamworks 时：

Steampipe GUI Tool、Steamworks、Steam Greenlight（绿光）、AppId、Depot

以及基本大家都知道的：

krkr.eXe krkrsteam.dll（krkrsteam-d.dll debug 时用）

![](http://i.imgur.com/g4a7zKz.png)

如果你有英文、日文阅读 readme/文档 的能力的话更好，因为操作上窝也是看 readme/文档 之后才学会的。

这个教程里面没有提到怎么发 Greenlight（绿光），发绿光的话依然也是跟着官方操作步骤指引，文档指南可以做到的，在绿光通过之后，就是 Greenlint 之后会得到一个 appid，这个 appid 是标识自己在测试游戏的名称，及发布时玩家在玩游戏时显示的 XXX 正在玩 XXX 的识别符。

同时也没有提怎么申请 Steamworks 开发者账号，官方操作流程指引已经很清楚了，就没必要一步一步说这些了……

# 编译 krkrsteam 插件

krkrsteam 的源码可以在 kirikiri2 官网 svn 服务器里下载：https://sv.kikyou.info/svn/kirikiri2/trunk/kirikiri2/src/plugins/win32/steam 建议把 `plugins` 文件夹下的所有插件都下载到本地。

也可以在有人 clone 的 GitHub repo 里下载：https://github.com/jeeb/kirikiri2/tree/master/kirikiri2/src/plugins/win32/steam 这个基本就只能把 repo 本体全部下载到本地了，不过可以在下载完成之后把 `plugins` 文件夹 copy 到其它位置之后在那个文件夹里开始作业。

源码下载到本地之后，可以看 `readme.txt` 里的内容配置编译环境，这里只作一个简要介绍。

Steamworks 的 SDK 可以在 https://partner.steamgames.com/home 里拉到下面的右侧看到下载地址，下载完成解压到 C 盘，然后把 `sdk` 文件夹重命名为 `steam_sdk` 文件夹

1. 首先生成 Visual Studio 2012 的 project（项目）文件时需要 premake4 这个工具，可以在 http://industriousone.com/premake 里下载。
2. 下载 premake4 安装到本地文件夹里，如：`c:\premake\` 然后把这个路径配置到 `系统环境变量` 中去，同时也把 steam_sdk 的环境变量设置下，步骤：
    1. 使用组合快捷键 `win+r` 打开运行窗口<br/> ![](http://i.imgur.com/7OjVXzY.png)
    2. 输入 `SystemPropertiesAdvanced` 按回车打开系统属性/高级窗口
    3. 点击 `环境变量(N)...` 按钮 -> 找到 `系统变量(S)` 下的变量名为 `Path` 的那一栏之后，双击进入编辑模式，定位到最开始，输入 `C:\premake;` （或者拷贝 premake4 安装的文件夹路径，粘贴到这里之后加上一个 `;` 分隔符号），点击 `确定`，再次点击 `确定`。<br/> ![](http://i.imgur.com/OHJ00QR.png) <br/> 此时 `premake4` 的系统环境变量设置已经完成。同时在这个步骤新建一个环境变量变量名为：`STEAMWORKS_SDK` 变量值为：`C:\steam_sdk` （或者直接拷贝你解压 steam_sdk 文件夹的路径粘贴到这里来。）<br/> ![](http://i.imgur.com/navXhLg.png)
    4. 打开命令提示符（`win+r` 打开运行框之后输入 `cmd` 然后按 `Enter` 键）后，输入 `premaker4` 然后按回车键之后，应该会有 `Type 'premake4 --help' for help` 这一行字出现，如果没有出现请确认上述步骤和路径设置正确。如果已经出现表示 premake 的系统环境变量设置已经完成。<br/> ![](http://i.imgur.com/jOIf5i0.png)
    5. 使用 `cd` 命令在命令提示符窗口里切换当前工作路径到 krsteam 文件夹里，如：`cd C:\krkr_plugins\plugins\win32\steam`
    6. 输入 `premake4 vs2012` 按回车之后应该能看到 krsteam 文件夹多了一个 `vs2012` 文件夹，里面有 Visual Studio 2012 可以打开的 project solution 文件

3. 安装 Visual Studio 2012。（应该会耗时挺久的…………）
4. 使用 Visual Studio 2012 打开在 `krkrsteam` 文件夹里的 `vs2012` 文件夹下的 project solution 文件。（名字应该是：`krkrsteam.sln`）
5. 编译之后你会发现有一些错误，把相关代码注释掉之后再次编译，应该就正常的编译成功了。如果出现大巴大巴的错误，请检查：
    1. 是不是不是用的 VS2012？（VS2015 会出现各种莫名其妙的错误，为了节省时间请用 VS2012 来编译开发插件……显然这里是一个问题，不知道维护者会不会改进下，并且目前 tp_stub 文件的生成也不能使用 perl，jin1016 在窝发的这个 issue 里 https://github.com/krkrz/krkrz/issues/264 说了，乃去用  https://github.com/krkrz/krkrz/tree/last_hodgepodge_repository 这个 branch 里的文件好了。嗯，就这样。）
    2. STEAMWORKS_SDK 的环境变量设置了没？（这里的环境变量名可以在 premake4.lua 文件中看到有定义）
    3. krkrsteam 文件夹是否是和下载的 plugins 文件夹里一同放着的？（因为 krkrsteam 有用上一级目录里的 ncbind 插件和 tp_stub.h tp_stub.cpp 文件所以才会需要直接把所有的插件都给下载下来。）

6. 编译完成之后会在 krkrsteam 文件夹里生成一个 bin/krkrsteam-d.dll 和一些其它的文件，那些暂时不用管，把 krkrsteam-d.dll 拷贝到 krkr.eXe 所在的文件夹里去，自己用的最初的 krkrsteam 插件就算 ok 了。

关于 demo、release 时的 krkrsteam 插件：

可以在 VS 里使用打开 Project 的 Peoperties，使用 Configuration Manager 把 Active solution configuration 从 Debug 切换到 Release，然后 build 就会生成 krkrsteam.dll 不是带 -d 的了。


关于启动时显示未运行 Steam 客户端，不能打开的问题：

其实 demo 或者正式版 release 的时候是不会带 steam_appid.txt 这个文件的，其中的 appid 是要自己修改 krkrsteam 源码在 `SteamAPI_Init()` 这行代码之前调用 `SteamAPI_RestartAppIfNecessary( YOUR_APPID )` 这行代码的，详细可以参考 Steam 官方的 sample 代码。在测试的时候大概是这个样子：

```cpp
// 把 YOUR_APPID 替换为自己游戏的 AppId
if ( SteamAPI_RestartAppIfNecessary( YOUR_APPID ) )
{
	// if Steam is not running or the game wasn't started through Steam, SteamAPI_RestartAppIfNecessary starts the
	// local Steam client and also launches this game again.

	// Once you get a public Steam AppID assigned for this game, you need to replace YOUR_APPID with it and
	// removed steam_appid.txt from the game depot.
    // 下面这一行代码在 release 的时候注释掉，以免报错……在 debug 的时候可以保持这样子
	TVPThrowExceptionMessage(L"SteamAPI_RestartAppIfNecessary failed");
}
```

# 集成到 KAG 脚本中

在 `data/system/Initialize.tjs` 的 Plugins.link 那几行代码里加入 `Plugins.link("krkrsteam-d.dll");` 这时候在初始化 KAG 的时候就会尝试在 krkr.eXe 所在的文件夹下寻找 `krkrsteam-d.dll` `steam_api.dll` `steam_appid.txt` 这三个文件，不出意外的话，在进入游戏之后会在左上角显示提示使用 `Shift+Tab` 显示 Steam 面板什么的，这个时候尝试使用 `F12` 截图应该也会有通知提示，初步 Steam 集成的工作就算到这里成功了。

![](http://i.imgur.com/g4a7zKz.png)

因为这张图很重要，所以要放两边！

关于成就解锁：

成就定义：基本上跟着文档走，只用把 Step 1 定义搞好了之后就可以进行下一步了 https://partner.steamgames.com/documentation/bootstrap_achieve

写 KAG 脚本时触发成就，依然使用说明见 ：https://github.com/jeeb/kirikiri2/blob/master/kirikiri2/src/plugins/win32/steam/manual.tjs

这里基本上没啥好说的，看文档跟着走测试就是。

# Build Depot 上传到 Steam 供内部测试

嗯，还是跟着官方文档走 https://partner.steamgames.com/documentation/steampipe

不想使用命令行和自己写配置文件 build 的话，可以使用官方文档里面有提到的 Steampipe GUI Tool http://steamcommunity.com/groups/steamworks/discussions/0/412449508292646864/

![](http://i.imgur.com/oBpXxOs.png)

# 配置 Steam 云存档

在 https://partner.steamgames.com/apps/cloud/YOUR_APPID 里面跟着官方文档 https://partner.steamgames.com/documentation/cloud 里的 Steam Auto-Cloud for legacy games 里的步骤走，基本上不需要自己写什么代码就能把云存档给搞定。（当然这里说的也是基本的，会使用代码自定义的话能实现更自由的操控感。）

![](http://i.imgur.com/o392Nh1.jpg)

# 最后

整体上找到 krkrsteam 源码，编译成自己的游戏所需要的，这个部分花费的时间是挺多的，而 Steamworks 的使用上，人家的文档写的真的真的真的很详细，跟着走就是。

希望自己所做的事情能够为中文 AVG 创作者们带来一些帮助，以上。
