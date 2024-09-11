---
title: MAGES引擎游戏资源提取方法指北v2.3
date: 2024-09-11 22:45:06
tags:
---
基于v2.2进行少量更新，此处只写更新的部分。  

## 写在前面
根据一些软件的问题反馈，Github Runner和Visual Studio自2024年6月中的一次更新后所编译生成的程序可能无法在Windows7上运行。如果您仍在使用这个系统，请注意此问题，并根据自身情况选择更新系统或者使用2024年6月前的版本。  

## 通用处理逻辑
GARbro个人维护版本迁移仓库。我为个人维护版本和crskycode版本添加了自动构建脚本，如果您想要体验最新版的功能但不方便在本地构建，可以在登录Github账号后在对应仓库的 Actions 下找到对应的workflow，下载其中的ci-build版本的程序。根据仓库设置，这些内容会保留1-3个月不等。  
[GARbro 个人维护版本|Github](https://github.com/Manicsteiner/GARbro) 需要DotNet Framework 4.6.2  

## MAGES引擎-PC端
有网友重置了此脚本。个人不对其功能和稳定性做保证。  
[ChaosChildPCTools-wangyw15|Github](https://github.com/wangyw15/ChaosChildPCTools) 当前版本(53fe761)需要Python3.12，需要pip依赖 pillow >=10.1.0，<=10.3.0  

## MAGES引擎早期版-PSV
使用了类似BGM_AT9.MPK命名的MPK文件可以用最新版的GARbro打开。  

## M2/E-mote/KaledoADV引擎
PS3平台的密钥现在有办法获取，您需要安装并配置好RPCS3模拟器，在工具栏选择 Utilities-Decrypt PS3 Binaries，选择对应游戏的 EBOOT.BIN 文件，解密得到一个 EBOOT.elf 文件，然后可以按类似PSV版的方法，在"script_info.psb.m"等一系列文件名前找到。  

## Unity引擎
AssetStudio原版已长时间未更新，推荐两个有少量更新维护的版本。  
[AssetStudio-zhangjiequan|Github](https://github.com/zhangjiequan/AssetStudio) 需要DotNet Framework 4.7.2 或 DotNet 5/6  
[AssetStudio-aelurum|Github](https://github.com/aelurum/AssetStudio) 需要DotNet Framework 4.7.2 或 DotNet 6/8  

## Unity引擎+CRIWare封包
YuruCampHeaderAdder 在热心网友的帮助下已经可以处理其他几个图片包。  

## Unity引擎+未知封包
幻想マネージュ（Switch）：QPK文件似乎可以由最新版的GARbro处理，双击DATA\#00002打开，其中的bg按文件夹打开，可以查看其中的图片文件。记得按顺序从上到下打开各个文件，否则有可能报错。  