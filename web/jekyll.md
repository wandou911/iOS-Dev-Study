

### github pages 搭建遇到的问题

运行：`jekyll serve` 
报错：

#### [问题1:](https://ruby-china.org/topics/26844)
```
kernel_require.rb:55:in `require': cannot load such file -- bundler (LoadError) 错误 

```


解决方法：
1 重新安装bundler：`$ gem install bundler`
2 然后 `$ bundle install`

#### [问题2 ：](https://blog.csdn.net/moonclearner/article/details/52238033)

```
Could not find gem 'jekyll-sitemap' in any of the gem sources listed in your Gemfile. (Bundler::GemNotFound)
```
原因：这个问题很明显，提示没有(Bundler::GemNotFound)
解决方法：

```
$ cd 你的blog根目录  
$ bundle install
```

关于 Fork 之后的 404 错误

一般来说Fork之后修改仓库名就可以访问自己的博客了。

[对于出现的 404 问题：](https://github.com/qiubaiying/qiubaiying.github.io/issues/98)

1 检查仓库名是否正确

2 刷新浏览器，耐心等待一段时间
3 我个人认为 Github 的处理速度的问题，大部分人出现的404等一段时间就可以了。

4 当fork之后， 修改setting文件，访问自己的网站报404 时，建议修改一下CNAME 文件，在code下找到CNAME文件，将里面的内容改为：https://你的Github账号名.github.io，然后点底部的commit changes，应该就可以了

#### mac 设置ruby源

1 查看版本

```
$ ruby -v
ruby 2.3.3p222 (2016-11-21 revision 56859) [universal.x86_64-darwin17]

$ gem -v
2.5.2
```

2 更换源

因为Ruby的默认源使用的是cocoapods.org，国内访问这个网址有时候会有问题，网上的一种解决方案是将远替换成淘宝的，替换方式如下

```
$gem source -r https://rubygems.org/
$ gem source -a https://ruby.taobao.org
```

3 验证是否替换成功

`$ gem sources -l`

4 正常的输出结果：

```
CURRENT SOURCES　　　　　　　　　　　　

http://ruby.taobao.org/
```


