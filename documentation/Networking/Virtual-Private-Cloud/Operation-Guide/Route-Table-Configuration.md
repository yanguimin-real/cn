## **路由表配置**

#### **步骤一、创建自定义路由表**

1. 打开控制台，选择 网络 > 路由表 ，进入路由表列表页；
2. 选择创建路由表所属地域（目前开放华北、华南地域），点击“创建”按钮；
![](/image/Networking/Virtual-Private-Cloud/Operation-Guide/Route-Table-Configuration/Step1.png)

3. 地域选择：在此步骤仍可以选择创建路由表的地域；
![](/image/Networking/Virtual-Private-Cloud/Operation-Guide/Route-Table-Configuration/Step2.png)

4. 选择所属私有网络，路由表必须创建在某个私有网络内。
5. 设置路由表名称：名称不可为空，只支持中文、数字、大小写字母、英文下划线“_”及中划线“-”，且不能超过32字符；
6. 设置路由表描述：描述可以为空，只支持中文、数字、大小写字母、英文下划线“_”，且不能超过256字符；
7. 点击【确定】后即可进入“控制台”查看创建的路由表；
8. 创建路由表后，可进行路由规则配置，也可稍后进入详情页自行配置；

#### **步骤二、关联子网**

1. 打开控制台，选择 网络 > 路由表 ，进入路由表列表页；
2. 点击操作列的“关联子网”：
![](/image/Networking/Virtual-Private-Cloud/Operation-Guide/Route-Table-Configuration/Step3.png)

3. 在弹出的子网选择页面，选择要关联该路由表的子网，可将该路由表关联至同私有网络下的子网：
![](/image/Networking/Virtual-Private-Cloud/Operation-Guide/Route-Table-Configuration/Step4.png)

4. 点击【确定】后即可将路由表关联至子网；


#### **步骤三、修改名称/描述**

   1. 打开控制台，选择 网络 > 路由表 ，点击路由表名称进入路由表详情页；
   2. 点击名称/描述后的修改按钮，即可对路由表名称/描述进行修改，具体的名称/描述规则参见路由表创建；
![](/image/Networking/Virtual-Private-Cloud/Operation-Guide/Route-Table-Configuration/Step5.png)



#### **步骤四、删除路由表**

1. 打开控制台，选择 网络 > 路由表 ，进入路由表列表页；
2. 点击操作列的删除；
![](/image/Networking/Virtual-Private-Cloud/Operation-Guide/Route-Table-Configuration/Step6.png)

3. 二次确认删除路由表后，即可删除该路由表；
4. 删除路由表的限制：
    a) 关联了子网的自定义路由表不可删除。
    b) 默认路由表不可删除。



#### **步骤五、路由规则**

1.默认路由表，创建私有网络时，默认会创建一张默认路由表，包含两条默认的路由规则，分别为私有网络内部通信的Local和访问公网的Internet网关。Local路由不能修改、不能删除，其具体规则为[Local Local Local]，Internet路由可以修改、可以删除。
2.自定义路由表，用户创建的路由表为自定义路由表，包含一条默认的路由规则，为私有网络内部通信的Local，不能修改、不能删除。
3.私有网络内的子网之间进行通信，优先匹配Local路由。
4.路由表的路由规则匹配顺序为从上至下，精确匹配。
![](/image/Networking/Virtual-Private-Cloud/Operation-Guide/Route-Table-Configuration/Step7.png)




#### **步骤六、编辑路由规则**

1.路由规则的目的端不能为空，且路由规则之间的目的端不能完全相同，目的端输入格式为网段的CIDR。
2.若路由表所在的私有网络有预设CIDR，则路由规则的目的端不能与所属私有网络的CIDR有冲突。
3.若路由表所在的私有网络无预设CIDR，则路由规则的目的端不能与所属私有网络中的任何子网的CIDR有冲突。
4.下一跳类型，支持Internet和云主机作为下一跳，流量若要访问Internet，可选择Internet网关，或自建云主机作为公网网关。
5.下一跳(地址)，支持Internet和云主机作为下一跳地址，可选择某台配置了SNAT功能的云主机作为下一跳的网关。
![](/image/Networking/Virtual-Private-Cloud/Operation-Guide/Route-Table-Configuration/Step8.png)