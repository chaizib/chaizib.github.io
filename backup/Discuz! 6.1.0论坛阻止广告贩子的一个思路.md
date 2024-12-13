### 以下思路和代码提供来自 [天毅](http://gubo.org/)

&emsp;&emsp;注册页面添加一非必须项，回答任意答案均不影响注册成功，但回答正确后用户级别正常，错误则禁言。用来防范广告机的恶意注册【这年头，邮箱验证已经不能阻止广告机的脚步了】发广告。

&emsp;&emsp;以Discuz! 6.1.0为例，代码如下：

**在register.htm的第92行开始插入**
```
<!--验证数值-->
<tr>
<th><label for="ftyear">何时开始使用费尔 *</label></th>
<td>
<input type="number" id="ftyear" name="ftyear" size="25" maxlength="4" value="$ftyear" tabindex="3" /><span>&nbsp;请填入2002年到2011年间的一个4位年份数字，*没有使用费尔请填2011。<font color="red">填写不正确者直接禁言</font></span>
</td>
</tr>
```
**在join.php的第308行插入：**

```
//数字年份判断是否是待审状态,如果填入数字不在2000~2012范围之内，把groupid设置为禁言用户组
$ftyear = (int) $ftyear;
if ($ftyear<2000){
$groupinfo[groupid]=4;
}
elseif ($ftyear>2012){
$groupinfo[groupid]=4;
}
```

<!-- ##{"timestamp":1301729136}## -->