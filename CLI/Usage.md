
# 使用说明

## 前置条件

### 鉴权AccessKey和SecretKey

与京东云Open API一样，使用京东云CLI，需提前申请AccessKey和SecretKey，用户的AccessKey和SecretKey信息由用户中心统一维护，京东公有云各业务线共用密钥对(基础云、数据云等)；

密钥对允许启用、禁用，启用后可用其调用CLI，禁用后不能用其调用CLI；

密钥对涉及主子账号功能，由用户自己申请的密钥对属于主密钥对，可用于操作自己账号下的所有资源。由用户给子账号申请的密钥对属于子密钥对，用于子账号操作主账号下的已授权资源。

### 京东云Python SDK

目前CLI依赖京东云Python SDK，但在CLI的安装过程中会自动安装依赖。如果因为版本不对应导致CLI不能正常运行等问题，需要手动安装Python SDK，请参考“常见问题“中的安装方法。

### 京东云CLI和Python SDK版本对应表

发布日期	|	京东云CLI	|	京东云Python SDK
:---|:---|:---
2018.07.19  	|	0.3.0	|	1.2.0
2018.06.25	|	0.2.1	|	1.1.2
2018.06.23	|	0.2.0	|	1.1.1
2018.06.04	|	0.1.0	|	1.1.1



## 结构模型


	jdc [options] <command> <sub-command> [parameters and help]
options：全局选项，包括help、debug、quiet、output格式等

command：云产品服务与工具命令

sub-command：对应OpenAPI接口，格式为小写加中划线

parameters and help：sub-command 中输入的操作所对应的参数列表。该参数列表的顺序不会对命令的使用产生影响。参数可采用各种类型的输入值，如数字、字符串、JSON 结构。





## 输入参数

输入参数支持三种形式：

标准CLI，操作参数格式为小写加中划线，参数名前带--（比如：--name）

如：


	jdc nc describe-container --container-id c-8b23fwsb22



json格式的参数，OpenAPI的POST或PUT请求，支持直接输入json串或指定本地文件两种子形式

如：

a) 直接指定json串


	jdc nc create-container --input-json
	'{
	    "maxCount": 1,
 	   "containerSpec":
	    {
        //此处省略具体字段，详情请参考示例章节
	    }
	}'

b) 指定json文件


	jdc nc create-container --input-json 'file:///root/create.json'



标准CLI和json的混合格式，包含标准CLI格式和json格式的参数（或者文件）

如：


	jdc nc exec-create --container-id c-4rdi9c1jw3 --input-json '{"command": ["/bin/sh"]}'

 如图所示，是创建云主机时具体的输入参数帮助界面，在这里解释一下需要注意的地方。



输入-h或--help即可得到此界面。Usage中使用中括号括起来的参数是可选参数，反之是必选参数。每个参数的help中开始部分小括号中是参数类型，复杂类型（如instanceSpec）可以使用json方式输入，也可以使用统一的input-json参数输入。复杂类型内的具体字段可以使用各产品下的generate-skeleton命令生成，还可以参考京东云官方线上文档OpenAPI文档：https://www.jdcloud.com/help/faq?act=3。



注意：

简单参数如整数和字符串，且中间无空格可以不用引号括起来。复杂参数如json参数，必须使用单引号括起来，以和json串中的双引号区分。

如果具体操作命令中没有输入region-id参数，默认会使用Profile中配置的region-id值。

如果需要设置额外的header，例如要调用开启了MFA操作保护的接口，需要传递x-jdcloud-security-token，则按照如下方式：


	jdc nc delete-container --headers '{"x-jdcloud-security-token":"xxx"}' --container-id xxxxx

     




## 输出结果

调用CLI服务后返回数据采用统一格式（与对应OpenAPI服务返回格式相同），返回的HTTP状态码为2xx，代表调用成功；返回4xx或5xx的HTTP状态码代表调用失败。

成功调用CLI后返回的数据采用统一格式，格式为json，由请求参数中的output确定，默认为json格式，目前版本仅支持返回json格式的数据；

返回结果需要固定包含requestId属性。成功的操作如有返回数据，需封装在result对象中。操作失败时需要在返回数据中提供error对象。error对象的定义见错误码定义。部分成功的操作需要同时返回result和error对象。

返回结果示例：

成功情况   


	{
    "result": {
        "instances": [Instance],
        "totalCount": 5
        },
    "requestId": " bc8gf89in0boc7bejvbikfecigrf3v1n"
	}

     

失败情况


	{
    "requestId":" bc8gf89in0boc7bejvbikfecigrf3v1n",
    "error": {
        "code": 429,
        "message": "Out of resource quota",
        "status": "QUOTA_EXCEEDED",
        "details": [
        {
           "xxx": xx
        }
        ]
    }
	}




## 交互式命令

目前支持容器产品的两个交互式命令：attach和exec-start。



- attach

命令示例：


	jdc nc attach --container-id c-afeqy1jcnb

命令说明：可以attach到一个已经运行的容器的stdin，然后进行命令执行的动作。执行Enter键，当前界面为命令执行界面，例如输入ls，显示目录列表。

需要注意的是，对从stdin输入的命令，是依赖容器的command/args进程。当command/args是/bin/sh时候，exit会导致sh的退出，进而使容器停止。必须使用退出快捷键Ctrl+PQ退出attach。如果容器异常退出了，可以尝试使用start-container命令重新启动容器。



 

- exec-create

命令示例：


	jdc nc exec-create --container-id containerid --input-json '{"command": ["/bin/sh"] , "tty":true}'

命令说明：创建执行环境





- exec-start

命令示例：


	jdc nc exec-start --container-id containerid --exec-id execid

命令说明：对容器内部执行上述创建的命令



注意：Windows平台中，容器交互命令为exprimental阶段。在命令前需要增加winpty前缀，如：


	winpty jdc nc attach --container-id c-abcdefg

建议使用Linux 或 Mac平台。



## Skeleton生成

每个产品命令下都有一个generate-skeleton子命令，用于生成某个子操作的输入参数骨架，即空的json串。用户可以将复杂的输入参数json串复制到文件中存储，根据OpenAPI文档中标识的参数必选、可选信息填充具体参数，再使用--input-json ‘file://xx/x.json’方式创建或修改资源。

OpenAPI文档：https://www.jdcloud.com/help/faq?act=3


 
## 多用户使用



如上图所示，可以使用jdc configure命令配置多套Profile，区分不同用户。每个Profile有相应的名称，可以使用use子命令进行切换。

注意：

AccessKey和SecretKey均以明文存储，注意安全

当前使用的Profile不能删除

添加Profile时不能重名
