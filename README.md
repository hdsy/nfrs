# NFRS
natural frequency restriction strategy 

基于自然时间（秒、分、时、日、月、年）设定频率限制策略，用来控制特定业务的访问频次。
日常应用中每一个应用都需要在本地、集中的方式获得授权、非授权用户的访问频次，用来确保服务的可用性，了解客户的性能要求。

在实际代码中，如下调用即可。例如：

---
// init

CNFRS objCNFRSofPlaceOrder(busid_of_PlaceOrder);

......

if (objCNFRSofPlaceOrder(customerID) != 0)
{
  error_output(customerID,objCNFRSofPlaceOrder.getRetcode(),objCNFRSofPlaceOrder.getMessage());
  return ;
}

......


---

#系统的组成

命令 CMD + C库 API + WEB服务 WEB SERVICE

**命令 CMD **
  初始化环境 ： 开辟存储空间，启动相关应用服务
  配置策略 ： 配置相关业务的限制策略，以及空间大小
  查看、修改数据等
  
**C库 API **
  集成到CPP开发程序中，实现频率限制
  
**WEB服务 WEB SERVICE **
  对外提供服务

