## App Store 内购审核过程

### 第1次提交 
打算上内购功能，在提交时候不小心勾选了内购的选项，还有内购的商品

被拒：Nov 28, 2018 at 11:03 PM


```
Nov 28, 2018 at 11:03 PM
From Apple
3. Business: Preamble
Guideline 3.0 - Business


We began the review of your app, but we are not able to continue because we need additional information about your app.

Please reply to this message in Resolution Center to confirm that the price of your 6986艺点, 149.99 USD, is the intended price. If you have additional information about your app, please include it in your response as well.

Once we receive your confirmation, we will continue with the review of your app.



Since your App Store Connect status is Metadata Rejected, we do NOT require a new binary. To revise the metadata, visit App Store Connect to select your app and revise the desired metadata values. Once you’ve completed all changes, reply to this message in Resolution Center and we will continue the review.
```
我们的回复：Nov 29, 2018 at 9:41 AM

```
Nov 29, 2018 at 9:41 AM
From iart@boe.com.cn (Beijing BOE Artcloud Technology Co. Ltd)
您好，我们3.0.2版本还没有加APP内购项目，我们只是在3.0.2版本修改了几个小bug，希望你们能继续审核。
```


### 第2次提交

被拒：Nov 30, 2018 at 6:08 AM
原因：在app有购买虚拟商品，但是没有走苹果内购
```
Nov 30, 2018 at 6:08 AM
From Apple
2. 1 Performance: App Completeness
Guideline 2.1 - Performance - App Completeness


Thank you for resubmitting your app. We have continued the review and would like to provide our findings.

We found that while you have submitted in-app purchase products for your app, the in-app purchase functionality is not present in your binary.

Next Steps

If you would like to include in-app purchases in your app, you will need to upload a new binary that incorporates the in-app purchase API to enable users to make a purchase.

Once you revise and resubmit your binary, you will also need to resubmit your in-app purchases for review since they are in the Developer Action Required state. For each in-app purchase product submitted, please be sure to edit the detail information or cancel the request to change the detail information for the in-app purchases using App Store Connect.

Alternatively, if you do not want to include in-app purchase products in your app, it would be appropriate to remove any unused in-app purchase products from App Store Connect.

Resources

For more information on how to implement in-app purchase in your app, please refer to the In-App Purchase Programming Guide.

Learn more about offering in-app purchases in App Store Connect Help.
```

我们的操作：把内购商品删掉，再次提交
## 第3次提交

被拒：Dec 2, 2018 at 8:00 AM

原因：
1 在app有购买虚拟商品，但是没有走苹果内购
2 强制要求用户认证

```
Dec 2, 2018 at 8:00 AM
From Apple
3. 1.1 Business: Payments - In-App Purchase
5. 1.1 Legal: Privacy - Data Collection and Storage
Guideline 3.1.1 - Business - Payments - In-App Purchase


We noticed that your app or its metadata enables the purchase of content, services, or functionality in the app by means other than the in-app purchase API, which is not appropriate for the App Store.

Specifically, your app enables points, or intermediate currencies, without using the in-app purchase API. Additionally, please note that the cost of the points or the intermediate currency cannot be included in the purchase price of the app.

Next Steps

While the payment system that you have included may conduct the transaction outside of the app, if the purchasable content, functionality, or services are intended to be used in the app, they must be purchased using in-app purchase, within the app - unless it is of the type referenced in guideline 3.1.3 of the App Store Review Guidelines.

In-App Purchase

It may be appropriate to revise your app to use the in-app purchase API to provide content purchasing functionality.

In-app purchase provides several benefits, including:

- The flexibility to support a variety of business models.
- Impacting your app ranking by consolidating your sales to one app rather than distributing them across multiple apps.
- An effective marketing vehicle to drive additional sales of new content.

For information on in-app purchase, please refer to the following documentation:

In-App Purchase for Developers

In-App Purchase Programming Guide

For step-by-step instructions on in-app purchase creation within App Store Connect, refer to App Store Connect Help.

Guideline 5.1.1 - Legal - Privacy - Data Collection and Storage


We noticed that your app requires users to register with Chinese National ID and passport number to post “public works”, which does not comply with the App Store Review Guidelines.

Apps cannot require user registration prior to allowing access to app content and features that are not associated specifically to the user.

Next Steps

User registration that requires the sharing of personal information must be optional or tied to account-specific functionality.

To resolve this issue, please make it clear to the user that registering will enable them to access the content from any of their iOS devices and provide them a way to register at any time, if they wish to later extend access to additional iOS devices.

Please note that although guideline 3.1.2 of the App Store Review Guidelines requires an app to make subscription content available to all the iOS devices owned by a single user, it is not appropriate to force user registration to meet this requirement; such user registration must be made optional.



Please see attached screenshots for details.
```

