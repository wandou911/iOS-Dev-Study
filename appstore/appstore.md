## App Store 审核指南


### 提交之前 – 审核前核对清单

请确保：

* 测试 app 是否会发生崩溃、是否存在错误
* 确保所有 app 信息及元数据完整且正确
* 更新您的联系信息，以便 App Review 部门在需要时与您取得联系
* 提供有效的演示帐户和登录信息，以及审核 app 时所需的任何其他硬件或资源 (例如，登录凭证或示例二维码)
* 启用后台服务，以使其在审核期间处于活动和可用状态
* 在 App Review 备注中附上与非明显功能及 App 内购买项目相关的详细说明，包括支持文稿 (如适用)。如果由于地区锁定或其他限制而导致我们无法访问 app 的部分内容，请提供有关功能的视频链接
* 检查 app 是否遵循了其他文稿中的相关指南

```
1. 安全
1.1 令人反感的内容 1.2 用户生成的内容 1.3 儿童类别 1.4 人身伤害 1.5 开发者信息 1.6 数据安全

2. 性能 
2.1 App 完成度 2.2 Beta 测试 2.3 准确的元数据 2.4 硬件兼容性 2.5 软件要求

3. 业务
3.1 付款 3.1.1 App 内购买项目 3.1.2 订阅 3.1.3(a) “阅读器”App 3.1.3(b) 多平台服务 3.1.4 硬件相关内容 3.1.5 App 之外的商品和服务 3.1.6 Apple Pay 3.1.7 广告 
3.2 其他业务模式问题 3.2.1 可以接受 3.2.2 不可接受

4. 设计
4.1 抄袭者 4.2 最低功能要求 4.3 重复 App4.4 扩展 4.5 Apple 站点和服务 4.6 备选 App 图标 4.7 HTML5 游戏与聊天机器人 (Bot) 等

5. 法律
5.1 隐私 5.1.1 数据收集和存储 5.1.2 数据使用和共享 5.1.3 健康和健康研究 5.1.4 儿童 5.1.5 定位服务 5.2 知识产权 ￼5.3 游戏、赌博和彩票 5.4 VPN App 5.5 开发者行为准则
```

### 提交之后 – 预期事宜

在 App Store Connect 中提交 app 和元数据之后，您随即就会进入审核流程。请谨记以下几点：

* 时间：App Review 团队会尽快检查您的 app。不过，如果 app 比较复杂或者存在新的问题，则可能需要更深入的审查和考量。也请记住，如果 app 因为违反同一准则而一再被拒绝，或者您曾经试图操纵 App Review 流程，您的 app 将需要更长时间才能完成审核。进一步了解 App Review。
* 状态更新：App 的当前状态会反映在 App Store Connect 中，所以请多留意此处。
* 加急请求：如果您遇到了严重的时间问题，可以申请加急审核 (英文)。请仅在您真的需要加快审核时才提出申请，以便其他开发者的加急请求不受影响。如果我们发现您滥用此系统，从此以后我们可能都会拒绝您的申请。
* 发布日期：如果您设定在未来某个日期发布 app，在此日期到来之前，即使这个 app 已获得 App Review 团队的批准，也不会显示在 App Store 上。请注意，您的 app 可能需要长达 24 小时才能显示在所有选定的商店中。
* 拒绝：我们的目标是公平、持续地遵循这些准则，但是人无完人。如果您的 app 被拒绝，但您存在疑问，或希望提供其他信息，请使用解决方案中心，以与 App Review 团队直接沟通。这样可以帮助您的 app 出现在商店中，也可帮助我们改进 App Review 流程，并在我们的政策中发现需要阐明的部分。如果您仍对结果不满意，请提交申诉 (英文)。

## App Store 审核被拒的23个理由

iOS 应用提交审核要持续一周（现在大约2天），在提交之前，我们一定要进行「自我审查」，避免被拒。ASO100为大家收集整理了App Store 审核被拒的23个理由，并且附上官方拒绝理由原文，供大家上传应用时对照检查。

应用被拒分为两种：Binary Rejected 和 Metadata Rejected。前者需要重新上传应用并且重新排队，后者只需要修改信息，不需要重新上传应用。

1、应用内包含检查更新功能
iOS 应用的版本更新必须通过 App Store 进行，自身 App 内不能包含提示更新功能。从2015年3月起，所有包含检查更新功能的 App 都会被拒绝上架。

