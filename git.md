
## 画屏提交代码步骤

* fork 代码

* 克隆代码

	`git clone git@gitee.com:mnstar/iGallery.git`

* 检出分支
	
	`git checkout dev2.5.0`

* 打开xcode 修改代码

* 提交代码：

	1 先在网页更新自己的远端代码

	2 拉取代码到本地：

		`git pull`

	3 提交代码

	`git add -A`
	
	`git commit -m”更新说明”`

	4 推送到自己的远程

	`git push`

* pull request

## git 配置多个SSH-Key

我们在日常工作中会遇到公司有个gitlab，还有些自己的一些项目放在github上。这样就导致我们要配置不同的ssh-key对应不同的环境。下面我们来看看具体的操作：



### 1，生成一个公司用的SSH-Key     

```
$ ssh-keygen -t rsa -C "youremail@yourcompany.com” -f ~/.ssh/id-rsa
```

在~/.ssh/目录会生成id-rsa和id-rsa.pub私钥和公钥。 我们将id-rsa.pub中的内容粘帖到公司gitlab服务器的SSH-key的配置中。



### 2，生成一个github用的SSH-Key

```
$ ssh-keygen -t rsa -C "youremail@your.com” -f ~/.ssh/github-rsa
```

在~/.ssh/目录会生成github-rsa和github-rsa.pub私钥和公钥。 我们将github-rsa.pub中的内容粘帖到github服务器的SSH-key的配置中。



### 3，添加私钥
```
$ ssh-add ~/.ssh/id_rsa $ ssh-add ~/.ssh/github_rsa
```

如果执行ssh-add时提示"Could not open a connection to your authentication agent"，可以现执行命令：

```
$ ssh-agent bash
```

然后再运行ssh-add命令。

```
# 可以通过 ssh-add -l 来确私钥列表
$ ssh-add -l
# 可以通过 ssh-add -D 来清空私钥列表
$ ssh-add -D
```

### 4，修改配置文件

在 ~/.ssh 目录下新建一个config文件

```
touch config
```

添加内容
：
```
# gitlab
Host gitlab.com
HostName gitlab.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/github_rsa
```

### 5，目录结构

![图片](http://static.oschina.net/uploads/space/2015/1112/151152_7YR5_723271.png)

### 6，测试
```
$ ssh -T git@github.com
```

输出

Hi stefzhlg! You've successfully authenticated, but GitHub does not provide shell access.

就表示成功的连上github了.也可以试试链接公司的gitlab.

参考链接：

1 [git 配置多个SSH-Key](https://my.oschina.net/stefanzhlg/blog/529403)

