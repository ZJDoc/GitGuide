
# 版本更新后database出错

### 问题描述

拉取了最新的`Docker Gitlab`镜像，部署时发现了如下错误：

```
gitlab     |     System Info:
gitlab     |     ------------
gitlab     |     chef_version=14.14.29
gitlab     |     platform=ubuntu
gitlab     |     platform_version=16.04
gitlab     |     ruby=ruby 2.6.6p146 (2020-03-31 revision 67876) [x86_64-linux]
gitlab     |     program_name=/opt/gitlab/embedded/bin/chef-client
gitlab     |     executable=/opt/gitlab/embedded/bin/chef-client
gitlab     |     
gitlab     | 
gitlab     | Running handlers:
gitlab     | There was an error running gitlab-ctl reconfigure:
gitlab     | 
gitlab     | bash[migrate gitlab-rails database] (gitlab::database_migrations line 55) had an error: Mixlib::ShellOut::ShellCommandFailed: Expected process to exit with [0], but received '1'
gitlab     | ---- Begin output of "bash"  "/tmp/chef-script20200618-23-sfpkhu" ----
gitlab     | STDOUT: rake aborted!
gitlab     | PG::ConnectionBad: could not connect to server: No such file or directory
gitlab     | 	Is the server running locally and accepting
gitlab     | 	connections on Unix domain socket "/var/opt/gitlab/postgresql/.s.PGSQL.5432"?
gitlab     | /opt/gitlab/embedded/service/gitlab-rails/lib/tasks/gitlab/db.rake:48:in `block (3 levels) in <top (required)>'
gitlab     | /opt/gitlab/embedded/bin/bundle:23:in `load'
gitlab     | /opt/gitlab/embedded/bin/bundle:23:in `<main>'
gitlab     | Tasks: TOP => gitlab:db:configure
gitlab     | (See full trace by running task with --trace)
gitlab     | STDERR: 
gitlab     | ---- End output of "bash"  "/tmp/chef-script20200618-23-sfpkhu" ----
gitlab     | Ran "bash"  "/tmp/chef-script20200618-23-sfpkhu" returned 1
```

### 问题解决

在网上查了一些资料，说是新旧版本的配置格式不一致，需要删除之前的配置数据。幸好在本地保存了之前使用的镜像，打包该镜像后上传到服务器重新加载即可