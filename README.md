[TOC]



# SobotKit

Sobot sdk for ios 
========
智齿客服
========

=============   智齿SDK文档地址  =============

1.智齿集成文档地址： https://shimo.im/docs/HyQ9crCXWqQxtXKg   

2.智齿 iOS_SDK UI源码 Git下载地址：https://github.com/ZCSDK/sobotKit_UI_iOS  

3.智齿 iOS_SDK 常见问题解答 下载地址：https://github.com/ZCSDK/FAQ_iOS        

=============================================


==============  版本更新说明  =============
### SDK 2.7.12 版本更新说明
1、【优化】转人工过程不支持发送消息，解决人工聊天时偶发出现机器人消息问题    

2、【新增】直接跳转到留言页面方法   
+(void)openLeanve:(int ) showRecored with:(UIViewController *)byController onItemClick:(void (^)(NSString *msg,int code))CloseBlock;



### SDK 2.7.11 版本更新说明
1、【优化】使用WKWebView替换UIWebView，需要兼容iOS 8.0以前版本客户请联系售后
2、【优化】兼容iOS 13推送
3、【优化】解决@available方法引起的编译问题
4、【优化】仅人工模式不能与机器人发消息


### SDK 2.7.10 版本更新说明

1、解决webview查看txt乱码问题，优先使用UTF-8编码解析

2、解决iOS 13 使用presentViewController方式启动不兼容问题，添加.modalPresentationStyle = UIModalPresentationOverFullScreen;

3、补全国际化标签

4、商品标签颜色自定义

### SDK 2.7.9 版本更新说明

【增加】工单回复富文本优化

【增加】图片增加二维码识别

【增加】会话锁定功能



### SDK 2.7.8 版本更新说明

【增加】人工自定义功能和机器人自定义功能拆分

```
/**
 * 自定义输入框下方更多(+号图标)按钮下面内容(不会替换原有内容，会在原有基础上追加)
 * 修改机器人模式的按钮
 * 填充内容为：ZCLibCusMenu.h
 *  title:按钮名称
 *  url：点击链接(点击后会调用初始化linkBock)
 *  imgName:本地图片名称，如xxx@2x.png,icon=xxx
 */
@property (nonatomic,strong) NSMutableArray * cusRobotMoreArray;
```

【增加】新增多轮问题答案支持富文本形式展示

【修复】文本过长显示问题

【修复】iPhone X 版本 输入表情过多显示问题

【增加】点击拍摄按钮，弹出权限按钮，不同意授权后提示去授权

【增加】增加控制关闭按钮弹出评价的开关字段

```
/**
 *
 *   针对关闭按钮，单独设置是否显示评价界面，默认不显示
 *
 **/
@property (nonatomic,assign) BOOL isShowCloseSatisfaction;
```

【修复】ipad横屏显示通知小喇叭显示问题

【增加】留言转离线消息时“+”号内显示评价按钮

【修复】ipad版发送视频正在压缩时点击返回按钮闪退问题

### SDK 2.7.7 版本更新说明

1【新增】右上角评价按钮

### SDK 2.7.6 版本更新说明

1 [新增]  新增人工咨询页面结束会话按钮   
2 [新增]  消息卡片消息类型开放    
3 [新增]  转人工支持传入服务总结自定义字段 



###SDK 2.7.5 版本更新说明

1 [新增]  自定义转人工事件   
2 [新增]  商品卡片消息类型    
3 [新增]  服务总结自定义字段支持传参   
4 [新增]  多轮会话中自定义字段“multi-Params”   
5 [优化]  标签链接UI优化   
6 [优化]  支持富文本形式展现知识库词条文本内容  
7 [优化]  机器人设置-机器人引导问题展示--增加“换一组”功能   
8 [优化]  输入框遮挡聊天气泡  


