&emsp;&emsp;刚才大约十分钟以前，点击任何链接，均指向一个“Windows XP 安全更新程序 (KB929969)”页面，刷新后正常，但首次访问必然被劫持，第一反应是被万恶的猥琐ISP玩儿劫持了。然后尝试用IP直接访问网站，发现无碍，基本判断是dns出了问题[坚持标题党-_-!!!]，更换联通自己的dns服务器到Google的8.8.8.8，一切症状消失。

&emsp;&emsp;此次具体表现为：

- 1：国内外任何网站首次访问被劫持，刷新后正常
- 2：不是一般的访问转向，因为补丁无法下载
- 3：更换DNS服务器后，问题得到解决
- 4：应该与Jasmine无关，因为不具有针对性

&emsp;&emsp;截图如下

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213125819008.png>`

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213125833111.png>`

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213125849059.png>`

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213125910963.png>`

### 2011-02-22 14:37更新

&emsp;&emsp;半个小时后问题严峻了，只开启远程dns能解析正确，首页正确，但一切下载均被替换。比如柴子刚才找的巨盾补补和xuetr最新版，下载后解压，均为某274K小程序，因为是在店里，手头没有HIPS，未作行为分析跟进。手动用ark查看了一下，本机无碍[还没傻逼到运行该程序]。

&emsp;&emsp;目前症状如下：

- 1：仅开启远程DNS解析，页面正确，但下载被替换。比较智能化的是，下载后文件名不变，下载的rar和压缩包内文件名不变，但压缩包内仅一exe文件，命名为setup.exe

- 2：该样本文件信息如下：

> 大小: 280620 字节
> 修改时间: 2011年2月22日, 12:11:12
> MD5: 5E91FF55DC270D00DA95FBE7B2745216
> SHA1: BEEE3BAA3E6F9505AAA4D221E066603B1891698B
> CRC32: 68AB0A95

- 3：开启远程dns解析+全局ssh或者直接开启VPN全局，一切正常

&emsp;&emsp;初步判断是联通机房除了问题，比如机房arp神马的，哈哈，很欢乐的一天，已经给联通的朋友打电话反馈-_-!!!

<!-- ##{"timestamp":1298359536}## -->