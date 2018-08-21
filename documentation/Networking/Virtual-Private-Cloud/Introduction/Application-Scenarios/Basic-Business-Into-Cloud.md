## 基础业务上云

场景：您可以在私有网络内创建不同子网，整个Web层放在一个子网，通过配置弹性IP/NAT网关与Internet通信，逻辑层单独放在一个子网，数据层放在另外一个子网，子网和子网之间的流量通过网络ACL进行控制。这样安全、灵活的部署，即可满足您应用访问Internet的需求，又能保障数据库服务器的安全。更多联通性需求可通过VPC Peering、专线服务、VPN等产品实现。

建议配置：VPC、子网、云主机、RDS、云缓存、公网IP、网络ACL、安全组

![](/image/Networking/Virtual-Private-Cloud/Basic-Business-Into-Cloud.png)