```
自定义转人工事件 
如果实现该方法，SDK中转人工事件将交由外部控制处理，您可以跳转到自己设计的技能组页面，或者切换商品信息等，最后调取 -(void)turnServiceWithGroupId:(NSString *)groupId  Obj:(id)obj Msg:(NSString*)msg KitInfo:(ZCKitInfo*)uiInfo ZCTurnType:(NSInteger)turnType Keyword:(NSString*)keyword KeywordId:(NSString*)keywordId;方法去执行转人工操作。

/**
* 自定义转人工回调事件
* 拦截SDK 转人工事件 用于跳转到自己的app页面动态处理转人工 配置技能组id 商品信息等参数
***/
@property (nonatomic,strong)  TurnServiceBlock    turnServiceBlock;

/**
*  自定义 转人工事件（在turnServiceBlock回调事件中调用）
*   groupId 传入技能组id
*   obj   转人工参数
msg   转人工信息
uiInfo   配置商品信息和自动发送参数
turnType  转人工事件类型（按钮触发，关键字触发等）
Keyword 关键字
keywordId 关键字id
**/
-(void)turnServiceWithGroupId:(NSString *)groupId  Obj:(id)obj Msg:(NSString*)msg KitInfo:(id)uiInfo ZCTurnType:(NSInteger)turnType Keyword:(NSString*)keyword KeywordId:(NSString*)keywordId;


示例代码：

[ZCLibClient getZCLibClient].turnServiceBlock = ^(id obj,NSString *msg,NSInteger turnType, NSString *keyword ,NSString *keywordId) {

ZCProductInfo *productInfo = [ZCProductInfo new];
productInfo.thumbUrl = @"商品图片URL";
productInfo.title = @"商品标题";
productInfo.desc = @"摘要";
productInfo.label = @"标签";
productInfo.link = @"http://www.sobot.com";
uiInfo.productInfo = productInfo;
uiInfo.isSendInfoCard = YES;// 转人工工成功后是否自动发送该商品卡片信息

[[ZCLibClient getZCLibClient] turnServiceWithGroupId:@"技能组id" Obj:obj Msg:msg KitInfo:uiInfo ZCTurnType:turnType Keyword:keyword KeywordId:keywordId];
};

```



###SDK 2.7.4 版本更新说明
1 [新增]  通告设置拓展  
2 [新增]  留言转离线消息及回复功能    
3 [新增]  帮助中心   
4 [新增]  支持“指定客户优先”设置   
5 [新增]  工单满意度   
6 [新增]  发送订单信息功能   
7 [优化]  清空聊天记录新增二次确认浮层  
8 [新增]  查看对应商户客服是否正在和用户聊天API（仅电商版使用）


```
/**
 *
 *  启动 客户帮助中心
 *
 *  @param info         初始化参数，详情见ZCLibInitInfo not null
 *  @param byController 当前执行跳转的VC           not null
 *  @param delegate     ZCUIChatDelagete        聊天页面的代理，如果实现这个代理用户可以实现留言跳转到自定义页面
 *  @param pageClick    点击返回，UI修改, object为ZCChatController（使用系统导航栏场景） 或者 ZCChatView（使用SDK自定义导航栏场景） 
 *  @param linkBlock    点击消息链接回调，可以为null(注意：如果传递实现后内部将直接返回url，不在做跳转处理)
 *
 */
+(void)openZCServiceCentreVC:(ZCKitInfo *) info
                with:(UIViewController *) byController
                 onItemClick:(void (^)(ZCUIBaseController *object,ZCOpenType type))itemClickBlock;

```



```
发送订单信息
1.配置按钮
ZCKitInfo *uiInfo=[ZCKitInfo new];
NSMutableArray *arr = [[NSMutableArray alloc] init];

        ZCLibCusMenu *menu1 = [[ZCLibCusMenu alloc] init];
        menu1.title = [NSString stringWithFormat:@"订单"];
        menu1.url = [NSString stringWithFormat:@"sobot://sendOrderMsg"];;
        menu1.imgName = @"zcicon_sendpictures";
        [arr addObject:menu1];
        
    uiInfo.cusMoreArray = arr;
    
2.实现发送事件
[ZCSobot startZCChatVC:uiInfo with:self target:nil pageBlock:^(id object, ZCPageBlockType type) {
        
    } messageLinkClick:^BOOL(NSString *link) {
        if( [link hasPrefix:@"sobot://sendOrderMsg"]){
            // 发送位置信息
             [ZCSobot sendeOrderMsg:@"订单号：123456789012\n商品1：恰恰瓜子200g*1\n商品链接：www.baidu.com\n商品描述：恰恰瓜子恰恰瓜子恰恰瓜子\n恰恰瓜子恰恰瓜子恰恰瓜子恰恰瓜子...\n商品2：农夫山泉500ml*12\n商品链接：www.sina.com\n商品描述:农夫山泉农夫山泉农夫山泉\n农夫山泉农夫山泉农夫山泉农夫山泉..."];          
               return YES;
        }
       return NO;
    }];

```


