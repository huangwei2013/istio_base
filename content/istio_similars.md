# 第六章 竞品

## Service Mesh 常见组件

| 名称  | 来源方 | 成熟度  | 优势 | 劣势 |  基础  | 
| --- | --- | --- | --- | --- | --- | 
| AWS App Mesh | AWS |   | 与其他AWS服务，如EKS，Fargate和EC2的无缝集成； 支持如mTLS、高级负载均衡之类的安全功能  | 不能迁移到App Mesh外部或在多云设置中使用；不支持授权规则  | Envoy | 
| Istio | Lyft, Googel, IBM | 1.7.0 | 和K8S的无缝集成 | 有一定使用复杂度 | Envoy |
| Linkerd | | 2.7.1(2020.04) | 完全独立实现(不依赖于Envoy等)； 安装简洁 | | linkerd-proxy |
| Kuma | Kong  | 0.4.0 | | 不完善 | |
| Consul Connect | HashiCorp | | 可在任何Consul环境中无缝运行 | 只能满足与其他HashiCorp产品一起使用 |  同Consul、Envio集成使用  |
| Envoy Proxy | | | 同Envoy原生结合 | | | 