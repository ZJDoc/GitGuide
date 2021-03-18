
# unicorn出错

## 问题描述

通过`docker`部署`gitlab`一段时间后，突然出现`502`错误

查看容器状态，显示不健康

```
CONTAINER ID        IMAGE                     COMMAND                  CREATED             STATUS                 PORTS                                                           NAMES
89481faa2ed1        gitlab/gitlab-ce:latest   "/assets/wrapper"        2 weeks ago         Up 7 hours (unhealthy)
```

浏览容器日志，发现如下错误：

```
==> /var/log/gitlab/unicorn/unicorn_stdout.log <==
bundler: failed to load command: unicorn (/opt/gitlab/embedded/bin/unicorn)

==> /var/log/gitlab/unicorn/unicorn_stderr.log <==
ArgumentError: Already running on PID:460 (or pid=/opt/gitlab/var/unicorn/unicorn.pid is stale)
  /opt/gitlab/embedded/lib/ruby/gems/2.6.0/gems/unicorn-5.4.1/lib/unicorn/http_server.rb:205:in `pid='
  /opt/gitlab/embedded/lib/ruby/gems/2.6.0/gems/unicorn-5.4.1/lib/unicorn/http_server.rb:137:in `start'
  /opt/gitlab/embedded/lib/ruby/gems/2.6.0/gems/unicorn-5.4.1/bin/unicorn:126:in `<top (required)>'
  /opt/gitlab/embedded/bin/unicorn:23:in `load'
  /opt/gitlab/embedded/bin/unicorn:23:in `<top (required)>'

==> /var/log/gitlab/unicorn/current <==
2019-12-18_12:27:47.34406 failed to start a new unicorn master
2019-12-18_12:27:47.35882 starting new unicorn master
2019-12-18_12:27:47.91735 master failed to start, check stderr log for details
```

## 问题解析

看样子是`unicorn`的问题，参考：

[gitlab服务器502恢复过程](https://blog.csdn.net/zhouchuan152/article/details/95871798)

[gitlab docker Web界面打开反应迟钝的解决办法](https://blog.csdn.net/happyfreeangel/article/details/88653846)

进入容器内部，查看`unicorn`状态

```
$ docker exec -it xxxx bash
# gitlab-ctl tail unicorn
```

发现每次`unicorn`显示的`PID`都不同，修改`/etc/gitlab/gitlab.rb`，添加

```
unicorn['listen'] = 'localhost'
unicorn['port'] = 8999
```

更新并重启后，`gitlab`服务恢复正常

```
# gitlab-ctl reconfigure
# gitlab-ctl restart
```