```
附被拒理由原文：
Your app includes an update button or alerts the user to update the app. To avoid user confusion, app version updates must utilize the iOS built-in update mechanism. We’ve attached screenshot(s) for your reference.
Next Steps
Please remove the update feature from your app. To distribute a new version of your app, upload the new app binary version into the same iTunes Connect record you created for the app’s previous version. Updated versions keep the same Apple ID, iTunes Connect ID (SKU), and bundle ID as the original version, and are available free to customers who purchased a previous version.
```

2、使用第三方登录时未做安装检测
接入第三方登录要检测是否安装了第三方客户端，未安装时不要显示对应按钮。2015年9月之前，通常可以采用判断未安装则隐藏登录按钮的方式。但目前隐藏 按钮的方式也可能被审核拒绝，QQ 和微博提供了 web 登录的方式，如果判断未安装，需要允许用户使用 webview 的登录方式。苹果在条款中有声明不允许 iOS 应用的正常使用需要依赖另外一个 App。

```
附被拒理由原文：
We noticed that third-party app QQ/WeChat is required to use third-party authentication method. The user should be able to login without installing additional applications.
Next Steps
If you choose to support third-party authentication, please use methods that can authenticate users from within your app, such as a native web-view.
```

3、采集设备IDFA但应用没有广告功能
从2014年2月起，Apple 开始拒绝采集 IDFA (identifier for advertising) 却未集成任何广告服务的应用进入 App Store。如果 App 本身没有广告，ASO100.com 建议可以在审核的时候显示一个 Banner 广告，并且放在比较明显的位置，审核通过后关掉即可。

```
附被拒理由原文：
We found that your app uses the iOS Advertising Identifier but does not include ad functionality. This does not comply with the terms of the iOS Developer Program License Agreement, as required by the App Store Review Guidelines.
Specifically, section 3.3.12 of the iOS Developer Program License Agreement states:
“You and Your Applications (and any third party with whom you have contracted to serve advertising) may us the Advertising Identifier, and any information obtained through the use of the Advertising Identifier, only for the purpose of serving advertising. If a user resets the Advertising Identifier, then You agree not to combine, correlate, link or otherwise associate, either directly or indirectly, the prior Advertising Identifier and any derived information with the reset Advertising Identifier.”
Please remove the iOS Advertising Identifier from your app or add ad functionality to your app.
```

4、含UGC却未提供用户协议及举报功能
如果你的 App 内有发帖等UGC（用户产生内容）功能，必须提供用户协议，并留有内容举报功能，否则就会被审核拒绝。

```
附被拒理由原文：
We found your app enables the display of user-generated content which may become sexually explicit. Therefore we ask that you put the following precautions in place, to ensure your app remains in compliance with the App Store Review Guidelines.
Use Moderators to flag and remove inappropriate content
Require that your users agree to terms (EULA) and these terms must be clear that there’s no tolerance for objectionable content
Users need a way to flag or report objectionable content and users generating this content
Developer must act on objectionable content reports within 24 hours by removing the content and ejecting the user who provided the offending content
Developer needs a method for ejecting users who violate the terms of the EULA
Please keep in mind that it is not sufficient for the user to report an issue through a general user feedback / 反馈 or like/dislike feature of the app. Please ensure that the contents that may become objectionable have a reporting or flagging mechanism readily accessible by the user to allow the user to promptly report or flag the issue and clearly identify the offending content.
```

5、上传时没有使用真实的应用截图
应用程序的名称、描述、截图或者预览与应用的内容和功能不相关将会被拒绝。有 App 因为应用截图使用的是自己设计的插画而被审核拒绝。

```
附被拒理由原文：
We noticed that your marketing screenshot(s) do not sufficiently reflect your app in use.We’ve attached screenshot(s) for your reference.
Next Steps
Please revise your screenshots to demonstrate the app functionality in use.
```

6、应用必须使用邀请码才能注册使用
苹果要求应用不能限制只有部分用户可以使用。

```
附被拒理由原文：
Your app arbitrarily restrict users by requiring invitation code to register, which is not allowed on the App Store. We’ve attached screenshot(s) for your reference.
Next Steps
Please revise your app to remove any functionality that limits who can use the app.
```

7、应用内出现第三方移动平台的名字或图标
一直以来，苹果都不允许iOS开发者在进行软件描述时提到 Android 版本，而自从2015年4月起，在 App 内、截图等任何地方提到安卓、Android 的文字、图标、系统界面都会被拒。曾经有电商 App，因为出现了售卖三星安卓手机而被拒。。。

```
附被拒理由原文：
We found that your app and/or its metadata contains inappropriate or irrelevant platform information, which is not in compliance with the App Store Review Guidelines.
Specifically, your app mentioned other platforms, such as Android.
Providing future platform compatibility plans, or other general platform references, is not appropriate in the context of the App Store. It would be appropriate to remove this information.
```

