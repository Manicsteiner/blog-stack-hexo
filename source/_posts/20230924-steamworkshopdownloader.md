---
title: steamworkshopdownloader 更正和更新
date: 2023-09-24 18:33:46
tags:
---
'workshop_download_item \[appid\] \[pageid\]' 的规律并不总是有效。  
例如[更全面的灾厄体验1.4.4](https://steamcommunity.com/sharedfiles/filedetails/?id=3013209824)直接使用SteamCMD执行'workshop_download_item 1281930 301320984'会报错，在[steamworkshopdownloader.io](https://steamworkshopdownloader.io/)解析会得到一大堆创意工坊页面的链接。此种页面应为“组合包”，无法直接全部下载。  