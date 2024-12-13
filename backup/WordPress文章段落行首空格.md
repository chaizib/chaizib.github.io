&emsp;&emsp;关于WordPress文章段落首行空格的问题，WordPress在用Mozilla Firefox、谷歌浏览器Chrome、Opera这些浏览器编辑文章的时候，段落空格都会无效只能在HTML中写&nbsp; 或者切换到，HTML源代码编辑器，再用空格这样才能实现段落文字缩进的效果!
如用不是用这些方法Firefox、Chrome、Opera下面编辑发表文章每段前的空格总会变没有了！具体什么原因也不想研究，具体解决方法有如下两种:

&emsp;&emsp;第一种方法：直接用IE，行首空两个全角空格即可！这样就不会出现段落首行空格失效！（但搞网站的很少人用IE的了）

&emsp;&emsp;第二种方法：使用CSS,用CSS控制<p> 在使用的主题CSS中加入如下代码？

```
p{text-indent:2em;}
img{text-indent:2em;}
```

<!-- ##{"timestamp":1195003355}## -->