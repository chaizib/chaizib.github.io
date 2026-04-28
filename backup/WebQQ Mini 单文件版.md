&emsp;&emsp;狗日的腾讯现在已经把QQ客户端当成杀毒软件来做了，挂钩加驱加服务和买一送一的QQ电脑管家，怎么看都不是一个纯粹的IM通讯工具。当年的webqq倒是小清新了一把，结果和360一掐架，狗日的腾讯自己阉割了。

&emsp;&emsp;更值得吐槽的就是腾讯的封锁和不开放，协议三天两头更换，生怕出现个第三方客户端，mimQQ版本从2到3到4到现在集体沦陷，pidgin到2.9官方直接移除QQ协议，这是腾讯的胜利，然而也是腾讯的悲哀。

&emsp;&emsp;webqq现在已经升级到3.0，不愧为一款耗费cpu和内存的巨作，乱七八糟的的腾讯功能应有尽有，这货已经不仅仅是webQQ了，简直就一个webOS。幸好现在还有一个webqq mini ，但人不可能整天开个网页来挂webqq mini吧。干脆自己动手写一个……

&emsp;&emsp;找到AutoHotkey关于IE内嵌的文档看了半天，发现太麻烦，直接转到AU3，就容易多了，代码如下：

```
#include "ie.au3"
#include <Constants.au3>
#include <GUIConstantsEx.au3>
#include <WindowsConstants.au3>
$Form1 = GUICreate('WebQQ Mini', 500, 470)
$oie = _iecreateembedded()
guictrlcreateobj($oie, 0, 0, 500, 490)
_ienavigate($oie, 'http://w.qq.com')
GUISetState(@SW_SHOW)
Opt("TrayIconHide", 1)
Opt("TrayMenuMode",1)
Opt("TrayOnEventMode",1)
TraySetOnEvent($TRAY_EVENT_PRIMARYUP,"tray")
While 1
Sleep(1)
$nMsg = GUIGetMsg()
Switch $nMsg
Case $GUI_EVENT_CLOSE
Exit
Case $GUI_EVENT_MINIMIZE
GUISetState(@SW_HIDE, $Form1)
Opt("TrayIconHide", 0)
EndSwitch
WEnd
Func tray()
Opt("TrayIconHide", 1)
GUISetState(@SW_SHOW, $Form1)
WinActivate($Form1)
EndFunc
```

`Gmeek-html<img src=https://testingcf.jsdelivr.net/gh/chaizia/pic/img/20241213140327192.png>`

<!-- ##{"timestamp":1312453536}## -->