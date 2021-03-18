# ERROR

## 问题一：publickey denied

`ssh`连接失败，这个问题很迷，耗了`1`天时间，网上找了很多资料没有结果，有一个博客主也遇到了同样的问题，他最后解决是因为突然就可以了，我也一样

## 问题二：git is not in the sudoers file.  This incident will be reported.

是因为`git`没有添加到`sudo`权限，参考[xxx is not in the sudoers file.This incident will be reported.的解决方法](https://www.cnblogs.com/xiaochaoyxc/p/6206481.html)

1. 先切换到`ubuntu`用户

        $ su ubuntu

2. 赋予`sudo`文件写权限

        $ sudo chmod u+w /etc/sudoers

3. 修改文件`/etc/sudoers`

        $ sudo vim /etc/sudoers
        # 添加
        youuser ALL=(ALL) ALL

    表示允许用户`youuser`执行`sudo`命令(需要输入密码)

4. 撤销`sudo`文件写权限

        $ sudo chmod u-w /etc/sudoers

5. 重新切换回原来用户

        $ su git

## 问题三：perl: warning: Falling back to a fallback locale ("en_US.utf8").

```
$ sudo adduser zhujian
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
    LANGUAGE = (unset),
    LC_ALL = (unset),
    LC_MEASUREMENT = "zh_CN.UTF-8",
    LC_PAPER = "zh_CN.UTF-8",
    LC_MONETARY = "zh_CN.UTF-8",
    LC_NAME = "zh_CN.UTF-8",
    LC_ADDRESS = "zh_CN.UTF-8",
    LC_NUMERIC = "zh_CN.UTF-8",
    LC_TELEPHONE = "zh_CN.UTF-8",
    LC_IDENTIFICATION = "zh_CN.UTF-8",
    LC_TIME = "zh_CN.UTF-8",
    LANG = "en_US.utf8"
    are supported and installed on your system.
perl: warning: Falling back to a fallback locale ("en_US.utf8").
Adding user `zhujian'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC+VVpw5kOZBmzJYz/vngYpAAV61Fq9oChSflQFkfzr1sKHRqq2/sqeZD3gzPQZbrKWcHbuGCWyQOvm1gH+67gW+TpUO9DWeeHqo3h5rlCW+ElJcL/q4b+ZBVEmGDjzE+Sg+6wM+izBl5xzHDFeLhN3Yw1OVc2rwQFQ/CD6FSKdL4b5bt0/5rpu65sv7haXjfDMSEsIVgPY5behLzZzoXy81iN4/tPF3cjDsn/x5Yywc60LdslJ5hW5wlozhq1LibUXk9JQu/+5DDZKi8ytMEoe1S7yROvaC/ofJQR22hINnFoLNBC8gSFM2YR+t9oBF0eiAaVwfgddA0+ScYrWA5Yr zj@zj-ThinkPad-T470p ...
Adding new group `zhujian' (1000) ...
Adding new user `zhujian' (1000) with group `zhujian' ...
Creating home directory `/home/zhujian' ...
...
...
```

提示语言包问题，参考[perl: warning: Falling back to a fallback locale ("en_US.UTF-8")](https://blog.csdn.net/jmpjmpkiss/article/details/55098794)

    $ sudo apt install locales-all

## 问题四：`remote: error: cannot lock ref 'refs/heads/master': ref refs/heads/master`

在`Travis CI`上上传文件到远程仓库，出现如下问题

    remote: error: cannot lock ref 'refs/heads/master': ref refs/heads/master

### 起因

我在上传提交时中间中断了

    $ git push -u origin dev
    Counting objects: 6, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (6/6), done.
    Writing objects: 100% (6/6), 556 bytes | 0 bytes/s, done.
    Total 6 (delta 5), reused 0 (delta 0)
    remote: Resolving deltas: 100% (5/5), completed with 5 local objects.
    ^C

然后再更新文章后再一次提交，就出现了远程仓库锁定的问题

### 解决

参考：[git: error: cannot lock ref, error: cannot lock ref](https://blog.csdn.net/sinat_36246371/article/details/79959598)

将远程仓库下载到本地，然后执行如下命令

    git remote prune origin

其作用是同步本地远程分支，删除本地已过时的远程分支

重新触发`CI`工具执行，此时能够成功更新了

## 问题五：error: RPC failed; curl 56 GnuTLS recv error (-9)

### 问题描述

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

### 解析

参考[git error: RPC failed; curl 56 GnuTLS](https://stackoverflow.com/questions/38378914/git-error-rpc-failed-curl-56-gnutls)和[Git 克隆错误‘RPC failed; curl 56 Recv failure....’ 及克隆速度慢问题解决](https://blog.csdn.net/qq_34121797/article/details/79561110)，有可能是`http缓存不够`或者`网络不稳定`问题

* 对于网络不稳定问题

>Rebuilding git with openssl instead of gnutls fixed my problem.

* 对于`http`缓存不够

```
# httpBuffer加大    
$ git config --global http.postBuffer 524288000
```

### 解决

重新设置了`http`缓存，不过最后是通过码云的方式解决的

1. 先将`Github`仓库拉取到码云仓库
2. 在从码云上下载

## 问题六：fatal: 无法读取远程仓库。

```
$ git clone ssh://git@gitlab.zhujian.tech:7020/zjykzj/hexo-blog.git
正克隆到 'hexo-blog'...
remote: 
remote: ========================================================================
remote: 
remote: The project you were looking for could not be found.
remote: 
remote: ========================================================================
remote: 
fatal: 无法读取远程仓库。

请确认您有正确的访问权限并且仓库存在。
```

参考：[How to fix 'The project you were looking for could not be found' when using git clone](https://stackoverflow.com/questions/54571213/how-to-fix-the-project-you-were-looking-for-could-not-be-found-when-using-git)

添加私钥

```
eval "$(ssh-agent -s)"

ssh-add ~/.ssh/<id_rsa>
```

## 问题七：fatal: 无法读取远程仓库。

```
$ git push origin master 
ssh: connect to host ssh.github.com port 443: Connection timed out
fatal: 无法读取远程仓库。

请确认您有正确的访问权限并且仓库存在。
```

1. 激活私钥
2. 测试远程登录
3. 代理（推荐）

参考：[git上传代码报错ssh: connect to host github.com port 22: Connection timed out解决办法](https://blog.csdn.net/qq_42146613/article/details/82772734)

## 问题八：gnutls_handshake() failed: Error in the pull function

参考：[使用curl出现gnutls_handshake() failed: Error in the pull function或者GnuTLS recv error: Error in the pull](https://blog.csdn.net/anlian523/article/details/90729063)

* 方法一：`sudo apt-get install libcurl4-openssl-dev`
* 方法二：开启代理（推荐）