```

/**
 *
 *   获取对应商户客服是否正在和用户聊天（仅电商版使用）
 *   appkey：商户id   uid： ZCPlatformInfo 类中的uid 
 **/
+(BOOL)getPlatformIsArtificialWithAppkey:(NSString *)appkey Uid:(NSString*)uid;

-(void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath{
 ZCPlatformInfo *info = [_listArray objectAtIndex:indexPath.row];
[ZCSobot getPlatformIsArtificialWithAppkey:info.appkey Uid:info.uid];
}
```



###SDK 2.7.2 版本更新说明

1 [新增]  留言模板      
2 [新增]  留言工单客户可在原渠道查看工单回复    
3 [新增]  咨询页面新增自定义按钮（评价、呼叫）   
4 [新增]  转人工溢出功能  
5 [优化]  机器人转人工业务逻辑



```
2.7.2新增初始化方法
/**
 初始化智齿客服 2.7.2开始使用
 
 @param appkey 智齿appkey(如果是电商版本，请填写自己公司的APPKEY)
 @param resultBlock 初始化结果回调
 */
-(void)initSobotSDK:(NSString *) appkey result:(void (^)(id object))resultBlock;

原方法： -(void)initSobotSDK:(NSString *) appkey;  可以继续使用
```



###SDK 2.7.0 版本更新说明

1 [新增] 推送消息支持来源  
2 [新增] 本地消息格式优化  
3 [新增] 发送地理位置   
4 [新增] 拍摄和发送小视频   

###SDK 2.6.9 版本更新说明

1 [新增] 发送文件


###SDK 2.6.7 版本更新说明

1 [新增] 机器人切换业务时切换欢迎语

2 [新增] 商家删除指定商户接口(仅电商版使用)

3 [新增] 清空用户下的所有未读消息(本地清空)



###SDK 2.6.6 版本更新说明

1 [新增]iPhone 新机型适配

2 [新增]增加商户对接id(仅电商版使用)

3 初始化方法中 pageBlock 中原 ZCChatController *object 替换为 id object 

```
[ZCSobot startZCChatVC:uiInfo with:self target:nil pageBlock:^(id object, ZCPageBlockType type) {
                // 点击返回
                if(type==ZCPageBlockGoBack){
//                    NSLog(@"点击了关闭按钮");
                }
                // 页面UI初始化完成，可以获取UIView，自定义UI
                if(type==ZCPageBlockLoadFinish){
//                    NSLog(@"页面加载完成");
                }
    } messageLinkClick:nil];
```



###SDK 2.6.5 版本更新说明

1 聊天页导航栏新增评级入口（可选）

2 机器人顶踩UI优化

3 新增获取商家信息列表功能（仅电商版使用）


###SDK 2.6.4 版本更新说明

1[新增] 自定义发送消息功能

2[新增] 自定义排队说辞



###SDK 2.6.3 版本更新说明

1[新增] UI自定义属性
>更多按钮默认图片  
>更多按钮选中图片  
>转人工按钮默认图片  
>转人工按选中图片  
>返回按钮默认图片  
>返回按钮选中图片  
>返回按钮的默认背景色  
>返回按钮的高亮背景色  
>导航栏背景色 
>自定义输入框下方更多(+号图标)按钮下面内容cusMoreArray 

2[新增] 智能路由逻辑处理

3[修改] 方法变更

```  

原： -(void)initZCIMCaht ；方法弃用
原：+(void)closeZCServer:(BOOL)isClosePush; 方法弃用
原：-(void)aginitIMChat; 方法弃用

新增：
/**
 @note 检查当前消息通道是否建立，没有就重新建立
 如果调用 closeIMConnection 后，可调用此方法重新建立链接
 */
-(void)checkIMConnected;

/**
 @note 关闭当前消息通道，使其不再接受消息
 */
-(void)closeIMConnection;


/**
 移除IM所有监听，可能会影响应用在后台存活时长，如果调用此方法后需要checkIMObserverWithCreate重新激活
 网络监听 ZCNotification_NetworkChange
 UIApplicationDidBecomeActiveNotification
 UIApplicationDidEnterBackgroundNotification
 */
-(void)removeIMAllObserver;

/**
 检查当前监听是否被移除，如果移除就重新注册
 */
-(void)checkIMObserverWithRegister;

```


