解决 Charles、Fiddler 等网络代理工具开启 SSL Proxying 后 HTTPS 抓包报错失败等问题。

**很多文章都说要把证书放到system下，但是没有提到证书要用openssl做转换。导致花了不少时间**

**前提条件：**

1.  Android 设备已 root；
2.  Windows 需安装 OpenSSL，下载连接：

**应用场景：**

使用 Charles、Fiddler 等中间人网络代理工具时，通过设备浏览器访问 [chls.pro/ssl](https://link.zhihu.com/?target=http%3A//chls.pro/ssl) 安装证书只在“用户”层，启用“SSL 代理”会因证书不受信导致 https 抓包失败。

**操作步骤：**

1.  打开 Charles 按照下图提示导出证书并保存为“.pem”文件，其他代理工具方法类似；

![](https://pic4.zhimg.com/v2-68e09dafd3ef9ec5de1540a5ad1202af_b.jpg)

2\. 导出证书并保存为扩展名“.pem”或“.cer”文件；

3\. 使用 CMD 或 PowerShell 命令查看证书信息；

“.pem”文件使用：

```text
openssl x509 -subject_hash_old -in cert.pem
```

“.cer”文件使用：

```text
openssl x509 -subject_hash_old -in cert.cer -inform der
```

![](https://pic1.zhimg.com/v2-9d5f41fdb74f9214e24cb524c6ab6190_b.jpg)

3\. 重命名“cert.pem”为“311f0693.0”（查看命令执行后第一行字符串+.0），并将文件“311f0693.0”通过 MT 文件管理器保存至 Android 设备目录“/system/etc/security/cacerts/”下；

4\. OK，系统设置中已系统信任的 Charles 证书。

![](https://pic3.zhimg.com/v2-497806d778bf015ccb4f2a2824533d1a_b.jpg)

模拟器中配置代理ip两种方式 ，二选一结果都一样

1. wifi中直接设置

2. PC上cmd 中adb设置代理

   `adb shell settings put global http_proxy 192.168.2.146:8888`

   `adb shell settings put global https_proxy 192.168.2.146:8888`