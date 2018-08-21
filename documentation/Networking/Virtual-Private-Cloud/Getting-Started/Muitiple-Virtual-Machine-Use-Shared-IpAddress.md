# **多主机共享公网IP**

应用场景：实现相同VPC下的多台主机通过一台作为NAT网关的主机访问公网，共享IP带宽。假定目前存在VPC名为NAT01（10.1.0.0/16），下属两个子网：SNAT01(10.1.1.0/24)、SNAT02(10.1.2.0/24)，SNAT02下存在多台主机，实现子网SNAT02下的多台主机可通过子网SNAT01下一台作为NAT GW的主机上网。

**步骤一：在SNAT01子网下创建一台作为NAT网关的主机**

![](/image/Networking/Virtual-Private-Cloud/Getting-Started/Muitiple-Virtual-Machine-Use-Shared-IpAddress/Step1-1.png)



在SNAT01下创建一台主机，镜像选择CentOS-7.2 64位 NAT Gateway

![](/image/Networking/Virtual-Private-Cloud/Getting-Started/Muitiple-Virtual-Machine-Use-Shared-IpAddress/Step1-2.png)



选择所属VPC为NAT01、子网为SNAT01

配置公网IP类型、带宽

主机命名为SNAT01

![](/image/Networking/Virtual-Private-Cloud/Getting-Started/Muitiple-Virtual-Machine-Use-Shared-IpAddress/Step1-3.png)



创建完成后，在主机列表页可以看到相同VPC下不同子网的主机情况



**步骤二：配置子网SNAT02的路由表指向NAT网关**

![](/image/Networking/Virtual-Private-Cloud/Getting-Started/Muitiple-Virtual-Machine-Use-Shared-IpAddress/Step2-1.png)



通过子网SNAT02查看和子网绑定的路由表

![](/image/Networking/Virtual-Private-Cloud/Getting-Started/Muitiple-Virtual-Machine-Use-Shared-IpAddress/Step2-2.png)



编辑路由表：下一跳类型：云主机，下一跳主机：SANT01

配置完成后，子网SNAT02下的所有主机都可以通过SANT01作为NAT网关进行公网访问。

同理，可配置相同VPC下其他的子网路由。

**注意：如主机需要通过NAT网关通信，不能选择与主机所在子网绑定同一张路由表的子网内的主机作为NAT网关。**