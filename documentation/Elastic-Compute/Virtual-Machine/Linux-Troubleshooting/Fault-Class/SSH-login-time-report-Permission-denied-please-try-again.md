# SSH登录时报Permission denied, please try again




注意：本文相关 Linux 配置及说明已在 CentOS 6.5 64 位操作系统中进行过测试。其它类型及版本操作系统配置可能有所差异，具体情况请参阅相应操作系统官方文档。



**问题现象**

当使用 SSH 登录Linux 云主机时，如果是 root 用户，即便正确输入了密码，也会出现类似如下错误信息。

*• Permission denied, please try again.*

• SSH 服务器拒绝了密码，请再试一次。

但非root用户可以正常登录，而且root用户通过 VNC 登录也正常。



**问题原因**

服务端SSH 服务配置了禁止root用户登录策略。



**处理办法**

说明：相关策略可以提高服务器的安全性。请用户基于安全性和易用性权衡后，再确定是否需要修改相关配置。

要解决此问题，请进行如下配置检查和修改：

1.通过 VNC 进入系统。

2.通过 cat 等指令查看 /etc/ssh/sshd_config 中是否包含类似如下配置：


*PermitRootLogin no*

参数说明：

• 未配置该参数，或者将参数值配置为 yes （默认情况），都允许 root 用户登录。只有显示的设置为 no 时，才会阻断 root 用户登录。

• 该参数只会影响用户的 SSH 登录，不影响用户通过 VNC 等其它方式登录系统。



3.如果需要修改相关策略配置，在继续之前建议进行文件备份。

4.使用 vi 等编辑器，将参数值设置为 yes，或者整个删除或注释（在最开头添加 # 号）整行配置。比如：

*# PermitRootLogin no*

5.使用如下指令重启 SSH 服务：


*service sshd restart*

6.尝试再次使用 root 用户登录服务器。



如无法解决您的问题，请向我们提工单。
