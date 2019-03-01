iOS 上线故障记录


新的版本后台接口开启全站https，旧的版本http访问被自动转换为https，post请求变为get请求，因为后台接口不支持get请求，就引起接口报错。
后来后台接口临时做调整，支持get请求，暂时问题解决，可是post请求的参数就没法传过去了

备注：另外android没有问题，能够正常访问

网络请求用的[YTKNetwork](https://github.com/yuantiku/YTKNetwork)+ AFNetworking

![](https://ws4.sinaimg.cn/large/006tKfTcly1g0nba8ietgj31kv0u07iy.jpg)

网上查了很多文章，也看了猿题库github上的issue，说是网络重定向的问题，可以通过：
 [AFHTTPSessionManager setTaskWillPerformHTTPRedirectionBlock] 判断网络状态。

```
AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];
[manager setTaskWillPerformHTTPRedirectionBlock:^NSURLRequest * _Nonnull(NSURLSession * _Nonnull session, NSURLSessionTask * _Nonnull task, NSURLResponse * _Nonnull response, NSURLRequest * _Nonnull request) {
    NSLog(@"%@", request.URL);
    // This will be called if the URL redirects
    return request; // return request to follow the redirect, or return nil to stop the redirect
}];
[manager GET:_URLString parameters:nil progress:nil success:^(NSURLSessionTask *task, id responseObject) {
    NSLog(@"Response: %@", responseObject);
} failure:^(NSURLSessionTask *operation, NSError *error) {
    NSLog(@"Error: %@", error);
}];
```



参考链接：

1 [Nginx部署HTTPS服务过程与异常处理实践](https://juejin.im/post/5b73a1656fb9a0099b0fb0f0)

2 [关于重定向currentRequest 和 originalRequest ](https://github.com/yuantiku/YTKNetwork/issues/228)

3 [iOS 防 DNS 污染方案调研（五）--- 302等 URL 重定向业务场景](https://github.com/ChenYilong/iOSBlog/issues/15)

4 [AFNetworking 3.0 migration for redirect block
](https://stackoverflow.com/questions/37487533/afnetworking-3-0-migration-for-redirect-block)