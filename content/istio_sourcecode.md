# 第三章 源码选读

略扫过 Istio 的代码，目前关注点都在 ./pilot 和 ./pkg 两个子目录上


## 3.1 主要数据结构

## 3.2 Pilot 主流程


Pilot将服务信息和配置数据转换为xDS接口的标准数据结构，通过gRPC下发到数据面的Envoy
Pilot的输入
包括两部分数据来源：

	* 服务数据： 来源于各个服务注册表(Service Registry)，例如Kubernetes中注册的Service，Consul Catalog中的服务等。
	* 配置规则： 各种配置规则，包括路由规则及流量管理规则等，通过Kubernetes CRD(Custom Resources Definition)形式定义并存储在Kubernetes中。

Pilot的输出

	* 为符合xDS接口的数据面配置数据
	* 并通过gRPC Streaming接口将配置数据推送到数据面的Envoy中。



![istio_pilot_workflow.png](./img/istio_pilot_workflow.png)



## 3.3 Pilot 初始化流程


![istio_pilot-discovery_init.png](./img/istio_pilot-discovery_init.png)
