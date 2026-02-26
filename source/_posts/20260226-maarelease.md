---
title: 自行发版MAA指北-6.3.x
date: 2026-02-26 22:42:17
tags:
---
## 写在前面
参考前篇 [自行发版MAA指北](/blog/20241126-maarelease/)

## 当前版本
2026年2月
branch [AVD-6.3.0](https://github.com/Manicsteiner/MaaAssistantArknights/tree/AVD-6.3.0) 可能长期存在，也可能被移除  

sample [fakebuild](https://github.com/Manicsteiner/MaaAssistantArknights/commit/fcd2e9ba36d680d625c38407f2856f9f3b59a442)  

 - 删除66-69行的release tag判断和changelog生成。
 - 删除102行的winarm生成。
 - 在191-212行的Collect PDB Files、Upload PDB Files等环节添加手动打包和上传FakeOTA，并记得清除它。
 - 删除224-539行的ubuntu和macos生成，本次保留了ubuntu x64版本，在543行的依赖移除对应的系统。
 - 删除553-554行的changelog和macos杂项清理，它们本就不存在。
 - 将565行的prerelease设置改为 `prerelease: true`。
 - 删除566行以后的后续工作流内容。

`package-definition.json` 似乎已经没有作用，不需要再进行修改。FakeOTA的生成改在此工作流内进行。