###SDK 2.6.2 版本更新说明

1、修改bug


###SDK 2.6.1 版本更新说明

1、【新增】关键字提醒功能   
2、【新增】关键字转人工功能     
3、【新增】机器人多轮会话模板  



###SDK 2.6.0 版本更新说明

1、【新增】机器人切换业务功能   
2、【新增】快捷入口功能   
3、【新增】客服消息撤回提示  
4、【优化】表情资源文件和语言文件文件路基结构   

注：
> 1.原ZCEmojiExpression.bundle 表情资源包不在需要导入到项目中，现放到 SobotKit.bundle包中的emoji文件中。   
> 2.原SobotLocalizable.strings 语言文件现放在SobotKit.bundle中。  
> 3.手动集成SDK 需要导入到项目中的文件 SobotKit.framework 和SobotKit.bundle 。


###SDK 2.5.5 版本更新说明

1、【新增】获取用户app名称和版本号 获取用户手机型号  
2、【优化】技能组选择弹框页面（多个技能组展示）   
3、【新增】通告跑马灯效果   
4、【优化】SDK启动方法 新启动方法如下：
```  
+(void)startZCChatVC:(ZCKitInfo *) info
                with:(UIViewController *) byController
              target:(id<ZCChatControllerDelegate>) delegate
           pageBlock:(void (^)(ZCChatController *object,ZCPageBlockType type))pageClick
    messageLinkClick:(void (^)(NSString *link)) messagelinkBlock;
```

###SDK 2.5.3 版本更新说明

1、外抛自定义导航栏ZCTopView;

###SDK 2.5.2 版本更新说明

1、多轮会话中模板二和模板三增加分页;  

###SDK 2.5.0 版本更新说明

1、代码重构，新增ZCChatView.h，可自定义页面大小;  
2、ZCUIChatController更名为ZCChatController，原ZCUIChatController将不再维护;  
3、新增自适应系统导航逻辑，不在对系统导航单独隐藏;  
4、优化初始化方法，启动之前新增初始化方法  
-(void)initSobotSDK:(NSString *)appkey;

###SDK 2.4.3 版本更新说明

1、增加机器人分词联想（自动补全）功能


###SDK 2.4.2 版本更新说明

1、增加机器人热点引导问题功能

###SDK 2.4.1 版本更新说明

1、增加机器人多轮会话功能

###SDK 2.4.0 版本更新说明

1、智能转人工

###SDK 2.3.3 版本更新说明

1、优化图片加载方式   
2、适配iOS 11 UI 
3、优化代码，解决获取异常信息可能引起异常冲突文件

###SDK 2.3.2 版本更新说明

1、新增机器人语音翻译功能   
2、留言增加自定义字段设置


###SDK 2.3.0版本更新说明

1、支持人工客服满意度自定义设置   
2、满意度评价页交互优化   
3、通告置顶   
4、自动转留言设置   
5、初始化对接字段调整为后台自定义字段  
6、支持设置转留言到客户自定义的页面   
7、自动应答可设置开关  

###SDK 2.2.2版本更新说明

1、优化网络监听管理类 


###SDK 2.2.1版本更新说明

1、通告自定义  
2、自动应答(说辞)自定义    
3、用户排队达到阀值可以自动跳转到留言页   
4、优化消息通道稳定性
5、新增可配置的自定义参数



###SDK 2.2.0版本更新说明

1、 SDK支持设置【机器人引导转人工】  
2、 评价机器人推送 （顶、踩）  
3、 支持客户自己配置用户提交完成人工满意度评价后释放会话   
4、 留言支持添加图片  



详情[<https://docs.sobot.com/kai-fa-zhe-wen-dang/duo-qu-dao-jie-ru/ios-sdk-jie-ru.html>]  






