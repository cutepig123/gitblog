# [sockscap代理不支持代理的软件](https://github.com/cutepig123/gitblog/issues/27)

要求
windoes平台
原先我有一些程序，但是他们不支持代理。如何让他们也能用？
这个代理工具最好支持多个代理，首先通过p单的，然后再经过一个专有代理，比如shadowsocks实现加密

找到的工具
proxifier 缺点是收费

sockscap64 缺点是不能链式代理

proxycap 缺点是需要重啟電腦，估计他主要管理员权限

freecap 测试没成功

使用这类软件不能连接localhost，我怀疑localhost之类的不会经过dns解析，所以他的远程解析失效了？

todo

- [ ] 做一个基于detours的类似于sockscap工具，感觉只需要hook connect就行了

