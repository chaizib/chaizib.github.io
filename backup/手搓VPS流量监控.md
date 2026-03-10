> **起因：安卓党的自救**
> 搬瓦工iOS上的BWHbox挺好用，但移动端体验一直差点意思。作为“流量焦虑症”玩家，必须随时掌握流量动态，不然本博客和图片将不够挥霍了。与其在浏览器里手忙脚乱的访问官网，不如自己手搓一个全链路加密的监控看板。

### 1. 架构之争：为什么抛弃 HTML，死磕 PHP？
初学者喜欢用 index.html + JavaScript 调 API。但在 Web 世界里，这叫“裸奔”。

- 风险：HTML/JS 是前端执行。别人按个 F12，你的 API_TOKEN 就像写在脸上的秘密。
- 对策：选用 PHP 后端渲染。API Key 锁在服务器（Server-side）内存里。服务器去取经，用户只看结果。

### 2. 守门人：Nginx 加固配置
在 Debian 12 上，我们要把 Nginx 调教得滴水不漏。
路径： /etc/nginx/sites-enabled/your-site-config
```Nginx
server {
    listen 443 ssl http2;
    server_name your-domain.com; # 替换为你的域名
    root /var/www/your-project-path;

    index index.php;

    # 【加固】禁止探测任何隐藏文件（如 .git, .env）
    location ~ /\.(?!well-known) { 
        deny all; 
    }

    # 【核心】对接 PHP 处理器并防源码泄露
    location ~ \.php$ {
        # 如果 PHP 进程挂了，直接 404，严禁将源码作为文本下载
        try_files $uri =404; 
        
        include snippets/fastcgi-php.conf;
        # 这里的版本号需根据你安装的 PHP 版本（如 7.4 或 8.2）调整
        fastcgi_pass unix:/run/php/php7.4-fpm.sock; 
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

### 3. 大脑：PHP 高精度倒计时逻辑
文件： index.php
我们要实现“离重置还剩 X天 X时 X分”，这种读秒的快感才是极致追求。
```php
<?php
// --- 核心配置：API 密钥锁定区（绝对不出服务器） ---
$servers = [
    [
        'name' => '博客所在VPS',
        'veid' => '1234567', // 替换为你的 VEID
        'key'  => 'private_YOUR_API_KEY_HERE', // 替换为你的 API KEY
        'total'=> 1000 // 流量总量 GB
    ]
];

function fetch_bwh_data($veid, $key) {
    $url = "https://api.64clouds.com/v1/getServiceInfo?veid=$veid&api_key=$key";
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false); // 解决部分环境 SSL 握手问题
    $res = curl_exec($ch);
    return json_decode($res, true);
}

// 核心算法：计算倒计时
$diff = $data['data_next_reset'] - time();
$d = floor($diff / 86400);
$h = floor(($diff % 86400) / 3600);
$m = floor(($diff % 3600) / 60);
?>
```
### 4. 颜值：带“蓝色竖纹”的 UI 设计
为了让看板看起来像“工业级监控”，左侧的一道蓝色侧边条是视觉灵魂。
```css
/* 专属侧边纹样式 */
.card {
    background: #fff;
    border-radius: 20px;
    border-left: 5px solid #3b82f6; /* 这道蓝纹就是格调 */
    box-shadow: 0 10px 25px rgba(0,0,0,0.05);
    padding: 26px;
}

/* 红色倒计时数字 */
.days-red {
    color: #ef4444; /* 醒目红，增加危机感 */
    font-weight: 800;
}
```
### 5. 避坑结案陈词（安全建议）

1. Token 隔离：代码里的 API_KEY 只要不分享、不提交到 GitHub，它就是绝对安全的。
2. 重置密钥：如果你在调试过程中（没配好 PHP 时）不小心让源码在浏览器显示过，请务必去后台重置 API Key！旧钥匙必须作废。
3. SSH 安全：既然 Key 锁在服务器里，那么保护好服务器的 SSH 密码就是最后的底线。


