&emsp;&emsp;在服务器上测试了两天，最后决定使用更轻量访问速度更快的typecho，然后在各种崩溃中终于把WordPress数据全部迁移到了typecho里，一打开就发现一个问题，在伪静态设置中无法去掉index.php的路径名，google了一下找到解决方案，感谢各位前辈君。

&emsp;&emsp;在网站根目录（即www）中创建**.htaccess**文件，内容如下：
```
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php [L,E=PATH_INFO:$1]
</IfModule>
```
&emsp;&emsp;然后typecho后台 “设置”--“永久链接”中启用rewrite功能即可。

`Gmeek-html<img src=https://testingcf.jsdelivr.net/gh/chaizia/pic/img/20241213150858631.png>`

&emsp;&emsp;其实还有更简洁的办法，服务器如果有宝塔控制面板，可以更轻松搞定，网点选择伪静态，菜单下拉选择typecho，内容如下：

```
if (!-e $request_filename) {
      rewrite ^(.*)$ /index.php$1 last;
     }
```

&emsp;&emsp;看起来顺眼多了，嗯，舒适。

<!-- ##{"timestamp":1607999136}## -->