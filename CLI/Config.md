# 配置 #
## 配置KEY ##


    jdc configure add --profile default --access-key your-ak --secret-key your-sk


根据提示输入access-key、secret-key即可配置完成，其它项为可选项。

资源所在区域region-id默认值为cn-north-1。

网关地址endpoint默认值为www.jdcloud-api.com。

协议scheme默认值为https（为了保障安全，建议使用https）。

以上信息将被保存到home目录的~/.jdc/config文件中。