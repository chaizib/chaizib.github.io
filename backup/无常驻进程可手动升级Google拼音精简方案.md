&emsp;&emsp;Google拼音是[柴子](https://chaizi.cc/)一向很欣赏的一款输入法『不会五笔的再次潸然泪下T.T…』，相比搜狗和QQ来说更偏向纯输入法，没有乱七八糟的功能，比如什么截屏啊发微博啥的，长句很精准，智能联想效果不错，日用聊天常规文档写作基本无碍。不过缺点也很明显：没有直接辅助码『拼音加加大爱』，已存词组不能缺省联想『必须要bairiyishanjin=白日依山尽，拼音加加只需bairiyis=白日依山尽』

&emsp;&emsp;Google的一贯特色是不能自定义安装，并且有常驻后台进程，这一点是很让人不爽的，在此提供一个比较方便小白的精简办法『用最没有技术含量的手段来解决问题，剽窃飘MM的签名档』

### 小白精简办法：

1. 直接去Greendown下载免安装[Google拼音](http://www.greendown.cn/soft/6292.html)，达到自定义安装目录的目的 
2. 记事本打开%systemroot%\system32\drivers\etc\hosts，添加 74.125.153.113 clients2.google.com
3. 运行@绿化工具.exe安装，在设置中登录gmail帐号并勾选自动同步两个选项
4. 注册表HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run删除"Google Pinyin 2 Autoupdater"，然后精简安装目录文件如下列表

### 精简后的安装目录文件：

保留文件：

- Google Pinyin2
- │  @绿化工具.exe
- │  bihua.00000
- │  component.00000
- │  control.bin
- │  english.00000
- │  GooglePinyinDaemon.exe
- │  GooglePinyinDictionary.exe
- │  GooglePinyinOptions.exe
- │  index.00000
- │  model.00000
- │  stock_shuangpin_dict.00000
- │  sysbitmap.00000
- │  sysdict.00000
- ├─delta
- └─Extensions
- ....└─base.lua

&emsp;&emsp;手动升级系统词典版本：
&emsp;&emsp;cd到安装目录，带参数运行GooglePinyinDaemon.exe update_now

&emsp;&emsp;手动同步用户词库和设置：
&emsp;&emsp;cd到安装目录，带参数运行GooglePinyinDaemon.exe sync_now

<!-- ##{"timestamp":1289013936}## -->