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
<blockquote>
	<i>Note:</i>
	<ol>
		<li>assets目录与main.iOS.jsbundle通过打包成zip包上传到服务器。</li>
		<li>该路径中所用到的&/bundles需要在项目根目录下手动创建,可以为任意目录。</li>
		<li>图片资源目录assets与jsbundle文件在打包成zip包时,必须在同一级,如图所示。</li>
	</ol>
</blockquote>
<br />
<p class="subTitle">下载bundle文件</p>
<u><b>下载文件</b></u>和<u><b>解压缩</b></u>js实现，在<u><i>src/layouts/Global.js中的_onUpdate()</i></u>函数内。

<ol>
	<li>使用<a href="https://github.com/johanneslumpe/react-native-fs">react-native-fs</a>实现下载zip包功能，将其放在Documents目录下。
	</li>
	<li>解压缩工作使用<a href="https://github.com/remobile/react-native-zip">react-native-zip</a>实现，解压至Documents目录下。
	</li>
	<li>解压成功后，使用<a href="https://github.com/johanneslumpe/react-native-fs">react-native-fs</a>将zip删除。
	</li>
</ol>

<br />
<p class="subTitle">替换bundle文件</p>
<ol>
	<li>新建<i><u>MJAppUtilModuleManager类</u></i>类，并提供<i><u>bundleUrl</u></i>类方法。</li>
	<li>在application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary
*)launchOptions中使用<i><u>jsCodeLocation = [MJAppUtilModuleManager bundleUrl];</u></i></li>
	<li>MJAppUtilModuleManager类中导出方法<i><u>setJSBundleFile: (NSString *)DEST</u></i>提供给js。js在解压缩成功后调用该方法，并向其传递参数<u>bundle文件的绝对路径</u>。(例如，/var/mobile/Containers/ Data/Application/5F3FEF2A-F938-481A-A46C-83C8EE626222/Documents/chat/iOS/ main.jsbundle)</li>
	<li>在setJSBundleFile方法中将绝对路径进行处理，得到相对路径，并将<u><b>相对路径目录</b></u>和<u><b>文件名</b></u>分别存入MJAppUtilDEST.plist文件，下次启动App时读取并重新进行拼接。</li>
	<li>在类方法<i><u>bundleUrl</u></i>中，将plist文件中的路径拼接得到当前bundle文件的绝对路径。对文件是否存在进行判断，若存在则使用该bundle文件，若不存在，则依旧使用main.jsbundle。
</li>
	<li>在js文件中通过<i><u><Image source = { require(‘./imgs/test.png') } /></u></i>被获取的图片资源会被打包至assets目录下。若使用热更新，只要assets目录与bundle文件在<u><b>同一目录</b></u>下，那么js文件中使用require获取的图片资源就会从assets目录下获取。图片资源的热更新也就实现了。</li>
</ol>