苹果截图：

![限量收藏](https://ws2.sinaimg.cn/large/006tNbRwly1fyar2beib4j30u0140gol.jpg)

![支付宝支付](https://ws3.sinaimg.cn/large/006tNbRwly1fyar3kdeqdj30u0140tbf.jpg)

![用户认证](https://ws2.sinaimg.cn/large/006tNbRwly1fyar3z7n85j30u01400w2.jpg)

我们的回复：

1 声明购买的作品是推送到硬件的，而不是在app内使用

2 发布公开作品要求用户认证是遵守国家网络安全法

并且录了个视频演示如果购买作品并推送到硬件设备

```
Dec 3, 2018 at 11:02 PM
From iart@boe.com.cn (Beijing BOE Artcloud Technology Co. Ltd)
Dear APPLE team，
The following are our explanations about the two problems in your email.

1) 3. 1.1 Business: Payments - In-App Purchase
The limited collection of the items on our platform is used for our hardware rather than for the APP. Users can push specified pictures to the screen of our hardwares after the purchase. We just attached a detailed video to explain it.

2) 5. 1.1 Legal: Privacy - Data Collection and Storage
Only Certified Users can post ‘public works’ which can be seen and purchased by our users. According to the Chinese internet security laws, users must verify the ID before they make public opinions and public behaviors, including the ‘public works’. And if you don't want to upload your identity , you can only upload private works, which can’t be seen by others.
limited_collection.mov
```

## 第4次提交

被拒：Dec 5, 2018 at 7:33 AM
原因：购买的商品和服务是在app内使用的，但是没有走苹果内购

```
Guideline 3.1.1 - Business - Payments - In-App Purchase


We noticed that your app or its metadata enables the purchase of content, services, or functionality in the app by means other than the in-app purchase API, which is not appropriate for the App Store.

Specifically, your app enables points, or intermediate currencies, without using the in-app purchase API. Additionally, please note that the cost of the points or the intermediate currency cannot be included in the purchase price of the app.

Next Steps

While the payment system that you have included may conduct the transaction outside of the app, if the purchasable content, functionality, or services are intended to be used in the app, they must be purchased using in-app purchase, within the app - unless it is of the type referenced in guideline 3.1.3 of the App Store Review Guidelines.
```

解决方案：加入苹果内购功能，再次提交审核

## 第5次提交

被拒：在app里面有使用内购充值买艺点，但是找不消费地方。
原因：苹果没有找到在哪里消费艺点

```
Guideline 3.1.1 - Business - Payments - In-App Purchase


We noticed that your app uses in-app purchase products to purchase credits or currencies that are not consumed within the app, which is not appropriate for the App Store.

Next Steps

To resolve this issue, please revise your app to ensure that the credits or currencies purchased with in-app purchase products are used within the app or remove the in-app purchases entirely.
```

解决方法：
在Resolution Center给苹果发送截图，录视频，告诉苹果如何使用艺点购买作品

备注：因为这个被拒了3次，第一次，只发了截图，简单说明了一下，苹果还是没有找到如何消费；第二次，发截图，录视频，再加上解释，苹果依然没有找到；第三次，详细解释，录视频，苹果终于看懂了

## 第6次提交
被拒：

1 我们在支付教程里面，导航栏title 写了苹果支付教程，苹果认为有误导用户

2 我们的app里面有余额提现功能，苹果不知道余额是从哪里来的

```
Guideline 1.1.6 - Safety - Objectionable Content


We noticed that your app’s in-app purchase products are mislabeled as Apple Pay, which could confuse and mislead users.

Next Steps

To resolve this issue, please revise your app so that all in-app purchase products include accurate and clear labels. If your app does not include any Apple Pay functionality, please remove any references to Apple Pay from your app and its metadata.

Guideline 2.1 - Information Needed


We have started the review of your app, but we are not able to continue because we need additional information about your app.

Next Steps

To help us proceed with the review of your app, please provide detailed information to the following questions. The more information you can provide upfront, the sooner we can complete your review.

- Please explain who provides reward for identified artists for their public works in the 余额 section? 
```

解释：

1 余额是艺术家在平台上销售自己的作品，平台给的佣金

2 移除苹果支付字眼

## 第7次提交

被拒：


```
you have included may conduct the transaction outside of the app, if the purchasable content, functionality, or services are intended to be used in the app, they must be purchased using in-app purchase, within the app - unless it is of the type referenced in guideline 3.1.3 of the App Store Review Guidelines.
```

大意就是：如果购买的商品是虚拟商品，就必须使用苹果内购，如果是实体商品，就不能使用苹果内购 。

被拒原文：

```
Guideline 3.1.1 - Business - Payments - In-App Purchase


We noticed that your app or its metadata enables the purchase of content, services, or functionality in the app by means other than the in-app purchase API, which is not appropriate for the App Store.

Specifically, your app enables points, or intermediate currencies, without using the in-app purchase API. Additionally, please note that the cost of the points or the intermediate currency cannot be included in the purchase price of the app.

Next Steps

While the payment system that you have included may conduct the transaction outside of the app, if the purchasable content, functionality, or services are intended to be used in the app, they must be purchased using in-app purchase, within the app - unless it is of the type referenced in guideline 3.1.3 of the App Store Review Guidelines.
```


解释：
我们的app有虚拟商品和实体商品。虚拟商品仅仅使用苹果内购支付；实体商品可以使用支付宝和苹果内购混合支付

## 第8次提交

被拒：

```
Guideline 3.1.5 - Business - Payments - Physical Goods and Services Outside of the App


Your app allows users to purchase physical goods or services using the in-app purchase API, which is not appropriate for the App Store.

Next Steps

To resolve this issue, please revise your app to use a different purchasing mechanism for physical goods.

```


大意就是：app使用苹果内购购买实体商品，这是不符合苹果规范的

![真品购买](https://ws3.sinaimg.cn/large/006tNbRwly1fyiq42mxmcj30u0140jw6.jpg)
最后在真品购买去掉了苹果内购，提交审核


## 总结
这次审核从11.29号开始审核，一直经过11.22号苹果圣诞节放假，提交了10次，都没有通过。历时一个多月

究其原因：栽在两个主要问题上，Guideline 3.1.1，Guideline 3.1.5

简单来说：苹果内购审核原则就是虚拟商品只能走内购，实体商品不能走内购


1 ，就是还是没有弄清楚内购的原理。有时候在同一个问题上反复被拒，浪费了好多时间。

2 我们在上线苹果内购的时候，一次上的功能太多，既有虚拟商品，又有实体商品，导致苹果审核有一点问题就被拒，反复解释苹果也无法理解。所以在上线的时候，一次最好只上线一个功能，苹果审核就很容易通过。



#### 参考文献：

[App Store 审核指南](https://developer.apple.com/cn/app-store/review/guidelines/)




