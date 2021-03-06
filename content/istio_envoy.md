# 第五章 Envoy

Envoy是由lyft开源的边缘和和服务代理，后被捐赠给CNCF基金会。

就如 xDS 协议不属于 Istio，Envoy 也另有出身。

## 基本概念

Envoy 是以 C++ 开发的高性能代理，通讯遵从 xDS 协议，其内置功能：
* 服务发现
* 负载均衡
* TLS终止
* HTTP/2
* GRPC代理
* 熔断器
* 健康检查
* 基于百分比流量拆分的灰度发布
* 故障注入

## 版本变迁

* V1版本
使用HTTP+轮询方式，实现DS

* V2版本
(于Google合作加强)，使用 GRPC+push实现
兼容V1的 SDS/CDS/RDS/LDS
增加ADS、HDS

## 数据结构和代码
### xds
对xds的支持，从 [grpc-go](https://github.com/grpc/grpc-go)就开始了(之前以为都是在 Istio-pilot包中处理xds协议，没想到xds被当作通用协议，在grpc-go这种通用包中就支持)
在其中的
* v2client.go：通讯底层、按请求类型处理
* types.go：基本定义