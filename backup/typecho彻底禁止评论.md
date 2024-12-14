&emsp;&emsp;今天接到某局电话，有个傻X在我博客以前的老文章中留言评论，其个人网站链接为某黄色网站，应要求删除该人评论后，索性准备直接关闭留言评论功能。因为开放评论即有审核的义务，但平时根本不可能有那么多时间来核实所有链接，不如关闭省事。

&emsp;&emsp;但问题来了，在typecho的系统中，只能更改评论的权限，不能在设置中做到完全禁止。于是干脆曲线救国，直接关闭显示入口，找到当前主题的post.php和page.php文件，打开后直接搜索评论显示部分：

`<?php $this->need('comments.php'); ?>`

&emsp;&emsp;删除该行内容或者注释掉，搞定。

`<?php /* $this->need('comments.php');  */ ?>`

PS：实名谴责AirPods 3，脑残似的改成这么傻短粗，磨合硬撑了四个月，耳朵眼子依然生疼…… shit！

`Gmeek-html<img src=https://testingcf.jsdelivr.net/gh/chaizia/pic/img/20241213152231191.png>`


<!-- ##{"timestamp":1647311136}## -->