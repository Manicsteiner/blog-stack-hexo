---
title: 自行发版MAA指北
date: 2024-11-26 22:04:31
tags:
---
## 写在前面
MAA是开源软件，原则上任何人都可以在遵守相应开源协议的前提下自行改动、分发。  
但是，出于对您的账号与数据安全，**不建议**您使用任何**非官方**的发行版。除非您了解自行制作的发行版有哪些新功能、哪些漏洞，也不建议尝试使用自行制作的发行版。  
如果您认为MAA有哪些需要改进的、添加的功能，建议前往主仓库与维护者讨论。  

## 基本状况
当前，基本所有的MAA相关代码和素材都储存在github仓库，发版过程也依赖github actions的运行，进行后续步骤需要一个github账号。  
如果只是修改和替换资源、素材，可以不用自行发版，直接在本地进行素材替换即可。只有C++、C#代码的修改才需要通过自行发版获得一个发行版。其实自己在本地使用Visual Studio生成的dirty版本也可以正常使用，是否需要自行发版请自行斟酌。  
在发版时，如果使用一个官方版本中存在的版本号，那么在官方版本推出新的版本号时，您的MAA客户端可以通过自动更新变为官方最新版本，但添加的额外文件不会被自动移除。如果您不希望发生这种自动更新，请禁用自动更新功能。如果您使用了符合规则但不存在的版本号，那么自动更新时会下载完整包并替换，添加的额外文件很可能也不会自动移除。如果您使用了一个远超当前版本的版本号，我不确定会发生什么，不建议这样做。  

## 具体方法
首先，克隆主仓库至自己的github账号下。在自己的仓库的actions页面，此时应当触发一个“ci”workflow，大约12~20分钟左右生成完毕，在workflow详情页面最下面的Artifacts中会有几个CI-build版本的压缩包，页面左侧最后一项release没有运行。这个生成流程将是我们需要的工作流，但是我们还需要给它添加一个“正式”的版本号，并且推送到release。  
回到自己的仓库的主界面，点击分支，生成一个新分支，我们对源代码的修改和对ci工作流的修改都将在这个分支进行，避免影响主线。  
在新的分支下，打开 `/.github/workflow/ci.yml` 文件，这就是ci工作流的内容。接下来要进行一些修改。  

 - 删除76-86行的changelog生成，479行的移动changelog，488行的输出changelog。  
 - 删除101-102行的生成ARM版。  
 - 删除185-466行的ubuntu版和macos版的生成工作，并删除469行release步骤对ubuntu版和macos版的依赖，和480行的移除macos-build。  
 - 将491行的prerelease设置改为 `prerelease: true`。
 - 删除493行以后的生成OTA工作。  

然后为了方便自行使用，我们在仓库根目录的 `package-definition.json` 添加一个伪OTA包，仅包括程序文件即可。  
```
    {
        "name_template": "FakeOTA-ProgramOnly-{VERSION}-win-{PLATFORM}",
        "type": "FakeOTA",
        "configuration": {
            "include": ["**/MAA.exe", "**/MaaCore.dll"]
        }
    }
```
添加你想要的修改后，来到你的仓库的release页面，点击 `Draft a new release`，生成的新tag处输入一个当前的版本号，如果是内测版的版本号就直接输入 `v5.4.2-alpha.1.d104.g2428a4610` 这样的版本号，而不是主仓库下使用的`alpha/*`，因为我们不打算区分版本，全部将发行版放在此仓库。Target branch选择刚才添加修改的分支。然后勾选`Set as a pre-release`，随意填写title和description，点击发版。然后等待CI执行完毕，生成的发行版包和FakeOTA就会出现在这条release下。

## 操作解释
 - 删除changelog
   印象里是出过错误才删掉的，其实可以保留，不过也没人看，有需求建议手写。
 - 删除ubuntu版和macos版，删除arm版
   你不需要那个，对吧
   不需要的东西会消耗更多的时间。尽管它们会并行执行，还是有可能会消耗更久。
   而且linux和macos使用的编译器对代码要求更严格，如果有未使用的变量会报错误而不是警告等等，可能卡死工作流。
 - 删除OTA生成
   这个工作需要你再克隆MaaRelease仓库、添加拥有写入权限的token，反正我们也不需要将自己的版本的OTA推送给谁，删掉它、把这些工作留在主仓库就好。
 - prerelease设置
   避免仓库被设置最新发行版，也避免误导其他人
 - 479，480行
   删除没有的东西会报错，所以相应改动后记得删掉这里。

## 参考代码
最后发现懒得截图了，请自行参考仓库代码。  
[2024年5月版本](https://github.com/Manicsteiner/MaaAssistantArknights/commit/ca3348c65807d4f4744e70c73678a9f03605a967)
[2024年11月版本](https://github.com/Manicsteiner/MaaAssistantArknights/commit/860c3dedf43c063d2a7dca476217418a88744828)
[release效果](https://github.com/Manicsteiner/MaaAssistantArknights/releases/tag/v5.9.1-alpha.1.d082.g5e959927f)