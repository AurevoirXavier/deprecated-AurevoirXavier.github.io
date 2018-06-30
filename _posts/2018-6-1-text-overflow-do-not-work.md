---
layout: post
title: "text-overflow: ellipsis do not work"
date:   2018-06-01
excerpt: "text-overflow ellipsis 无效"
tags: [css]
comments: true
---

<center><h2>text-overflow ellipsis 无效</h2></center>

<!--more-->

今天在更新本站界面的时候发现有些标题过长会影响内容的显示，于是打算把过长的标题多出的部分用省略号替换。经过一番搜索，发现甚至不用编写一个函数来控制长度，可以直接通过 **css** 来控制，而且有一个好处就是这样是动态伸展的。

下面这个例子是可以正常工作的：

```html
<html>
<head>
	<style>
	.foo {
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
	}
	</style>
</head>
<body>
	<div class="foo">
        A long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long text.
	</div>
</body>
</html>
```

然后在一个稍微复杂的页面照葫芦画瓢：

```html
<html>
<head>
	<style>
        .foo {
            display: flex;
        }
        .bar {
            flex: 1;
            /*max-width: 100%;*/
        }
		.baz {
        	white-space: nowrap;
        	overflow: hidden;
        	text-overflow: ellipsis;
		}
	</style>
</head>
<body>
    <div class="foo">
    	<div class="bar">
			<div class="baz">
        		A long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long text.
			</div>
    	</div>
    </div>
</body>
</html>
```

上面这个例子是不生效的，而核心就在于注释的那一行宽度设定，只有知道确定的宽度才能确定什么时候该缩略。有些人可能会说即使你不设置宽度那些元素也不代表没有宽度，这么说虽然没错但是一开始进行渲染的时候并不知道确切的宽度，你看到的都是元素排版后的情况。顺便一提，不一定要设置 `max-width` 使用 `min-width`，`width` 或者其他能设置宽度的都是可行的。