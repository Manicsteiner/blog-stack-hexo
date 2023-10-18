---
title: CRIWare AWB 新版文件问题
date: 2023-10-18 20:24:24
tags:
---
在游戏"Summertime Render Another Horizon" (Switch) 中，awb格式文件有所改动，其中一些原先使用两字节ushort存储的数据改为使用四字节uint，导致老旧处理工具无法使用。如有处理需求请使用foobar2000+VGMStream。