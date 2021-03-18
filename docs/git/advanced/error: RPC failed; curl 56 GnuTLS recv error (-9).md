
# error: RPC failed; curl 56 GnuTLS recv error (-9)

## 问题描述

下载`Github`仓库时出现如下错误

```
remote: Enumerating objects: 150, done.
remote: Counting objects: 100% (150/150), done.
remote: Compressing objects: 100% (90/90), done.
error: RPC failed; curl 56 GnuTLS recv error (-9): A TLS packet with unexpected length was received.
fatal: The remote end hung up unexpectedly
fatal: 过早的文件结束符（EOF）
fatal: index-pack 失败
```

## 解析

参考[git error: RPC failed; curl 56 GnuTLS](https://stackoverflow.com/questions/38378914/git-error-rpc-failed-curl-56-gnutls)和[Git 克隆错误‘RPC failed; curl 56 Recv failure....’ 及克隆速度慢问题解决](https://blog.csdn.net/qq_34121797/article/details/79561110)，有可能是`http缓存不够`或者`网络不稳定`问题

* 对于网络不稳定问题

>Rebuilding git with openssl instead of gnutls fixed my problem.

* 对于`http`缓存不够

```
# httpBuffer加大    
$ git config --global http.postBuffer 524288000
```

## 解决

重新设置了`http`缓存，不过最后是通过码云的方式解决的

1. 先将`Github`仓库拉取到码云仓库
2. 在从码云上下载