
# [github][gitee]SSH公钥设置

## [github]公钥设置

参考：[Adding a new SSH key to your GitHub account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

登录`github`，进入个人主页，选择`Settings->SSH and GPG keys->New SSH key`

填写`title`，并复制个人主机中的公钥到`key`

    $ cat github_id_rsa.pub 
    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDIUsnRNu/+Zeurm2Ty/Xac+q+0y87aHWr0N7fb+gygQK7xRux9UAI7UK3GwP7dwxYT8KTOrxf0tPnI4d/bCtETHcoj0D2UlwMO20FWFaoOocteccJLbmQ9XXsrt05KlJcDGr9L8e9eMyWKj5ZXMOxSwravv+e64XGkFaAmNX4XkCkENlZcIq6w+Fo/xtyPZA0W/oYnBWAvKd937GbKEA1m1rARzo/xGCn8uf76PUlNy2UscujnWbMUYGeLxf5jRCgWD0KZLJsJAsOCxczeRn0EAczgNcgyBbjotDnpTKbP6Xtqvf3TtVty9fgQgs7/oLNb8K+v0XVVR9XsX+DZkqF+JCzIOf+0dpnJiery187rw4MuRIlct+vGM1P+FaiPphh2vMhe5YEaFErrHNTDZiw+LbHCE3Eo9wK9t0wb/yFiHELempoZI+K3Zjv6cnUnl3urXQFHV/RJCj/JHOEA1Q3jvVLa3nETRMfBBEiDuK0YPH6OUac+GSg+ldCVwDydeCa2Z4/OdgZqsoyTU5o4vewbT3vKwmQGfu7BNOmHgnIzMZQsg0JWScDX9/c/DoCaGW95ej68niZ3ICtUWnlYKZVlzg+cyIRzuzSmaa5ecOgzxZ6moW4wRGrvMM94X0HMmWWXXV/WLXiUG2KN1upz7m78zwJ6ZXvh2sWmCe+q+YhJIw== github.com

`github`上设置的公钥同时具备`推送/拉取`的权限

### 密钥失效

参考：[About SSH](https://help.github.com/articles/about-ssh/)

    If you haven't used your SSH key for a year, then GitHub will automatically delete your inactive SSH key as a security precaution. For more information, see "Deleted or missing SSH keys."

`github`规定自动删除一年内未使用的`SSH`密钥

## [gitee]公钥设置

参考：

[公钥管理](https://gitee.com/help/articles/4180)

[SSH 公钥设置](https://gitee.com/help/articles/4191#article-header0)

码云可以在个人主页上设置公钥，也可以在个人仓库上设置公钥，这两个地方的读写权限不一致

### 个人主页

登录码云，选择`设置->安全设置->SSH公钥`，在添加公钥页面输入标题和公钥即可设置

在个人主页上设置的公钥同时具备`推送/拉取`的权限

### 个人仓库

进入仓库页面，选择`管理->部署公钥管理->公钥管理`，点击添加公钥选项，输入标题和公钥即可

在个人仓库上设置的公钥仅具备`拉取仓库代码`的功能

## 测试

参考：[Testing your SSH connection](https://help.github.com/articles/testing-your-ssh-connection/)

在`github`上设置好公钥之后

    SSH
    zj-github
    d9:fc:d8:02:ee:6c:75:68:a1xxx Added on Feb 4, 2019 Last used within the last week — Read/write 

在本地测试是否成功

    $ ssh -T git@github.com
    Hi zjZSTU! You've successfully authenticated, but GitHub does not provide shell access.
    $ ssh -T git@gitee.com
    Hi zjZSTU! You've successfully authenticated, but GITEE.COM does not provide shell access.

## 下载代码

选择仓库，以`ssh`协议下载

    $ git clone git@github.com:zjZSTU/git-guide.git

这一次会要求你输入设置好的密码(`passphrase`)，之后的拉取代码操作都可以自动认证完成