8、应用内涉及奖励，未声明与苹果无关
App 里有实物奖励的话，不能使用苹果产品（例如 iPhone 、iPad 等）作为奖品。另外一定要声明“奖励由本公司提供，与苹果官方无关”。

```
附被拒理由原文：
Your app includes a contest or sweepstakes but it does not:
Indicate that Apple is not involved in any way with the contest or sweepstakes.
Next Steps
It is necessary to:
Include official rules of the contest or sweepstakes in the app
Include an explicit statement in the contest or sweepstakes rules specifying that > Apple is not a sponsor
Ensure that the contest or sweepstake prizes are not Apple products
```

9、没有提供恢复内购的方法
增加一个“恢复购买记录”的按钮即可。

```
附被拒理由原文：
We found that your app offers In-App Purchase/s that can be restored but it does not include a “Restore” feature to allow users to restore the previously purchased In-App Purchase/s.
To restore previously purchased In-App Purchase products, it would be appropriate to provide a “Restore” button and initiate the restore process when the “Restore” button is tapped.
```

10、未注册时不能使用与账号无关的功能
对于资讯等 App，在没有进行与用户信息相关的操作时，却强行让用户登录，甚至不登录就无法看到任何内容，有可能会被拒绝。

```
附被拒理由原文：
We noticed that your app requires users to register with personal information to access non account-based features. Apps cannot require user registration prior to allowing access to app content and features that are not associated specifically to the user.
Specifically, your app forces users to login before they can read the news.
We features that your app requires users to register or log in, prior to accessing non account-based features. Apps cannot require user registration or login prior to allowing access to app content and features that are not associated specifically to the user.
Next Steps
User registration that requires the sharing of personal information must be optional or tied to account-specific functionality. Additionally, the requested information must be relevant to the features.
```

11、iPhone 应用在 iPad 上不能正常显示
iPhone程序必须不经修改就能以iPhone分辨率和2倍iPhone 3GS的分辨率在iPad上运行。即使你的App 只为 iPhone 用户提供，在 iPad 上也必须能够正常显示，否则审核会被拒绝。

```
附被拒理由原文：
We noticed that your app did not run at iPhone resolution when reviewed on iPad running iOS 9.1, which is a violation of the App Store Review Guidelines. We’ve attached screenshot(s) for your reference.
Specifically, the buttons at the bottom of the app are inaccessible when running on iPad.
Next Steps
Please revise your app to ensure it runs at iPhone resolution on iPad.
```

12、侵犯第三方版权
对于视频、音乐、图书类的应用很容易因为这一条而被拒。另外 ASO100.com 建议应用内最好不要出现第三方的商标，例如运营商的Logo、影视公司的 Logo 等。

```
附被拒理由原文一：
We found that your app allows users to download music without authorization from the relevant third-party sources.
We’ve attached screenshot(s) for your reference.
Next Steps
Please provide documentary evidence of your rights to allow music or video content download from third-party sources. If you do not have the requested permissions, please remove the music or video download functionality from your app.
附被拒理由原文二：
Your app includes content or features that resemble a well-known, third-party mark, Fox . We’ve attached screenshot for your reference.
Pursuant to your agreement with Apple, you represent and warrant that your application does not infringe the rights of another party, and that you are responsible for any liability to Apple because of a claim that your application infringes another party’s rights. Moreover, we may reject or remove your application for any reason, at our sole discretion.
Accordingly, please provide documentary evidence of rights to use this content. Once Legal has reviewed your documentation and confirms its validity, we will proceed with the review of your app.
```

13、应用截图、名称、描述等出现不雅词汇
在应用截图、名称、描述等任何地方出现例如诸如 牛逼、绿茶婊、无节操、逗比 等词汇，都会被苹果审核拒绝。

```
附被拒理由原文：
We found that your app contains content that many audiences would find objectionable, which is not in compliance with the App Store Review Guidelines.
Specifically, we noticed your app name 打飞机-简单粗暴 is objectionable.
We encourage you to review your app content and evaluate whether you can modify the content to bring it into compliance with the Guidelines.
```

14、应用出现 beta版、测试版字样
不要过度谦虚地在启动画面或者应用名称上加上”beta”字样，苹果不允许测试版产品上架。

