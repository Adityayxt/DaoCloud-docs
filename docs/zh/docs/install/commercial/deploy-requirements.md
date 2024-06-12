
# 部署要求

部署 DCE 5.0 时需要先做好软件规划、硬件规划、网络规划。

## 操作系统要求

| **架构** | **操作系统** | **推荐内核版本** | 备注（安装指导文档） |
| -------- | ----------- | ----------- | ----------------- |
| AMD 64 | CentOS 7.X | Kernel 3.10.0-1127.el7.x86_64 on an x86_64 | 推荐 CentOS 7.9<br />[离线安装 DCE 5.0 商业版](start-install.md) |
| | Redhat 8.X | 4.18.0-305.el8.x86_64 | 推荐 Redhat 8.4<br />参考[离线安装 DCE 5.0 商业版](start-install.md) |
| | Redhat 7.X | 3.10.0-1160.e17.x86 | 推荐 Redhat 7.9<br />参考[离线安装 DCE 5.0 商业版](start-install.md) |
| | Redhat 9.X | 5.14.0-284.11.1.e9_2.x86_64 | 推荐 Redhat 9.2<br />参考[离线安装 DCE 5.0 商业版](start-install.md) |
| | Ubuntu 20.04 | 5.10.104 | 参考[离线安装 DCE 5.0 商业版](start-install.md) |
| | Ubuntu 22.04 | 5.15.0-78-generic | 参考[离线安装 DCE 5.0 商业版](start-install.md) |
| | 统信 UOS V20 （1020a） | 5.4.0-125-generic | 参考 [UOS V20 (1020a) 上部署 DCE 5.0 商业版](../os-install/uos-v20-install-dce5.0.md) |
| | openEuler 22.03 | 5.10.0-60.18.0.50.oe2203.x86_64 | 参考[离线安装 DCE 5.0 商业版](start-install.md) |
| | Oracle Linux R9/R8 U1 | 5.15.0-3.60.5.1.el9uek.x86_64 | 参考 [Oracle Linux R9 U1 上部署 DCE 5.0 商业版](../os-install/oracleLinux-install-dce5.0.md) |
| | TencentOS Server 3.1 | 5.4.119-19.0009.14 | 参考 [TencentOS Server 3.1 上部署 DCE 5.0 商业版](../os-install/TencentOS-install-dce5.0.md) |
| ARM 64 | 银河麒麟 OS V10 SP2 | 4.19.90-24.4.v2101.ky10.aarch64 | 参考[离线安装 DCE 5.0 商业版](start-install.md) |

!!! note

    若非上表中声明的操作系统，请参考文档 [Other Linux 离线部署 DCE 5.0 商业版](../os-install/otherlinux.md)进行安装部署。

## 内核要求

由于一些组件或功能对操作系统的内核版本有要求，部署前请根据实际情况参照下表来选择内核版本：

| 组件/功能 | 内核版本要求 |
| -------- | ---------- |
| 容器管理 GPU 能力 | ≥ 3.10.1160 |
| Cilium | ≥ 5.12 |
| Hwameistor DRDB 能力 | [DRBD 适配的内核版本](../../storage/hwameistor/intro/drbd-support.md) |
| Kubevirt | ≥ 4.x |
| Merbridge 要求 | ≥ 5.7 |

## 硬件要求

### CPU 、内存和硬盘

| **类型** | **具体要求** |
| ------- | ----------- |
| CPU | 不得超售 |
| 内存 | 不得超售 |
| 硬盘 | IOPS > 500 吞吐量 > 200 MB/s |

### 新手尝鲜模式 CPU 、内存、硬盘要求

参阅[新手尝鲜模式说明](./deploy-arch.md#_2)。

| **数量** | **服务器角色** | **服务器用途** | **cpu 数量** | **内存容量** | **系统硬盘** | **未分区的硬盘** |
| ------- | ------------- | ------------ | ----------- | ----------- | ----------- | ------------- |
| 1 | all in one | 镜像仓库、chart museum 、global 集群本身 | 16 core | 32G | 200G | 400G |

### 4 节点模式 CPU 、内存、硬盘要求

参阅 [4 节点模式说明](./deploy-arch.md#4)。

| **数量** | **服务器角色** | **服务器用途** | **cpu 数量** | **内存容量** | **系统硬盘** | **未分区的硬盘** |
| ------- | ------------- | ------------ | ----------- | ----------- | ----------- | -------------- |
| 1 | 火种节点 | 1. 执行安装部署程序<br />2. 运行平台所需的镜像仓库和 chart museum | 2 | 4G | 200G | - |
| 3 | 控制面 | 1. 运行 DCE 5.0 组件<br />2. 运行 kubernetes 系统组件 | 8 | 16G | 100G | 200G |

### 7 节点模式(生产环境推荐) CPU 、内存、硬盘要求

参阅 [7 节点模式说明](./deploy-arch.md#7-1-6)。

| **数量** | **服务器角色** | **服务器用途** | **cpu 数量** | **内存容量** | **系统硬盘** | **未分区的硬盘** |
| ------- | ------------- | ------------ | ----------- | ----------- | ----------- | -------------- |
| 1 | 火种节点 | 1. 执行安装部署程序<br />2. 运行平台所需的镜像仓库和 chart museum | 2 | 4G | 200G | - |
| 3 | master | 1. 运行 DCE 5.0 组件<br /> 2. 运行 kubernetes 系统组件 | 8 | 16G | 100G | 200G |
| 3 | worker | 单独运行日志相关组件 | 8 | 16G | 100G | 200G |

## 网络要求

### 网络拓扑

假设使用 VIP 作为全局集群的负载均衡方式：

![Network-Topology](https://docs.daocloud.io/daocloud-docs-images/docs/install/commercial/images/Network-Topology.png)

### 网络要求

| **资源** | **要求** | **说明** |
| ------- | -------- | ------- |
| `istioGatewayVip` | 1 个 | 如果负载均衡模式是 metallb，则需要指定一个 VIP，供给 DCE 的 UI 界面和 OpenAPI 访问入口。 |
| `insightVip` | 1 个 | 如果负载均衡模式是 metallb，则需要指定一个 VIP，供给 GLobal 集群的 insight 数据收集入口使用，子集群的 insight-agent 可上报数据到这个 VIP。 |
| 网络速率 | 1000 M/s | 不低于千兆，建议万兆 |
| 协议 | - | 支持 IPv6 |
| 保留 IP 地址段 | 需保留两段 | 供 Pod（默认 10.233.64.0/18）和 Service （默认 10.233.0.0/18 使用）。如果已经在使用了，可以自定义其他网段避免 IP 地址冲突。|
| 路由 | - | 服务器有 default 或指向 0.0.0.0 这个地址的路由。 |
| NTP 服务地址 | 1~4 个 | 确保您的数据中心有可以访问的 NTP 服务器 IP 地址。 |
| DNS 服务地址 | 1~2 个 | 如果您的应用需要 DNS 服务，请准备可以访问 DNS 服务器 IP 地址。 |

## 客户端浏览器的要求

- Firefox **≥** v49
- Chrome **≥** v54
