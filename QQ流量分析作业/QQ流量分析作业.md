1.首先保证手机和PC处于同一网络中。
![[p1.jpg]]
![[p2.jpg]]
![[p3.jpg]]
2.打开wireshark,选择WLAN,开始抓包。
3.用手机给PC发送数张图片。
![[p4.jpg]]
4.停止抓包，过滤器输入“ip.addr == 自己手机ip地址”，
![[p5.jpg]]
获得与ip相关的流量,并由右下角知道QQ传输数据是TCP协议。
5.找到一个传输协议为HTTP的包,并有（JEPG JFIF image）,右键->追踪流->TCP Stream.
![[p6.jpg]]
![[p7.jpg]]
6.在新建窗口下面选择原始数据，并另存为
![[p8.jpg]]
又由下图知QQ传输为密文
![[p9.jpg]]
7.将新保存的原始数据文件导入010Editor,得到：
![[p10.jpg]]
8.查找FF十六进制字节，然后找到FF D8 FF，
![[p11.jpg]]
把前面的字节全部删除，另存为为jpg文件，得到传输的原始图片。
![[picture-origin.jpg]]
![[Snipaste_2026-10-25_15-55-09.jpg]]