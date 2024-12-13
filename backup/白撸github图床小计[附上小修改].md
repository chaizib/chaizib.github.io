&emsp;&emsp;最近在做网站备案，临时搬到wiki主机处，他家的虚拟主机空间有点限制，然后就搜了一下现在有没有什么靠谱的图床之类的可以加加速也避免被限制，然后就发现有人早就打上了GitHub的主意，仔细看了看，十分值得推荐。

### 原理

&emsp;&emsp;GitHub给开发者提供无限制的免费私有存储库，这首先就解决掉了图床的存储问题，但是GitHub在国内无法正常访问，于是再借用jsdelivr的免费CDN加速（有国内节点），于是一个高速访问无限制的图床诞生了。但是这依然不够完美，地址转换也比较麻烦，于是[乔千](https://github.com/MliKiowa/GitStatic)大佬写了一个插件“GitStatic”，可以在typecho中上传附件，文件直接传到GitHub，然后转换成jsdelivr加速过的链接直接在文章内引用。

### 效果

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213151937817.png>`

### 方法

&emsp;&emsp;教程太多了，随便找一个大家看吧。这里不再详述。[点击查看教程](https://zhuanlan.zhihu.com/p/133331451)

&emsp;&emsp;原作者更新的2.0 alpha 版加入了整站加速的内容，一般来说不需要，直接用其1.2版。

&emsp;&emsp;敲黑板，考点：在我搬到wiki主机处时，发现插件无法正常加载，经过排查，发现原作者有一处写法不够规范，修改后问题解决。涉及到的文件有GitHelper.php和Plugin.php，这两个文件用文本打开：

```
第1行原文
<?
直接修改成如下即可
<?php
```

<!-- ##{"timestamp":1608603936}## -->