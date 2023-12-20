网上很多frida hook的例子不再多说，有几点注意

*新版本app会检测frida，需要改名改端口，否则frida会自动退出*

*android 必须root，否则启动不了frida*

**frida的操作步骤如下：**

假设你已经将frida 放到android 的/data/local/tmp 目录下 ，并且改名为fs167（因为frida版本更新太快，我这里用的16.7）

1. adb -s xxx shell (adb连手机shell)
2.  cd /data/local/tmp
3. su
4. ./fs167 -l 127.0.0.1:9999（端口随意，下一步对应一致）
5. 另起cmd窗口做端口转发，adb forward tcp:9999 tcp:9999
6. frida -H 127.0.0.1:9999 -f com.jingdong.app.mall -l index.js（index.js为你的hook文件）



----

我是用的数据线连接的adb，想用wifi 连接一直报错，网上找的方法如下可用。但是有很大问题，这个操作要手机先连数据线，而且手机重启后还得再次设置。总之鸡肋~

后来从google 文档看到低版本的android就是不支持adb的wifi连接。别白费心思了。

[Android 调试桥 (adb)  | Android 开发者  | Android Developers (google.cn)](https://developer.android.google.cn/studio/command-line/adb?hl=zh-cn)

```
adb shell

setprop service.adb.tcp.port 5555

exit

adb tcpip 5555 

adb connect 192.168.2.176
```

