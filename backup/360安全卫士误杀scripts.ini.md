&emsp;&emsp;下午出去和友人吃饭唱歌小high一把。傍晚回来发现老妈帮我整了电脑，打开一看果然临走之前忘了开启影子模式。电脑上安装了360安全卫士一个，查看记录，清理了若干插件，并且恢复了我的notepad2为notepad(-_-# 坑爹啊)，果断卸载，然后开启影子。

&emsp;&emsp;重启之后看了下事件管理器，发现有“组策略客户端扩展 脚本 执行失败。请查看此扩展先前报告的所有错误。”如图：

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213141858917.png>`

&emsp;&emsp;果断检查开机关机脚本，因为我一直用一个关机脚本，关机时自动删除Firefox的浏览记录、书签、cookies和密码，打开C:\WINDOWS\system32\GroupPolicy\Machine\Scripts一看，果然没有了scripts.ini，新建了一个搞定，重启后错误解决。

&emsp;&emsp;然后重新安装360安全卫士，发现果然误杀scripts.ini，图就不截了，希望[@小紫英](http://weibo.com/baiyangzuo) 能帮忙反映一下，谢.....

<!-- ##{"timestamp":1318645536}## -->