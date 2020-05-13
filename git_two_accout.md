
# github 一个电脑配置多个账号

## 思路

ssh 方式链接到 Github，需要唯一的公钥，如果想同一台电脑绑定两个Github 帐号，需要两个条件:

- 能够生成两对 私钥/公钥
- push 时，可以区分两个账户，推送到相应的仓库

解决方案:

- 生成 私钥/公钥 时，密钥文件命名避免重复
- 设置不同 Host 对应同一 HostName 但密钥不同
- 取消 git 全局用户名/邮箱设置，为每个仓库独立设置 用户名/邮箱

## 操作方法

- 查看已有 密钥

`Mac 下输入命令 ls ~/.ssh/，看到 id_rsa 与 id_rsa_pub 则说明已经有一对密钥。`

- 生成新的公钥，并命名为 id_rsa_2 (保证与之前密钥文件名称不同即可)

`ssh-keygen -t rsa -f ~/.ssh/id_rsa_2 -C "yourmail@xxx.com"`

- 在 .ssh 文件夹下新建 config 文件并编辑，另不同 Host 实际映射到同一 HostName，但密钥文件不同。Host 前缀可自定义，例子中ieit

```
# default                                                                       
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa
# two                                                                           
Host ieit.github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa_2
```

- 将生成的 id_rsa.pub，id_rsa_2.pub内容copy 到对应的 repo


参考教程: [使用SSH密钥连接Github【图文教程】](http://www.xuanfengge.com/using-ssh-key-link-github-photo-tour.html)

- 测试 ssh 链接

```
ssh -T git@ieit.github.com
ssh -T git@github.com
# Hi IEIT! You've successfully authenticated, but GitHub does not provide shell access.
# 出现上边这句，表示链接成功
```

- 将项目 `clone` 到本地， `folder-name` 是本地文件夹路径

```
git clone git@github.com:whatever folder-name
```

- 取消全局 用户名/邮箱设置，并进入项目文件夹单独设置

```
# 取消全局 用户名/邮箱 配置
git config –global –unset user.name
git config –global –unset user.email
# 单独设置每个repo 用户名/邮箱
git config user.email “xxxx@xx.com”
git config user.name “xxxx”
```

- 命令行进入项目目录，重建 origin (whatever 为相应项目地址)

```
git remote rm origin
git remote add origin git@ieit.github.com:whatever
```

- 成功，可以 push 测试一下
```
git push origin master
```

参考链接：

1 [一台电脑绑定两个github帐号教程](https://www.jianshu.com/p/3fc93c16ad2d)

2 [如何在一台电脑上设置多个github账号](https://www.shenxt.info/post/2020-03-11-multi-github-in-one-pc/)

3 [Git 最著名报错 “ERROR: Permission to XXX.git denied to user”终极解决方案](https://www.jianshu.com/p/12badb7e6c10)