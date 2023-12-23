# sign生成方式

目前已知的有两种方式，python的和java的。github上都能找到。

原理大致如下 [[原创\]记一次unicorn半自动化逆向——还原某东sign算法-Android安全-看雪-安全社区|安全招聘|kanxue.com](https://bbs.kanxue.com/thread-266377.htm)



---

sign要注意参数，body要与hook出来的完全一致，否则604

1. uuid 要用纯数字的，不是被加密后的，可以抓包抓到
2. body 要注意空格，引号。生成sign的body和请求的body，格式一般是不一样的。

uuid的加密解密也能hook到，参考[手把手教你从Apk中取出算法 - 奋飞安全 (91fans.com.cn)](http://91fans.com.cn/post/getcodeformapk/)

将java代码转换为python代码，可以借助AI来实现。