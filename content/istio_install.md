# 第二章 安装

Istio 的安装，主要是：
* pilot server，即 pilot-discovery
* pilot agent
* envoy

另外还有一些辅助组件，如
* istio-ingressgateway
* istio-egressgateway
* istio-tracing：目前基于 jaeger
* prometheus
* grafana
* kiali：Istio 简单的页面

## 2.1 基本准备


## 2.2 Docker 安装



## 2.3 源码编译安装

### 获取源码

**源码包下载方式**
下载istio zip包，解压到本地后，执行：
```
git init
git remote add origin https://github.com/istio/istio
git fetch
git checkout -f remotes/origin/release-1.7
```


**git 克隆方式**
```
git clone https://github.com/istio/istio
```
不能用浅层克隆，否则编译会出错
具体可参看：https://www.orcode.com/question/1233033_k02c64.html


### 编译用基础镜像获取
通过阿里云+github解决被qiang问题
参看：https://www.jianshu.com/p/aac137b8a022


大致：
```
docker pull registry.cn-zhangjiakou.aliyuncs.com/com_ka_img/istio:v0.1
# 输入服务器密码

docker pull registry.cn-zhangjiakou.aliyuncs.com/com_ka_img/istio:v0.1

docker tag  registry.cn-zhangjiakou.aliyuncs.com/com_ka_img/istio:v0.1 gcr.io/istio-testing/build-tools:master-2020-07-08T14-39-36

```


构建成功后，拉取到本地：
```
docker pull registry.cn-hangzhou.aliyuncs.com/com_ka_img/aa:release-v1
docker tag registry.cn-hangzhou.aliyuncs.com/com_ka_img/aa:release-v1  gcr.io/istio-testing/build-tools:master-2020-06-22T20-44-43
```


### 编译

```
make init # 初始化，检查目录结构、Go版本号、初始化环境变量、检查vendor、envoy和webassembly插件等
make docker # 对各组件（istioctl、mixer、pilot、istio-auth等）进行二进制包编译、测试、镜像编译
make push # 推送镜像到dockerhub

# 其他指令
make pilot  docker.pilot # 编译pilot组件和镜像
make app  docker.app # 编译app组件和镜像
make proxy  docker.proxy # 编译proxy组件和镜像
make proxy_init  docker.proxy_init # 编译proxy_init组件和镜像
make proxy_debug  docker.proxy_debug # 编译proxy_debug组件和镜像
make sidecar_injector  docker.sidecar_injector # 编译sidecar_injector组件和镜像
make proxyv2  docker.proxyv2 # 编译proxyv2组件和镜像 
make push.docker.pilot # 推送pilot镜像到dockerhub，其他组件类似

```