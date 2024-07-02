---
title: 将Bilibili番剧页面变回旧版
date: 2024-06-30 20:30:19
tags:
---
小陈又一大恶行😈  
新版番剧页面无法与“解除B站区域限制”同时工作，需要将其切换回旧版。然后返回按钮又被藏起来了，所以需要复杂操作。  
首先打开一个B站页面（其实什么都可以，最好是需要转换的番剧页面），按F12进入调试模式，Edge在最上面一栏的工具栏里选“应用程序”（或点加号里找到它），选择“存储”-“Coockie”-“https://www.bilibili.com”，Firefox选择“存储”-“Coockie”-“https"//www.bilibili.com”，新建项目，名称为“i-wanna-go-back”，数值为2，然后删除名称为“buvid”开头的几个coockie条目（据说至少要删除“buvid3”），刷新页面即可。修改这些coockie不会丢失登录状态。如果有需求，可以将新建的条目的过期时间手动超级延后。  
相关的，还有几个coockie条目也被建议修改，但没有修改似乎也没什么影响：“i-wanna-go-feeds”，数值为-1；“go-back-dyn”：1；“go_old_video”：1；“nostalgia_conf”：1。  
以上方法基于旧播放页面仍然存在，仅向用户隐藏为前提，如果这个旧页面被彻底删除，则会失效。  
