&emsp;&emsp;作者：username 出处：http://hipschina.com/thread-2744-1-1.html

&emsp;&emsp;达到和ubuntu一样在复制文件或文件夹后粘贴时，如果是编辑框就粘贴路径，其它地方就照常粘贴，看图：

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213122022957.gif>`

&emsp;&emsp;AutoHotkey脚本代码如下：

```
^v::goto pastex
return

pastex:
ControlGetFocus,OutputVar,A
if ErrorLevel
gosub sendctrlv
else
{
OutputVar:=RegExReplace(OutputVar,"[0-9]")
if OutputVar=edit
gosub sendcliptext
else
gosub sendctrlv
}
return

sendctrlv:
Suspend,on
Send ^v
Suspend,off
return

sendcliptext:
ClipSaved:=ClipboardAll
clipboard=%clipboard%
gosub sendctrlv
Clipboard:=ClipSaved
ClipSaved=
return
```

<!-- ##{"timestamp":1290914736}## -->