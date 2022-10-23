### Master 组件 （control plane）
#### kube-apiserver
> Kubernetes控制平台的前端（front-end），可水平扩展（通过部署更多的实例以达到性能要求）。kubectl / kubernetes dashboard / kuboard 等Kubernetes管理工具就是通过 kubernetes API 实现对 Kubernetes 集群的管理。

#### etcd
> 支持一致性和高可用的名值对存储组件，Kubernetes集群的所有配置信息都存储在 etcd 中。

#### kube-scheduler
> 监控所有新创建尚未分配到节点上的 Pod，并且自动选择为 Pod 选择一个合适的节点去运行。
> - 单个或多个 Pod 的资源需求
> - 硬件、软件、策略的限制
> - 亲和与反亲和（affinity and anti-affinity）的约定
> - 数据本地化要求
> - 工作负载间的相互作用

#### kube-controller-manager
> 运行所有的控制器。逻辑上来说，每一个控制器是一个独立的进程，但是为了降低复杂度，这些控制器都被合并运行在一个进程里。
> - 节点控制器： 负责监听节点停机的事件并作出对应响应
> - 副本控制器： 负责为集群中每一个 副本控制器对象（Replication Controller Object）维护期望的 Pod 副本数
> - 端点（Endpoints）控制器：负责为端点对象（Endpoints Object，连接 Service 和 Pod）赋值
> - Service Account & Token控制器： 负责为新的名称空间创建 default Service Account 以及 API Access Token
> - 端点（Endpoints）控制器：负责为端点对象（Endpoints Object，连接 Service 和 Pod）赋值
> - Service Account & Token控制器： 负责为新的名称空间创建 default Service Account 以及 API Access Token

### Node 组件
Node 组件运行在每一个节点上（包括 master 节点和 worker 节点），负责维护运行中的 Pod 并提供 Kubernetes 运行时环境。
#### kubelet
> 是运行在每一个集群节点上的代理程序。它确保 Pod 中的容器处于运行状态。Kubelet 通过多种途径获得 PodSpec 定义，并确保 PodSpec 定义中所描述的容器处于运行和健康的状态。Kubelet不管理不是通过 Kubernetes 创建的容器


#### kube-proxy
>  是一个网络代理程序，运行在集群中的每一个节点上，是实现 Kubernetes Service 概念的重要部分
>  kube-proxy 在节点上维护网络规则。这些网络规则使得您可以在集群内、集群外正确地与 Pod 进行网络通信。如果操作系统中存在 packet filtering layer，kube-proxy 将使用这一特性（[iptables代理模式](https://kuboard.cn/learning/k8s-intermediate/service/service-details.html#iptables-%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F)），否则，kube-proxy将自行转发网络请求（[User space代理模式](https://kuboard.cn/learning/k8s-intermediate/service/service-details.html#user-space-%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F)）

### 容器引擎
> 容器引擎负责运行容器。Kubernetes支持多种容器引擎：[Docker](http://www.docker.com/)、[containerd](https://containerd.io/)、[cri-o](https://cri-o.io/)、[rktlet](https://github.com/kubernetes-incubator/rktlet)以及任何实现了 [Kubernetes容器引擎接口](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-node/container-runtime-interface.md)的容器引擎


### Addons
Addons 使用 Kubernetes 资源（DaemonSet、Deployment等）实现集群的功能特性。由于他们提供集群级别的功能特性，addons使用到的Kubernetes资源都放置在 `kube-system` 名称空间下。
#### DNS
> 除了 DNS Addon 以外，其他的 addon 都不是必须的，所有 Kubernetes 集群都应该有 [Cluster DNS](https://kuboard.cn/learning/k8s-intermediate/service/dns.html)
> Cluster DNS 是一个 DNS 服务器，是对您已有环境中其他 DNS 服务器的一个补充，存放了 Kubernetes Service 的 DNS 记录。
> Kubernetes 启动容器时，自动将该 DNS 服务器加入到容器的 DNS 搜索列表中。