---
title: 关于HTML的meta标签
date: 2017-11-26 18:55:01
categories: 				# 文章分类
- html
tags: 						# 文章标签
- meta标签
---

> 网页的meta标签必不可少，属性很多，本篇应用中的相关总结。

### 什么是meta标签？2
- meta 标签 -- 在head标签中的meta标签,可以为HTML文档提供额外信息。
- meta的英文翻译为"元"
- meta是metainformation的缩写


属性:
```
	I18N -- i18n属性
	xml:lang -- 国际化属性
	content -- content属性  
	id -- id属性
	name -- name属性，包括author、copyright、keywords、date、description、robots，与SEO有关
	scheme -- scheme属性
	http-equiv 属性 -- HTTP协议的响应头报文
```
http-equiv属性
* 此属性出现在meta标签中
* 此属性用于代替name，HTTP服务器通过此属性收集HTTP协议的响应头报文
* 此属性的HTTP协议的响应头报文的值应使用content属性描述

### 常用的http-equiv类型与name属性

1. charset -- charset 定义编码信息
2. refresh -- refresh 刷新与跳转网页
3. no-cache -- HTML meta no-cache 定义页面缓存
4. *expires -- HTML meta expires 定义网页缓存过期时间*

```html
	<meta http-equiv="content-type" content="text/html; charset=utf-8" /> 	//文件为html文件，且使用了utf8编码
	<meta http-equiv="content-language" content="zh-CN" />		//语言使用了中文

	<meta http-equiv="refresh" content="5" /> 		//5秒后刷新
	<meta http-equiv="refresh" content="5; url=http://hibop.github.io/" />		//5秒后跳转

	<meta http-equiv="expires" content="Sunday 26 October 2008 01:00 GMT" />		// expires用于设定网页的过期时间,一旦过期就必须从服务器上重新加载.时间必须使用GMT格式.

	<meta http-equiv="pragma" content="no-cache" />	//不缓存页面(为了提高速度一些浏览器会缓存浏览者浏览过的页面,通过下面的定义,浏览器一般不会缓存页面,而且浏览器无法脱机浏览.)	

	<meta name="author" content="http://hibop.github.io/" />		author用于定义网页作者

	<meta name="copyright" content="? http://hibop.github.io/" />		定义网页版权

	<meta name="keywords" content="HTML XHTML" />		//关键字

	<meta name="date" content="2008-07-12T20:50:30+00:00" />	//网页生成日期

	<meta name="description" content="html toturial and html books" />		//描述


	<meta name="robots" content="noindex" />
	上面示例定义了此网页不被搜索引擎索引进数据库，但搜索引擎可以通过此网页的链接继续索引其它网页

	<meta name="robots" content="nofollow" />
	上面示例定义了梦之都此网页被搜索引擎索引进数据库，但搜索引擎不可以通过此网页的链接继续索引其它网页

	<meta name="robots" content="none" />
	上面示例定义了此网页不被搜索引擎索引进数据库，且搜索引擎不可以通过此网页的链接继续索引其它网页

	<meta name="googlebot" content="noindex, nofollow" />
	可以将name的属性只定义为GOOGLEBOT标识为谷歌搜索引擎。 使用元标记拦截或删除网页

	<meta name="baiduspider" content="noarchive" />
	可以将name的属性只定义为baiduspider标识为百度搜索引擎。禁止搜索引擎收录的方法
```

### Page-Enter、Page-Exit (进入与退出)

说明：这个是页面被载入和调出时的一些特效。

```html
<Meta http-equiv=”Page-Enter” Content=”blendTrans(Duration=0.5)”>

<Meta http-equiv=”Page-Exit” Content=”blendTrans(Duration=0.5)”>

注意：blendTrans是动态滤镜的一种，产生渐隐效果。另一种动态滤镜RevealTrans也可以用于页面进入与退出效果:

<Meta http-equiv=”Page-Enter” Content=”revealTrans(duration=x, transition=y)”>

<Meta http-equiv=”Page-Exit” Content=”revealTrans(duration=x, transition=y)”>

```

### Duration表示滤镜特效的持续时间(单位：秒)

Transition滤镜类型。表示使用哪种特效，取值为0-23。

        0 矩形缩小 1 矩形扩大 2 圆形缩小 3 圆形扩大 4 下到上刷新 5 上到下刷新 6 左到右刷新 7 右到左刷新 8 竖百叶窗 9 横百叶窗 10 错位横百叶窗 11 错位竖百叶窗 12 点扩散 13 左右到中间刷新 14 中间到左右刷新 15 中间到上下 16 上下到中间 17 右下到左上 18 右上到左下 19 左上到右下 20 左下到右上 21 横条 22 竖条 23 以上22种随机选择一种


### Content-Script-Type (脚本相关)

说明：这是近来W3C的规范，指明页面中脚本的类型。

用法：<Meta http-equiv=”Content-Script-Type” Content=”text/javascript”>


### Pics-label (网页RSAC等级评定)

说明：在IE的Internet选项中有一项内容设置，可以防止浏览一些受限制的网站，而网站的限制级

别就是通过该参数来设置的。

用法：
```
<META http-equiv=”Pics-label” Contect=

“(PICS－1.1′http://www.rsac.org/ratingsv01.html’

I gen comment ‘RSACi North America Sever’ by ‘inet@microsoft.com’

for ‘http://www.microsoft.com’ on ‘1997.06.30T14:21－0500′ r(n0 s0 v0 l0))”>

```

注意：不要将级别设置的太高。RSAC的评估系统提供了一种用来评价Web站点内容的标准。用户可以设置Microsoft Internet Explorer（IE3.0以上）来排除包含有色情和暴力内容的站点。上面这个例子中的HTML取自Microsoft的主页。代码中的（n 0 s 0 v 0 l 0）表示该站点不包含不健康内容。级别的评定是由RSAC，即美国娱乐委员会的评级机构评定的，如果你想进一步了解RSAC评估系统的等级内容，或者你需要评价自己的网站，可以访问RSAC的站点：http://www.rsac.org/。
