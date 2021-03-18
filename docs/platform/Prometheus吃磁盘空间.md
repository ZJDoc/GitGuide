
# Prometheus吃磁盘空间

在云服务器上部署`Gitlab`，今天发现无法登录了。登上云服务器后发现磁盘容量没有了，通过查找发现`Prometheus`目录下占据了`30GB`的空间（总共`50GB`）

参考：

[Monitoring GitLab with Prometheus](https://docs.gitlab.com/ee/administration/monitoring/prometheus/)

[Prometheus eats disk space in /var/opt/gitlab/prometheus/data](https://gitlab.com/gitlab-org/omnibus-gitlab/-/issues/4166)

[GitLab 官方镜像内部集成 Prometheus 历史数据过大的问题处理](https://lakelight.net/2020/03/24/GitLab-Prometheus-clean.html)

`Prometheus`是一个监控服务，会保存历史监控数据，下面尝试关闭该服务并删除之前的数据（在`Docker Gitlab`上操作）

1. 修改配置文件`/srv/gitlab/config/gitlab.rb`，添加

```
prometheus_monitoring['enable'] = false
```

2. 关闭`gitlab`并删除`/srv/gitlab/data/prometheus`文件夹数据

3. 重启`gitlab`，问题解决