---
layout: post
title: React Native 热更新
---

![]({{site.baseurl}}/public/images/hot/hot00-.png)
<p class="subTitle">RN加载脚本的机制</p>
打包的时候RN会将js文件打包成main.jsbundle，启动App的时候会加载这个bundle文件，所以脚本热更新就是替换掉这个bundle文件。
<br />
<br />
<p class="subTitle">生成bundle文件</p>
在RN项目根目录执行以下命令来得到bundle文件和图片资源

> react-native bundle --entry-file &lt;需要打包的js文件&gt; --bundle-output &lt;jsbundle文件存放路径&gt; --platform &lt;平台，值为ios或android&gt; --assets-dest &lt;图片资源存放路径&gt; --dev &lt;是否为开发版本，打正式版时赋值为false&gt;

![]({{site.baseurl}}/public/images/hot/hot01.png)
<br />

> *Note：*
> 1. assets目录与main.iOS.jsbundle通过打包成zip包上传到服务器。
> 2. 该路径中所用到的&/bundles需要在项目根目录下手动创建,可以为任意目录。
> 3. 图片资源目录assets与jsbundle文件在打包成zip包时,必须在同一级,如图所示。