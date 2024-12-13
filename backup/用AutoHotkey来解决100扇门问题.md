> 100 doors：————VIA:Rosetta Code
> Problem:You have 100 doors in a row that are all initially closed. You make 100 passes by the doors. The first time through, you visit every door and toggle the door (if the door is closed, you open it; if it is open, you close it). The second time you only visit every 2nd door (door #2, #4, #6, ...). The third time, every 3rd door (door #3, #6, #9, ...), etc, until you only visit the 100th door.
> Question: What state are the doors in after the last pass? Which are open, which are closed?

&emsp;&emsp;有100扇关闭的门，然后改变开关门状态[门开着则关闭，门关闭则打开]，第一次改变所有门的状态[打开所有门]，第二次改变2的倍数所有门的状态，第三次改变3的倍数所有门的状态，依此类推，直到第100次为止。问到最后，哪些门是开着的？

### 标准解法一：

```
Loop, 100
Door%A_Index% := "closed"

Loop, 100 {
x := A_Index, y := A_Index
While (x <= 100)
{
CurrentDoor := Door%x%
If CurrentDoor contains closed
{
Door%x% := "open"
x += y
}
else if CurrentDoor contains open
{
Door%x% := "closed"
x += y
}
}
}

Loop, 100 {
CurrentDoor := Door%A_Index%
If CurrentDoor contains open
Res .= "Door " A_Index " is open`n"
}
MsgBox % Res
```

### 风骚解法2：

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213133354204.png>`

```
increment := 3, square := 1
Loop, 100
If (A_Index = square)
outstring .= "`nDoor " A_Index " is open"
,square += increment, increment += 2
MsgBox,, Succesfull, % SubStr(outstring, 2)
```

### 经典解法3：

```
While (Door := A_Index ** 2) <= 100
Result .= "Door " Door " is open`n"
MsgBox, %Result%
```

<!-- ##{"timestamp":1305962736}## -->