
# [github]DNS加速

## 加速原理

通过在本地域名文件中加入`github`相关网站的`DNS`地址，加快`DNS`解析过程，从而加快网页加载速度

## 方式一

参考：[加快国内访问Github网站的速度](https://aoenian.github.io/2018/05/12/github-access-fast/)

登录[DNS查询](http://tool.chinaz.com/dns/?type=1&host=github.com&ip=)网站进行查询

![](./imgs/github-dns.png)

分别查询以下网址对应的`DNS`服务器地址

```
github.com
github.global.ssl.fastly.net
assets-cdn.github.com
```

将查询得到的最短响应时间的服务器`IP`放置到文件`/etc/hosts`文件中

```
$ cat /etc/hosts
...
...

52.74.223.119 github.com
69.171.248.65 github.global.ssl.fastly.net
185.199.111.153 assets-cdn.github.com
```

## 方式二（推荐）

配置公告`DNS`，参考[[Ubuntu 18.04][resolv.conf]公共DNS设置](https://zj-network-guide.readthedocs.io/zh_CN/latest/advanced/[Ubuntu%2018.04][resolv.conf]%E5%85%AC%E5%85%B1DNS%E8%AE%BE%E7%BD%AE/)