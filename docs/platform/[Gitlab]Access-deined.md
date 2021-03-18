
# Access deined: You do not have permission push to this repository

在gitee上新建了一个账户，在上面新建一个仓库，将其ssh链接设置到本地已存在的仓库上，想要把本地仓库推送到远程仓库，出现如下错误：

```
$ git push origin master 
Access deined: You do not have permission push to this repository
fatal: 无法读取远程仓库。

请确认您有正确的访问权限并且仓库存在。
```

其原因在于本地新建了两个`ssh`密钥，设置在`gitee`的不同账户上，ssh使用之前的密钥读取gitee远程仓库，导致出错。参考[如何使用特定的SSH Key提交GIT](https://www.jianshu.com/p/82aa1678411e)

在`~/.ssh/config`文件上添加如下内容

```
Host gitee.com
	HostName gitee.com
	User git
	IdentityFile 私钥文件路径
	IdentitiesOnly yes
```

重新提交即可