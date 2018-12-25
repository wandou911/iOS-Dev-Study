## iOS真机测试证书问题

### 如果自动管理签名 无法打包 需要revoke证书

1 xcode选择开发者账号

![选择开发者账号](https://ws3.sinaimg.cn/large/006tNbRwly1fycys8k02ej30tc0b4jst.jpg)


2 登陆[苹果开发者中心](https://developer.apple.com)

选择证书 点击revove

![revoke](https://ws4.sinaimg.cn/large/006tNbRwly1fycyyrct6nj315e0cg76u.jpg)

3 再次回到xcode 点击运行 会要求输入密码 选择always allow
就可以在真机运行了

![keychain](https://ws4.sinaimg.cn/large/006tNbRwly1fycz05ymyuj30om0b60vc.jpg)





