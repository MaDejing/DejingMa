---
layout: post
title: React Native 热更新
---

![]({{site.baseurl}}/public/images/hot/hot00-.png)
<p class="subTitle">RN加载脚本的机制</p>
打包的时候RN会将js文件打包成main.jsbundle，启动App的时候会加载这个bundle文件，所以脚本热更新就是替换掉这个bundle文件。

<p class="subTitle">生成bundle文件</p>
在RN项目根目录执行以下命令来得到bundle文件和图片资源：

>
> 
>
