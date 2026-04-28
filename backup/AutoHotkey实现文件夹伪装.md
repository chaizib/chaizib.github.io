&emsp;&emsp;继续学着编辑一些很简单的AutoHotkey脚本，嘿嘿。柴子现在貌似有点上瘾，从简单的来，自从ss给了那个加密爆破的玩意之后，现在很多现成编译的文件都能直接看代码。。感觉老外好强… 好强……！

&emsp;&emsp;在BBS上翻老帖，看到有个文件夹伪装的比较好玩，好几年前曾经试过修改desktop.ini来伪装文件夹，嘎嘎，试试用AutoHotkey能不能实现，各种给力，FileAppend是个好命令o。

`Gmeek-html<img src=https://testingcf.jsdelivr.net/gh/chaizia/pic/img/20241213121501924.png>`

&emsp;&emsp;脚本代码如下：

```
#NoTrayIcon
Gui,+ToolWindow<!--more-->
Gui, Add, GroupBox, x6 y12 w220 h88 , 请选择要加密/解密的文件夹
Gui, Add, Edit, x16 y32 w200 h25 Vfilepath, %filepath%
Gui, Add, Button, x16 y62 w60 h25 gchose, 选 择
Gui, Add, Button, x86 y62 w60 h25 glock, 变 身
Gui, Add, Button, x156 y62 w60 h25 gunlock, 还 原
Gui, Show,  h106 w232 Center,-＝文件夹变身/还原『控制面板』＝-
Return

GuiClose:
GuiEscape:
ExitApp

chose:
FileSelectFolder,filepath
GuiControl,,filepath,%filepath%
Return

lock:
gui,submit,nohide
FileAppend,
(
[.ShellClassInfo]
UICLSID={7BD29E00-76C1-11CF-9DD0-00A0C9034933}
CLSID={21EC2020-3AEA-1069-A2DD-08002B30309D}
),%filepath%\desktop.ini
Sleep,10
FileSetAttrib,+SH,%filepath%
FileSetAttrib,+SH,%filepath%\desktop.ini
MsgBox,变身成功！
Return

unlock:
gui, Submit,NoHide
FileSetAttrib,-SH,%filepath%
FileDelete,%filepath%\desktop.ini
MsgBox,还原成功！
Return
```

<!-- ##{"timestamp":1289445936}## -->