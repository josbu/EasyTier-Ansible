# EasyTier-Ansible
EasyTier-Ansible 工程，方便批量管理 EasyTier 节点。

# 关于 EasyTier

EasyTier is a simple, safe and decentralized VPN networking solution implemented with the Rust language and Tokio framework.
一个简单、安全、去中心化的内网穿透 VPN 组网方案，使用 Rust 语言和 Tokio 框架实现。


- [GitHub@EasyTier](https://github.com/EasyTier/EasyTier)
- [EasyTier Official Website](https://www.easytier.top/)

# 部署模式

- Linux 裸机部署
- 服务位置：/opt/easytier/
- 配置信息：config.toml
- 节点信息配置：nodes.ini

# 快速开始

需自行根据服务器操作系统安装 Ansible。

# 脚本介绍

build_easytier_config.yml ：生成 easytier 配置文件

update_easytier.yml       ：更新 easytier 版本

restart_easytier.yml      ：重启 easytier 服务

# 目录结构

```
.
├── LICENSE
├── README.md
├── config                        # 配置文件模板
│   ├── easytier.toml.j2          # EasyTier 配置文件模板（适配 v1.2.3）
│   └── vars                      # 参数信息
│       ├── 172.16.0.1.yml        # 节点参数信息
│       ├── 172.16.0.2.yml        # 节点参数信息（文件名为节点 IP）
│       ├── flags.yml             # 网络 flags 信息
│       ├── network.yml           # 网络信息
│       └── peers.yml             # Peer 信息
├── nodes.ini                     # 节点配置文件（Ansible 配置文件）
├── update                        # 升级包目录
│   └── README.md
├── build_easytier_config.yml     # 生成 EasyTier 配置文件脚本
├── restart_easytier.yml          # 重启 EasyTier 服务脚本
└── update_easytier.yml           # 更新 EasyTier 版本脚本
```


# 使用范例

其中 core 为服务器组的名称，见 nodes.ini。

## 更新 EasyTier 服务版本程序
```
ansible-playbook update_easytier.yml -i nodes.ini --extra-var "dest_host=core"

```
## 重启 EasyTier 服务
```
ansible-playbook restart_easytier.yml -i nodes.ini --extra-var "dest_host=core"
```

## 生成 EasyTier 配置并发布到节点
```
ansible-playbook build_easytier_config.yml -i nodes.ini --extra-var "dest_host=core"
```
