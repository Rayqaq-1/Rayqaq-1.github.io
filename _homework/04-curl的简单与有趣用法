---
title: "curl 的简单与有趣用法"
---

curl（Client URL）是一个强大的命令行工具，用于在 Linux/Unix 系统中传输数据。它支持多种协议，包括 HTTP、HTTPS、FTP、SFTP 等，几乎所有和后端、运维、网络打交道的场景里，都能见到它的身影。

## curl 的主要特点

| 特点 | 说明 |
| --- | --- |
| 多协议支持 | 支持 HTTP、HTTPS、FTP、SFTP 等几乎所有主流网络协议 |
| 无界面操作 | 纯命令行工具，天然适合脚本和自动化任务 |
| 功能丰富 | 文件上传下载、表单提交、Cookie 处理一应俱全 |
| 跨平台 | Linux、macOS、Windows 上都能使用 |

> 小提示：Windows PowerShell 5.1 里 `curl` 其实是 `Invoke-WebRequest` 的别名，行为与真正的 curl 并不相同。想用原版，请写 `curl.exe`，或者直接使用 PowerShell 7+。

## 一、curl 的简单用法

### 1. 获取网页内容

想看看某个网页返回的“原始内容”？在终端里请求它就行。这里以必应（cn.bing.com）为例：

```bash
curl http://cn.bing.com
```

回车之后，整页 HTML 就会刷屏式地打印在终端里：

![图 1]({{ site.baseurl }}/assets/images/curl/curl-1.png)

从这段输出里，可以直接读到必应网页的标题和描述，比如：

> 使用 Microsoft 必应进行搜索，并利用 AI 的强大功能查找浏览网页、图像、视频、地图等。为永远充满好奇心的人提供的智能搜索引擎。

这些文字正来自 HTML 里的 `<title>` 和 `<meta name="description">`。也就是说，curl 拿到的是网页的“原材料”，浏览器只是把这份原材料渲染成了我们熟悉的页面。

### 2. 测试网站响应时间

curl 还能顺手当个简易的测速工具。这里以抖音（www.douyin.com）为例：

```bash
curl -o /dev/null -s -w "Connect: %{time_connect} TTFB: %{time_starttransfer} Total: %{time_total}\n" http://www.douyin.com
```

几个参数的含义：

- `-o /dev/null`：把响应体直接丢弃，不打印到屏幕（Windows 下可写成 `-o NUL`）
- `-s`：静默模式，不显示进度条和错误信息
- `-w`：请求结束后，按指定格式输出统计信息

执行结果如下：

![图 2]({{ site.baseurl }}/assets/images/curl/curl-2.png)

| 指标 | 含义 | 本次结果 |
| --- | --- | --- |
| `time_connect` | TCP 连接建立耗时 | 0.0368 s |
| `time_starttransfer` | 首字节时间（TTFB），服务器开始返回数据的时刻 | 0.0660 s |
| `time_total` | 整个请求的总耗时 | 0.0660 s |

可以看到，这次请求的总耗时约为 **0.066 秒**，网络状况相当不错。由于响应体很小（大概率只是一次重定向），TTFB 与总耗时几乎一致。

## 二、AI 告诉我的有趣玩法

### 1. 在终端里看天气

```bash
curl wttr.in/Guangxi
```

![图 3]({{ site.baseurl }}/assets/images/curl/curl-3.png)

wttr.in 会把天气预报渲染成 ASCII 字符画，包含当前温度、风速、能见度、降水量，以及未来三天的分时段预报。上图是广西（Guangxi）的天气：多云，气温 19°C，风速 11 km/h，能见度 10 km。

几个常用的小技巧：

- `curl wttr.in/Guangxi?0`：只看当前天气
- `curl wttr.in/Guangxi?format=3`：只输出一行简版天气
- `curl wttr.in/Guangxi?lang=zh`：用中文显示
- 把 `Guangxi` 换成任意城市名即可查其他地区

### 2. 把文字变成二维码

```bash
curl qrenco.de/hhx
```

![图 4]({{ site.baseurl }}/assets/images/curl/curl-4.png)

终端里直接“画”出一个二维码，手机扫一扫就能拿到对应的内容。原理很简单：qrenco.de 会把路径里的文字编码成二维码，再用 Unicode 方块字符拼出来显示。

把 `hhx` 换成任意内容即可生成自己的二维码；如果内容里含有特殊字符，记得先做 URL 编码。

## 三、小结

以上便是 curl 的一些简单和有趣的用法。除此之外，它还有不少值得一试的参数：

- `-I`：只查看响应头
- `-L`：自动跟随重定向
- `-X POST -d "k=v"`：发送 POST 请求
- `-H "Key: Value"`：自定义请求头
- `-b` / `-c`：读写 Cookie
- `--limit-rate 1M`：限制下载速度
- `--resolve`：把域名强行解析到指定 IP

一条命令、一个请求，简单直接。curl 从上世纪 90 年代诞生至今仍然活跃，靠的正是这种“够用、好用、随处可用”的气质。
