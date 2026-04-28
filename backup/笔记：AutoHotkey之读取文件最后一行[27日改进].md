&emsp;&emsp;在AutoHotkey中，可以使用fileread读取一个文件的内容给一个变量，借助loop按`n分割来逐行读取，或者使用filereadline读取指定行号，但是问题出来了，在帮助文件中没有找到直接读取文件的最后一行的命令。想了一会，可以曲线实现：循环读到最后一行；指定到最后一行，读取该行『以1.txt为例』

```
;循环读到最后一行I
Loop, read, 1.txt
last_line := A_LoopReadLine
MsgBox "%last_line%"
return
;循环读到最后一行II
fileread, nr, 1.txt
loop,parse, nr, `n, `r
{
last_line := A_loopField
}
msgbox, "%last_line%"
return
;直接读取最后一行
FileRead, fileContent, 1.txt
last_line := SubStr(fileContent, InStr(fileContent, "`n", False, 0))
MsgBox "%last_line%"
Return
```

&emsp;&emsp;呵呵，测试了一下，有效，这样的话就可以很舒服的直接屏蔽农牧偷匪外挂的弹出广告了『羞愧：玩QQ农场牧场可耻，用外挂更可耻』，部分代码如下：

```
Checkhosts: ;直接读取hosts最后一行，有则跳过无则添加
FileRead, fileContent, %SYSTEMROOT%\system32\drivers\etc\hosts
last_line := % SubStr(fileContent, InStr(fileContent, "`n", False, 0))
{
if last_line=`n127.0.0.1 www.qqceo.net
Gosub rungame
else
gosub hosts
}
return

hosts:;修改hosts文件，添加广告网址屏蔽
FileAppend,
(
`n127.0.0.1 www.nn47.cn
127.0.0.1 www.qqceo.net
),%SYSTEMROOT%\system32\drivers\etc\hosts
gosub rungame
Return

rungame: ;启动偷匪外挂
run qqnmtf266.exe
Return
```

&emsp;&emsp;吐槽：WordPress自带的排版真的很难搞，脚本源码看起来真那啥，求推荐-_-!!!

#### 27日更新：

&emsp;&emsp;前面所写的Checkhosts部分有个问题，如果广告网址屏蔽已经存在于hosts文件的非最后一行，会导致重复『感谢ss指出和帮助』修改如下：

```
;读取hosts全文检查是否已屏蔽广告网址，有则跳过无则添加
Checkhosts:
filename = %SYSTEMROOT%\system32\drivers\etc\hosts
host1 = 127.0.0.1 www.qqceo.net
host2 = 127.0.0.1 www.nn47.cn
FileRead, fileContent, %filename%
IfNotInString, fileContent, %host1%
FileAppend, `n%host1%, %filename%
IfNotInString, fileContent, %host2%
FileAppend, `n%host2%, %filename%
else
gosub rungame
return
```

<!-- ##{"timestamp":1290828336}## -->