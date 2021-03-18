
# [GitLab]重置密码

昨天新建的账户，今天突然等不上去了，参考以下文章重置密码

[gitlab 重置用户密码](https://blog.csdn.net/shanpenghui/article/details/89195511)

[gitlab管理员密码忘记如何强制重置找回](https://jingyan.baidu.com/article/6525d4b181bd41ac7d2e94af.html)

进入`gitlab`管理后台。当前使用`docker`版本`gitlab`，所以先进入容器

```
$ docker exec -it CONTIANINER_ID bash
```

切换到`git`用户

```
$ su git
```

登录`gitlab-rails`

```
$ gitlab-rails console production
DEPRECATION WARNING: Passing the environment's name as a regular argument is deprecated and will be removed in the next Rails version. Please, use the -e option instead. (called from require at bin/rails:4)
--------------------------------------------------------------------------------
 GitLab:       12.4.2 (393a5bdafa2)
 GitLab Shell: 10.2.0
 PostgreSQL:   10.9
--------------------------------------------------------------------------------
Loading production environment (Rails 5.2.3)
irb(main):001:0>
```

（上面这一步有点慢），查询用户是否存在

```
irb(main):001:0> user=User.where(name: "zxxU").first
=> nil
irb(main):002:0> user=User.where(name: "zxxu").first
=> nil
irb(main):003:0> user=User.where(name: "zxxxn").first
=> #<User id:2 @zxxxU>
```

充值密码并确认

```
irb(main):005:0> user.password=12345678
=> 12345678
irb(main):006:0> user.password_confirmation=12345678
=> 12345678
```

保存并退出

```
irb(main):007:0> user.save
Enqueued ActionMailer::DeliveryJob (Job ID: 2b220e18-d0ac-415e-a1cc-52f31069d3be) to Sidekiq(mailers) with arguments: "DeviseMailer", "password_change", "deliver_now", #<GlobalID:0x00007f4e84a25510 @uri=#<URI::GID gid://gitlab/User/2>>
=> true
irb(main):008:0> quit
```