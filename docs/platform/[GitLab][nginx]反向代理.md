
# [GitLab][nginx]反向代理

当前`gitlab`登录路径是`localhost:8080`

```
$ curl localhost:8800
<html><body>You are being <a href="http://localhost:8800/users/sign_in">redirected</a>.</body></html>
```

地址会跳转到`http://localhost:8800/users/sign_i`，下面通过反向代理简化登录地址

## 调整gitlab登录地址

修改`gitlab`配置文件`/etc/gitlab/gitlab.rb`，修改`external_url`访问路径

```
external_url 'http://localhost:8800/gitlabs/'
```

更新`gitlab`配置

```
$ gitlab-ctl reconfigure
$ gitlab-ctl restart
```

## nginx配置

修改`nginx`配置文件`/etc/nginx/conf.d/default.conf`，新增`location`

```
$ cat gitlab.conf 
server {
    ...
    ...
    location /gitlabs/ {
	    proxy_pass http://localhost:8800;
    }
    ...
    ...
}
```

刷新`nginx`

```
$ sudo nginx -t
$ sudo nginx -s reload
```

之后输入`localhost/gitlabs/`即可登录`gitlab`