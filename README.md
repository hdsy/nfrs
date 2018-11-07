# NFRS
natural frequency restriction strategy 

基于自然时间（秒、分、时、日、月、年）设定频率限制策略，用来控制特定业务的访问频次。
日常应用中每一个应用都需要在本地、集中的方式获得授权、非授权用户的访问频次，用来确保服务的可用性，了解客户的实际访问要求，也是实现服务治理的一个重要环节。

在实际服务代码中，建议如下应用形式。例如：

---
<PRE>
// init NFRS of service "PlaceOrder"

CNFRS objCNFRSofPlaceOrder(busid_of_PlaceOrder);

......

if (objCNFRSofPlaceOrder(customerID) != 0)
{
  error_output(customerID,objCNFRSofPlaceOrder.getRetcode(),objCNFRSofPlaceOrder.getMessage());
  return ;
}

......

</PRE>
---

# 系统的组成 

单节点，配置中心，集群

单节点实现本地化的频率控制策略，配置中心对整个集群进行控制策略管理，集群有两个以上节点组成。 每个节点将自己的数据上报给配置中心，并从配置中心获取最新的汇总信息，应用到自身的控制上。

## 单节点

命令 CMD + C库 API + 代理 AGENT

**命令 CMD **
  初始化环境 ： 开辟存储空间，启动相关应用服务
  配置策略 ： 配置相关业务的限制策略，以及空间大小
  查看、修改数据等
  
**C库 API **
  集成到CPP开发程序中，实现频率限制
  
**代理 AGENT **
  负责上报本地数据到配置中心，并将配置中心的汇总数据取下来，可配置频率（例如60秒更新一次）
  
## 配置中心 
WEB服务 WEB SERVICE

**WEB服务 WEB SERVICE **
  对外提供服务，基本的集群信息，频率配置策略，每节点频率策略；以及汇总运算，和相关视图
  

