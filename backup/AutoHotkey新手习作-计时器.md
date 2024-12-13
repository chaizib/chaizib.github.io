&emsp;&emsp;前两天刚刚开始接触AutoHotkey，发现真的很好玩，有一句口号说的太好了，AutoHotkey适合那些懒人>…<

&emsp;&emsp;看了一会帮助文件，发现比当初用过的按键精灵什么的舒服多了，试着做了一个模拟按键点技能的东西在wow中试了一下，感觉很不错。我下载的是AutoHotkey V1.0.48.05 ，顺手把壳扒了『UPX壳真的很龊』，汉化了部分，看起来顺眼多了

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213121234513.gif>`

&emsp;&emsp;昨天写过一个代替myentunnel的东西，ss大牛立马丢出来一个更好看的在[11楼](http://hipschina.com/viewthread.php?tid=2722&page=1&fromuid=4#pid26160)，大受刺激，下载源码后学了一下，然后查了下gui的写法，受益颇多 :) 刚好老婆要我烧水『家里用电磁炉配水壶烧水，我经常上网烧忘记了』，于是试试用AutoHotkey写个定时器，很容易三分钟就写出来了，很舒服。比用别的工具要简单的多。

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213121313060.gif>`

&emsp;&emsp;代码如下：『菜鸟习作，勿笑，敬请指点』

```
#SingleInstance,off
Menu,tray,NoStandard
Menu,tray,Tip, 计时器
Menu,Tray,Add,E&amp;xit,guiclose

Gui,Show, W200 H115 Center,定时器
Gui,Add,Button,Default x80 y85 w40 h22 gtimer,计时
Gui,Add,Text,x5 y5 w180,事由
Gui,Add,Edit,x5 y20 w190 vreason
Gui,Add,Text,x5 y45 w180,时间[单位:秒]
Gui,Add,Edit,x5 y60 w190 vtime
return

timer:
gui,hide
Gui Submit,nohide
time := time*1000
sleep, %time%
MsgBox,,定时警告,%reason%,3600
gosub guiclose

guiclose:
ExitApp
```

<!-- ##{"timestamp":1289186736}## -->