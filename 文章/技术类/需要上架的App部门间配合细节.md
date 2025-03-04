# App上架需知


## 为了啥？
  本文目的是为了在上架之前尽可能的向各大应用市场的政策靠拢，减少被打回的次数；本文内容是基于`启明智云` 、`中星快充`无数次的上架驳回积累的血与泪的经验完成的。
## 共同注意
1、将推送、广告等设置统一开关；隐私政策里  ，应用没广告的话别写上广告营销相关的字眼   
2、各应用市场上提交的隐私政策网址内容   要和 应用 里的隐私政策内容保持一致 ，各类协议中的主体名称、应用名称尤其要一致  ，例如主体：`山东中星快充新能源发展有限公司`，应用名`中星快充`  
3、没开发完的、开发完有异常的功能入口隐藏，例如 某充电桩应用的微信支付由于政策原因无法正常支付，需要对用户做出对应的提示，甚至直接隐藏微信支付入口  ；  
4、不可出现任何的测试数据，无论多隐蔽的界面  ，不能是空白列表   必须有数据  ；
## 客户、运营与市场部门注意事项
1、如客户要上架`Google Play`，或用到`FaceBook`等海外平台，需要客户提供一台随时可用于远程操作的海外电脑，或者海外的windows服务器，以防账号异地登录被封禁 ；
## 客服行政部门注意事项

## 后端工程师注意事项
1、支付金额必须与界面显示的一致  不能是测试用的小额 （此问题建议在内测阶段就直接改成真实金额 ，测试完毕每隔几小时进行退款即可 ）  
2、必须提供帐号注销服务   
## Android工程师需知
1、移除工程中清单文件中冗余权限  
2、主界面用不到的权限   等到用的时候再去申请 ;每个权限点拒绝测试一下，避免出现重复申请被拒绝的权限的情况 ；  
3、 vivo 可能需要V1签名，[方案](https://segmentfault.com/n/1330000041338709)  
4、启动页加载完后显示“隐私政策页”，用户可以同意或不同意，这个弹框加载之前不能申请权限，甚至不可以进行sdk的初始化 ，这一点华为要求极为严格  
5、查看gradle里 /Flutter工程的pubspec.yaml 里的三方依赖 ，涉及隐私敏感数据、用户信息 直接到隐私政策里写明用途、获取方式、使用范围 ；


### 附 上架被驳回的真实案例

1、【隐私政策问题】应用内（首次弹窗“隐私政策/用户协议”打不开/内容空白），请修改后重新提交审核。（整改教程：https://wikinew.open.qq.com/index.html#/iwiki/4007776059）  
2、【隐私问题】APP注册/登录底部下无"隐私协议"，请修改后重新提交审核。（整改教程：https://wikinew.open.qq.com/index.html#/iwiki/4007776059）  
3、【隐私政策问题】APP提供账号注册登录功能，隐私政策内缺少账号注销流程说明，请补充账号注销规则后重新提交审核。（常用注销方式：APP内提供注销按钮、预留客服电话注销、预留邮箱发邮件注销、通过网址在线注销等）  
4、【资质问题】APP涉及网赚功能/属于网赚类，需要提供：平台【网赚承诺】，请在版权证明处上传相关材料扫描件后重新提交。（承诺书模版下载地址https://yybopen.material.qq.com/wiki/bd1a91d45887a6498b1fc49cc968d94b.docx）  
5、【资质问题】APP涉及购物内容，需要提供：1、营业执照需要包含相关批发、零售或商品销售等，2、平台【购物类承诺函】（承诺书模板下载：https://d3g.qq.com/qzone/%E5%BA%94%E7%94%A8%E5%8F%91%E5%B8%83%E6%89%BF%E8%AF%BA%E5%87%BD%E3%80%90%E7%BD%91%E7%BB%9C%E8%B4%AD%E7%89%A9%E7%B1%BB%E3%80%91%E6%A8%A1%E6%9D%BF.docx）等资质，请在版权证明处上传相关材料扫描件后重新提交。（详情请查看帮助4.2.2：https://wikinew.open.qq.com/index.html#/iwiki/4007776097)  
6、【隐私问题】APP里未发现隐私政策的常驻入口，请修改后重新提交审核。（整改教程：https://wikinew.open.qq.com/index.html#/iwiki/4007776059）  
7、【隐私检测问题】APP/SDK在同意隐私政策前，获取【 获取Android_ID 】。请在报告页面下载堆栈信息进行定位修改：①APP同意前获取行为，在"同意"按钮加入判定函数，当用户点击"同意"后，在调用系统API。②SDK同意前获取行为，升级SDK到最新版本，按照官网教程将初始化SDK时机放在用户点击"同意"后。  
检测报告：https://app.open.qq.com/p/privacy/detail?appId=1112401008
（隐私整改教程：https://wikinew.open.qq.com/index.html#/iwiki/4007776061）  
【隐私检测问题】隐私政策内容缺少【获取Android_ID 】，请在隐私政策文本/URL进行补充。检测报告：https://app.open.qq.com/p/privacy/detail?appId=1112401008  
（隐私整改教程：https://wikinew.open.qq.com/index.html#/iwiki/4007776062）
#### flutter 工程特定
1- 您的应用存在隐藏最近任务列表名称的行为，不符合华为应用市场《审核指南》第2.19项。  解决方案：创建项目时，MaterialApp-title 属性写app名称
```
GetMaterialApp(
          title: MyString.app_name,// 一定调用统一名称 
          theme: currentTheme,
          home: MainPage(),
          builder: (context, child) {}
```

