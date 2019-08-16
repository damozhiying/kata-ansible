# 在 CentOS 上安装使用 kata-container 作为 Docker runtime

## 使用方法

编辑 `hosts` 文件，添加需要使用 kata-container 的节点

```ini
[kata_nodes]
172.16.140.37
```

kata-container 默认安装版本为 master, x86_64 和 CentOS 7，如需要不同版本，可以修改 `vars/main.yaml` 文件中的变量

```yaml
---
version: 7
branch: master
arch: x86_64
```

因为 GFW，下载 kata-container rpm 镜像可能会非常慢，推荐配置 yum 代理。
**在使用 kata-container 的节点**上配置 `/etc/yum.conf` 文件，添加代理设置

```conf
proxy=<schema>://<proxy_host>:<proxy_port>
```

**注意**
安装 kata-container 需要最新版 docker-ce，且覆盖 `/etc/docker/daemon.json` 文件，不建议在已经运行了 Docker 的
机器上安装 kata-container。

```bash
ansible-playbook -i host install.yaml
```
