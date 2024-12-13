&emsp;&emsp;刚才去广海，看到几个老帖，囧，话说最近很少去广海挖东西了，论坛全是求代码… 一些牛人少了，于是能挖到的好东西也就相应少了。有些感慨，如果没有广海偶们菜鸟怎么办？怎么办！

&emsp;&emsp;先来[mfm11111]贴出的喊话call：

```
//走路状态标识函数
void walk3(float x,float y)
{
/*  
二.走路分析：

1.用OD对05393EF0进行写入
053924F8+19f8代表X轴，后面依次代表H，Y轴
2.对当前坐标进行写入
053924F8+24ec代表X轴，后面依次代表H，Y轴

0046f544：mov [EBX+1A10]，0或1
[EBX+1A10]//跑步置1
[EBX+1A14]//跑步置1
*/

float xhy[3];
xhy[0]=x;
xhy[1]=300;
xhy[2]=y;
_asm
{
//  053924F8+19f8代表X轴，后面依次代表H，Y轴
mov ebx,0x053924F8
add ebx,0x19f8
mov eax,x
mov [ebx],eax
mov eax,y
mov [ebx+8],eax
//053924F8+24ec代表X轴，后面依次代表H，Y轴
mov ebx,0x053924F8
add ebx,0x24ec
mov eax,x
mov [ebx],eax
mov eax,y
mov [ebx+8],eax
//[EBX+1A10]//跑步置1
mov ebx,0x053924F8
mov byte ptr [ebx+0x1A10],1
//[EBX+1A14]//跑步置1
mov ebx,0x053924F8
mov byte ptr [ebx+0x1A14],1
}
}

//第一次找的走路CALL，但单独注入后不行，需要与后面的判断标识同时使用
void walk4(float xhy[3])
{
float x,h,y;
//float xhy[3];
x=xhy[0];
y=xhy[2];
h=xhy[1];
//xhy[2]=y;

_asm
{
mov ecx,0x053924F8
push 2
sub esp,0x0c
mov edx,esp
mov edi,x
mov [ecx+0x24ec],edi
mov [edx],edi
mov edi,h
mov [ecx+0x24f0],edi
mov [edx+4],edi
mov edi,y
mov [ecx+0x24f4],edi
mov [edx+8],edi
mov eax,0x0046d780
call eax
}
}

最后是调用这两个函数即可：
void CWGForm::OnButton3()
{
//点击右键后才走路
float xhy[3];
xhy[0]=53;
xhy[1]=-300;
xhy[2]=609;
//经测试，walk1和walk2都是按右键才走路
walk3(xhy[0],xhy[2]);//此函数是判断状态识别走路
walk4(xhy);//走路CALL
}
```

&emsp;&emsp;[min7229[min722922]发的热血喊话call：

```
------------------------   只要改变聊天框的内容就会 调用
0043DAE0  |.  8B45 0C       mov eax,[arg.2]
0043DAE3  |.  57            push edi                                          ;  Client.004F0001
0043DAE4  |.  50            push eax
0043DAE5  |.  8BCE          mov ecx,esi
0043DAE7  |.  E8 94040000   call Client.0043DF80
---------------------------------------------------------------------------
喊话执行的第一个CALL
0043DFF2  |.  8B8B 2C030000 mov ecx,dword ptr ds:[ebx+32C]
0043DFF8  |.  52            push edx
0043DFF9  |.  52            push edx
0043DFFA  |.  68 ED030000   push 3ED
0043DFFF  |.  8B01          mov eax,dword ptr ds:[ecx]
0043E001  |.  FF50 04       call dword ptr ds:[eax+4]
--------------------------------------------------------------------
0043C135  |.  8B16          mov edx,dword ptr ds:[esi]                        ;  Client.008B1E48
0043C137  |.  57            push edi
0043C138  |.  53            push ebx
0043C139  |.  68 ED030000   push 3ED
0043C13E  |.  8BCE          mov ecx,esi
0043C140  |.  FF52 04       call dword ptr ds:[edx+4]

00586DB3  |.  8B45 10       mov eax,[arg.3]                                   ;  2
00586DB6  |.  8B4D 0C       mov ecx,[arg.2]
00586DB9  |.  8B13          mov edx,dword ptr ds:[ebx]
00586DBB  |.  50            push eax
00586DBC  |.  51            push ecx
00586DBD  |.  68 ED030000   push 3ED
00586DC2  |.  8BCB          mov ecx,ebx
00586DC4  |.  FF52 04       call dword ptr ds:[edx+4]

005F842C  |.  8B45 10       mov eax,[arg.3]                                   ;  Case 3ED of switch 005F7CBB
005F842F  |.  83F8 0D       cmp eax,0D
005F8432  |.  75 76         jnz short Client.005F84AA
005F8434  |.  8BCE          mov ecx,esi
005F8436  |.  E8 A52D0000   call Client.005FB1E0
----------------------------------------------------------------------------------------------------
005FB542  |> \C6840D 91D5FF>mov byte ptr ss:[ebp+ecx-2A6F],0
005FB54A  |.  8A85 90D5FFFF mov al,byte ptr ss:[ebp-2A70]
005FB550  |.  FEC0          inc al
005FB552  |.  8D95 74D5FFFF lea edx,[local.2723]
005FB558  |.  8885 90D5FFFF mov byte ptr ss:[ebp-2A70],al
005FB55E  |.  0FBEC0        movsx eax,al
005FB561  |.  8D48 17       lea ecx,dword ptr ds:[eax+17]
005FB564  |.  83C0 1D       add eax,1D
005FB567  |.  66:898D 78D5F>mov word ptr ss:[ebp-2A88],cx
005FB56E  |.  8B0D F8E08A01 mov ecx,dword ptr ds:[18AE0F8]
005FB574  |.  50            push eax
005FB575  |.  52            push edx
005FB576  |.  E8 9539E5FF   call Client.0044EF10                发包

-----------------------------------------------------------
先把    聊天的内容写入内存  [18AF408]+13C      然后在调用

mov ebx,[018af408]
mov ecx,dword ptr ds:[ebx+32C]
push 0d
push 0d
push 3ed
mov eax,dword ptr ds:[ecx]
call dword ptr ds:[eax+4]
```

<!-- ##{"timestamp":1293161136}## -->