# 资源管理

在 Kubernetes 中，所有的内容都抽象为资源，用户需要通过操作资源来管理 Kubernetes。Kubernetes 的本质上就是一个集群系统，用户可以在集群中部署各种服务。所谓的部署服务，其实就是在 Kubernetes 集群中运行一个个的容器，并将指定的程序跑在容器中。

Kubernetes 的最小管理单元是 Pod 而不是容器，所以只能将容器放在 Pod 中，而 Kubernetes 一般也不会直接管理 Pod，而是通过 Pod 控制器来管理 Pod 的。

Pod 可以提供服务之后，就要考虑如何访问 Pod 中服务，Kubernetes 提供了 Service 资源实现这个功能。

当然，如果 Pod 中程序的数据需要持久化，Kubernetes 还提供了各种存储系统。

![alt text](image.png)

## 资源管理方式

- 命令式对象管理

    直接使用命令去操作 Kubernetes 资源
```bash
kubectl run nginx-pod --image=nginx:1.17.1 --port=80
```

- 命令式对象配置
    通过命令配置和配置文件去操作 Kubernetes 资源
```bash
kubectl create/patch -f nginx-pod.yaml
```
- 声明式对象配置
    通过 apply 命令和配置文件去操作 Kubernetes 资源
```
kubectl apply -f nginx-pod.yaml
```

|  类型   | 操作对象   |  适用环境   | 优点  |缺点|
|  ----   | ----   |  ----  | ----  | ----
| 命令式对象管理  | 对象 | 测试  | 简单 |    只能操作活动对象，无法审计、跟踪 |
| 命令式对象配置  | 文件 | 开发  | 可以审计、跟踪 |  项目大时，配置文件多，操作麻烦   |
| 声明式对象配置 | 目录 | 开发  | 支持目录操作 |   意外情况下难以调试  |

## kubectl命令
kubectl是kubernetes集群的命令行工具，通过它能够对集群本身进行管理，并能够在集群上进行容器化应用的安装部署。kubectl命令的语法如下：
```batch
kubectl [command] [type] [name] [flags]
```
- comand：指定要对资源执行的操作，例如create、get、delete

- type：指定资源类型，比如deployment、pod、service

- name：指定资源的名称，名称大小写敏感

- flags：指定额外的可选参数

```batch
# 查看某个pod,以yaml格式展示结果
kubectl get pod pod_name -o yaml
```

## 资源类型
经常使用的资源有下面这些：
Kubernetes 资源分类

| 资源分类          | 资源名称                      | 缩写 | 资源作用          |
|-------------------|-------------------------------|------|-------------------|
| 集群级别资源      | nodes                         | no   | 集群组成部分      |
|                   | namespaces                    | ns   | 隔离 Pod          |
| pod 资源          | pods                          | po   | 装载容器          |
|                   | replicationcontrollers        | rc   | 控制 pod 资源     |
|                   | replicasets                   | rs   | 控制 pod 资源     |
|                   | deployments                   | deploy | 控制 pod 资源     |
|                   | daemonsets                    | ds   | 控制 pod 资源     |
|                   | jobs                          |      | 控制 pod 资源     |
|                   | cronjobs                      | cj   | 控制 pod 资源     |
|                   | horizontalpodautoscalers      | hpa  | 控制 pod 资源     |
|                   | statefulsets                  | sts  | 控制 pod 资源     |
| 服务发现资源      | services                      | svc  | 统一 pod 对外接口 |
|                   | ingress                       | ing  | 统一 pod 对外接口 |
| 存储资源          | volumeattachments             |      | 存储              |
|                   | persistentvolumes             | pv   | 存储              |
|                   | persistentvolumeclaims        | pvc  | 存储              |
| 配置资源          | configmaps                    | cm   | 配置              |
|                   | secrets                       |      | 配置              |

## 操作


| 命令分类     | 命令       | 翻译        | 命令作用                    |
|--------------|------------|-------------|-----------------------------|
| 基本命令     | create     | 创建        | 创建一个资源                |
|              | edit       | 编辑        | 编辑一个资源                |
|              | get        | 获取        | 获取一个资源                |
|              | patch      | 更新        | 更新一个资源                |
|              | delete     | 删除        | 删除一个资源                |
|              | explain    | 解释        | 展示资源文档                |
| 运行和调试   | run        | 运行        | 在集群中运行一个指定的镜像  |
|              | expose     | 暴露        | 暴露资源为 Service          |
|              | describe   | 描述        | 显示资源内部信息            |
|              | logs       | 日志        | 输出容器在 pod 中的日志     |
|              | attach     | 缠绕        | 进入运行中的容器            |
|              | exec       | 执行        | 执行容器中的一个命令        |
|              | cp         | 复制        | 在 Pod 内外复制文件         |
|              | rollout    | 首次展示    | 管理资源的发布              |
|              | scale      | 规模        | 扩(缩)容 Pod 的数量         |
|              | autoscale  | 自动调整    | 自动调整 Pod 的数量         |
| 高级命令     | apply      | 应用        | 通过文件对资源进行配置      |
|              | label      | 标签        | 更新资源上的标签            |
| 其他命令     | cluster-info | 集群信息  | 显示集群信息                |
|              | version    | 版本        | 显示当前 Server 和 Client 的版本 |