```
附被拒理由原文：
Your app appears to be a pre-release, test, or trial version with a limited feature set. Apps that are created for demonstration or trial purposes are not appropriate for the App Store and do not comply with the App Store Review Guidelines.
To ensure compliance with the App Store Review Guidelines, it would be appropriate to revise your app to complete, remove, or fully configure any partially implemented feature(s).
If you would like to conduct beta trial for your app, you may wish to review the TestFlight Beta Testing Guide.
```

15、注册缺少隐私政策
如果应用包含注册功能，注册页面必须提供隐私说明协议按钮或者链接。另外在 iTunes connect 提交新版本的时候，Privacy Policy URL 必须要填写。

```
附被拒理由原文：
We noticed that your app includes account registration or access to users’ existing accounts but does not include a privacy policy, which does not comply with the App Store Review Guidelines.
Please update your app metadata to include a privacy policy and ensure that the privacy policy URL you provide directs the user to the intended destination.
```

16、应用出现崩溃、加载失败等 bug
审核期间出现崩溃会导致审核被拒。ASO100.com 建议，在审核期间务必保证服务器稳定，避免审核人员审核时出现内容加载失败的情况，导致被拒。

```
附被拒理由原文：
We discovered one or more bugs in your app when reviewed on iPhone running iOS 8.1.2 on both Wi-Fi and cellular networks.
Specifically, no content is fetched when users launch the app.Please see the attached screenshot/s for more information.
It would be appropriate to revise such issue(s) in your application.
Next Steps
Please run your app on a device to identify the issue(s), then revise and resubmit your app for review.
```

17、应用描述、截图和应用功能不符
如果应用的描述或截图介绍的功能在审核期间没有体现，则会被拒绝，如果介绍文案不够详细也会有一定概率被拒。

```
附被拒理由原文：
We found that your app did not achieve the core functionality described in your marketing materials or release notes, as required by the App Store Review Guidelines.
Specifically, your app does not include the feature of 微信朋友圈分享 that is written in your release note.
It would be appropriate to revise your app to ensure this feature is fully implemented or to revise your Application Description, Release Notes, and/or screenshots to remove this content.
```

18、应用包含应用推荐功能
除特殊情况，苹果明令禁止应用内推荐其他APP。

```
附被拒理由原文：
The 应用推荐 feature in your app displays or promotes third-party apps, which violates the App Store Review Guidelines. We’ve attached screenshot(s) for your reference.
Next Steps
Please remove the 应用推荐 feature from your app.
```

19、应用包含不正确的诊断功能
如果你的应用中，包含不真实的系统检测或优化功能，苹果会认为这项功能有误导用户的嫌疑，审核时会被拒绝。

```
附被拒理由原文：
We noticed that your app provides potentially inaccurate diagnostic functionality for iOS devices to the user.
We’ve attached screenshot(s) for your reference.
Next Steps
Currently, there is no publicly available infrastructure to support iOS diagnostic analysis. Therefore your app may report inaccurate information which could mislead or confuse your users. We encourage you to review your app concept and incorporate different content and features that are in compliance with the App Store Review Guidelines.
```

20、应用提交的新版本与上一版差异过大
如果你提交的新版本应用与上一版相比，功能上变化过大，比如将游戏升级为工具类应用，或在新版本中完全改掉前一版产品的功能，则会被苹果拒绝。

```
附被拒理由原文：
We found that your app did not achieve the core functionality described in your marketing materials or release notes, as required by the App Store Review Guidelines.
Specifically, the app has a whole content swap from a Game app to a Mobile Data Tracking app, which does not provide a good user experience when updating the app.
It would be appropriate to revise your app to ensure this feature is fully implemented or to revise your Application Description, Release Notes, and/or screenshots to remove this content.
If your iTunes Connect Application State is Rejected, a new binary will be required. Make the desired metadata changes when you upload the new binary.
```

21、应用违反当地法律法规
应用程序必须遵守上线地区的法律法规，禁止含有赌博、色情、有偿陪伴等违反法律的内容，尤其为用户提供付费社交服务的APP，例如在线直播类APP，必须严格遵守相关规定。

```
附被拒理由原文：
Your app contains content – or facilitates, enables, and encourages an activity – that is not legal in all of the locations where the app is available. Specifically, your app is advertised as a platform to provide paid companionship services.
We’ve attached screenshot(s) for your reference.
Next Steps
We encourage you to review your app concept and incorporate different content and features that are in compliance with the App Store Review Guidelines.
```

22、应用作者名与金融机构名字不一致
针对理财、P2P等金融相关产品，苹果增加规定
开发者的名字必须与APP内的金融机构名字保持一致，否则会被拒。
且由同一品牌的金融机构提供服务的APP，必须发布在同一个开发者账号跟名称下。
如果你已经代表委托人或者公司发布了这些APP，你的委托人或者公司应该注册iOS开发者账号，并把你添加到他们的开发者账号里，这样你就可以在他们账号下面提交并发布APP了。

