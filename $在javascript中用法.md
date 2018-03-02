### javascript中 $ 的作用
* 用作选择器
```
var e = $("h1 a");
var f = $("table tr:nth-child(even)")
```
* $用作功能函数前缀
```
var str = ' Welcome to 86shichang.com ';
str = $.trim(str);  //$.trim是jQuery的一个工具函数，实现去掉两边空格的功能
jQuery给我们提供了主要有7类工具函数
```
* $相当于 window.onload 和$(document).ready(...)

```
$(function(){...}); 里面的函数会在DOM树加载完之后执行
$(function) 是 $(document).ready()的简写方式，当DOM文档载入完成后执行相应的函数

以下两个相等

$(document).ready(function(){
 alert("Hello World!");
});

$(function(){
 alert("Hello World2!");
});
```

* $用来创建DOM元素
```
例如：$("<p>how are you?</p>")
创建DOM对象，注意必须有<p>和</p>或者是其他的html标签，如<h1></h1>,<span></span>
$('<div>86市场网</div>').appendTo('body');//动态创建一个div元素（以及其中的所有内容），并将它追加到body中。
```

