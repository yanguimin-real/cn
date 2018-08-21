
# 常见问题

##1. AccessKey、SecretKey如何获取？

请参考京东云OpenAPI帮助页面中“前置条件”小节：https://www.jdcloud.com/help/detail/355/isCatalog/0



##2. 如何选择区域（RegionId）？

请参考京东云OpenAPI帮助页面中“地域编码”小节：https://www.jdcloud.com/help/detail/355/isCatalog/0



##3.CLI命令行是否开源？

京东云CLI是开源的，可以从GitHub下载。地址：https://github.com/jdcloud-api/jdcloud-cli



##4.    返回错误时怎么办？

使用全局option debug打印详细信息，并反馈到京东云CLI的GitHub库的issue中，或在京东云官网提交工单。

示例：

	jdc --debug command sub-command
   

##5.    CLI是否付费？

暂不收费。



##6.    遇到问题时如何反馈和求助？

在京东云控制台提交工单

参考京东云官网联系我们页面提供的方式反馈，地址为：https://www.jdcloud.com/help/detail/129/isCatalog/1

在GitHub提交Issue，地址为：https://github.com/jdcloud-api/jdcloud-cli/issues



##7.    如何安装京东云Python SDK ？

pip安装


	pip install jdcloud_sdk
 该命令安装最新版本，指定版本安装，请参考以下举例。安装CLI时相同，不再赘述。

	pip install jdcloud_sdk==1.1.2
   

源码安装

下载地址：https://github.com/jdcloud-api/jdcloud-sdk-python

解压缩后在项目目录中执行：

	python setup.py install
建议按版本号下载releases中的稳定版本。