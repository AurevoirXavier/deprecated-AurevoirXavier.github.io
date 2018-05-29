---
layout: post
title: "jQuery.getScript()"
date:   2018-05-28
excerpt: "jQuery.getScript()"
tags: [php]
comments: true
---

<center><h2>jQuery.getScript()</h2></center>

<!--more-->

它通过 *GET HTTP* 请求加载一个 **JavaScript** 文件然后执行它，这是一个 **ajax** 函数的缩写形式，它等价于：

```javascript
$.ajax({
    url: url,
    dataType: "script",
    success: success
});
```

例子：

```javascript
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>jQuery.getScript demo</title>
    <style>
    .block {
       background-color: blue;
       width: 150px;
       height: 70px;
       margin: 10px;
    }
    </style>
    <script src="https://code.jquery.com/jquery-1.10.2.js"></script>
</head>
<body>
 
<button id="go">&raquo; Run</button>
<div class="block"></div>
 
<script>
var url = "https://code.jquery.com/color/jquery.color.js";
$.getScript( url, function() {
    $( "#go" ).click(function() {
      $( ".block" )
          .animate({
              backgroundColor: "rgb(255, 180, 180)"
          }, 1000 )
          .delay( 500 )
          .animate({
              backgroundColor: "olive"
          }, 1000 )
          .delay( 500 )
          .animate({
              backgroundColor: "#00f"
          }, 1000 );
    });
});
</script>
 
</body>
</html>
```

<center>[深入了解](https://api.jquery.com/jquery.getscript/)</center>