&emsp;&emsp;先发邮件给[get@psiphon3.com](mailto:get@psiphon3.com)等其自动回复即可获取赛风新版下载地址：目前是https://s3.amazonaws.com/phjr-lupf-zlgw/zh.html  （该地址可能会变，还是以发邮件为准）。

&emsp;&emsp;该软件运行后会默认使用L2TP/IPSec VPN连接，开启vpn失败才会启用ssh模式。当然使用全局vpn纯属找虐，自由的ssh才是王道，可以通过注册表来设置默认启用ssh模式。其注册表设置部分如下：

```
**不自动打开默认浏览器**
REG_DWORD, HKEY_CURRENT_USER, Software\Psiphon3,UserSkipBrowser,1
**跳过浏览器代理设置**
REG_DWORD, HKEY_CURRENT_USER, Software\Psiphon3,UserSkipProxySettings,1
**默认直接使用ssh连接**
REG_DWORD, HKEY_CURRENT_USER, Software\Psiphon3,UserSkipVPN,1
```
&emsp;&emsp;ssh模式下，psiphon3.exe会释放两个文件??.tmp到系统temp文件夹，其中一个连接ssh并设置代理端口socks5 1080，另外一个转换sock5代理到http:8080。比较有趣的地方在这里，直接看图：

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213141611664.png>`

&emsp;&emsp;是不是很熟悉，嘿嘿，plink啊plink，参见plink参数详解：[http://the.earth.li/~sgtatham/pu ... Chapter7.html#plink](http://the.earth.li/%7Esgtatham/putty/0.61/htmldoc/Chapter7.html#plink)   ，可以很轻松的看出来psiphon的ssh账号就是：

```
sever: 
69.90.151.45
username: 
psiphon_ssh_17063f1585a74e32
password: 
fd2bb3d81560a67188b831a583cb69e2d1b1c6991703f162f5d7644b177425e8
port:
22
```
&emsp;&emsp;基本上到这儿都知道该咋办了吧。猜测赛风如果再更新的话，也可能只是换个ssh账号而已，届时自己动手扒吧。如果没有Real-time Defender Professional的话，可以用Process Explorer直接看命令行 :)  good luck。

<!-- ##{"timestamp":1317867936}## -->