```
附被拒理由原文：
We found that the Seller and/or Artist names associated with your app do not reflect the name of the financial institution in the app and/or its name and metadata.
To be appropriate for the App Store, your app must be published under a Seller name and Artist name that reflects the financial institution brand, as required by the iOS Developer Program License Agreement.
Section 1.2:
“You” and “Your” means and refers to the person(s) or legal entity (whether the company, organization, educational institution, or governmental agency, instrumentality, or department) using the Apple Software or otherwise exercising rights under this Agreement. For the sake of clarity, You may authorize contractors to develop Applications on Your behalf, but any such Applications must be submitted under Your developer account.
If you have published these apps on behalf of a client, it would be appropriate for your client to enroll in the iOS Developer Program, then add you to their development team so you can develop an app for them to submit under their developer account.
```

23、应用提供功能过于简单
应用内的功能不能太过单一，苹果虽然理念中提倡“简单”，但并不代表能接受功能不够完善的应用，他们对应用的核心要求，是希望能够给用户更有价值的体验。 当然，如果你的产品太有创意，可能苹果的审核员没能理解它的独到之处，这样的情况下，你可以通过申诉来更详细的描述产品优势，以便通过审核。

```
附被拒理由原文：
We found that your app only provides a very limited set of features. It only provides an augmented reality reader mechanism with no other functionality. While we value simplicity, we consider simplicity to be uncomplicated – not limited in features and functionality.
We understand that there are no hard and fast rules to define useful or entertaining, but Apple and Apple customers expect apps to provide a really great user experience. Apps should provide valuable utility or entertainment, draw people in by offering compelling capabilities or content, or enable people to do something they couldn’t do before or in a way they couldn’t do it before.
We encourage you to review your app concept and evaluate whether you can incorporate additional content and features to be in compliance with the Guidelines. For information on the basics of creating great apps, watch the video The Ingredients of Great Apps.If you feel we didn’t understand the features of your app, or that we missed key functionality, and your app was incorrectly rejected, you may appeal to the App Review Board.
```

### 被拒原因总结

我收集了 9 月 App 所有审核被拒的条款，取其中占比最大的前十名将其展现出来

![9 月 App 所有审核被拒](https://segmentfault.com/img/bVWBt7?w=622&h=513)

占比 TOP3 的分别是 条款 2.3 元数据、2.1 App 的完整度、4.3 重复 App/马甲包，其中最主要的被拒原因是 App 的元数据违规或不符合苹果规定，苹果一直对 App 的质量有一定的要求。那么图中 TOP10 都分别对应着哪些具体问题呢？简单说明一下：

2.3 元数据

主要是标题违规，少数情况是截图、icon 违规

2.1 App 完成度

Bug、IPv6 未搭载、测试账号、隐藏开关等

4.3 垃圾应用

重复应用、马甲包

0.10.0 程序许可协议

违反了开发者指南、设计指南、品牌和营销指南等，如 PLA 1.2 问题

3.1.1 支付问题

接入第三方支付

5.1 隐私

未得到允许采集用户信息、与第三方共享收集的用户数据等，例：位置、账号……

2.5 软件需求

产品加入违规代码

4.2 低质量应用

产品功能性差，如直接嵌套网页的 App

5.2 版权

未经授权，使用受版权保护的第三方材料、App不得与苹果现有产品类似等

1.1 不良内容

色情、暴力、政治、宗教等

我们收集了今年 7 月、8 月、9 月三个月份的审核被拒原因，并将其中 TOP10 整理出来进行了比照。如下图：

![近 3 个月被拒原因](https://segmentfault.com/img/bVWBwo?w=621&h=268)

从上图我们不难看出近期苹果的审核重点—TOP3 仍然是 2.3 元数据、2.1 App 完成度、4.3 垃圾应用。除此之外，近三个月内条款 5.1 法律问题、5.2 知识产权问题已然成为了苹果审核侧重点

#### 参考链接:

1 [App Store 审核指南](https://developer.apple.com/cn/app-store/review/guidelines/)

2 [App Store 审核被拒的23个理由](https://www.kancloud.cn/hongweizhiyuan/apple_developer/712226)

3 [App Store 9月被拒原因汇总](https://segmentfault.com/a/1190000011545079)

4 [Solve-App-Store-Review-Problem](https://github.com/wg689/Solve-App-Store-Review-Problem)
