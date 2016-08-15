---
layout: post
title: React Native 热更新
---

![]({{site.baseurl}}/public/images/hot/hot00-.png)
<p class="subTitle">RN加载脚本的机制</p>
打包的时候RN会将js文件打包成main.jsbundle，启动App的时候会加载这个bundle文件，所以脚本热更新就是替换掉这个bundle文件。

<p class="subTitle">生成bundle文件</p>
在RN项目根目录执行以下命令来得到bundle文件和图片资源

> react-native bundle --entry-file *需要打包的js文件* --bundle-output *jsbundle文件存放路径* --platform *平台，值为ios或android* --assets-dest *图片资源存放路径* --dev *是否为开发版本，打正式版时赋值为false*
