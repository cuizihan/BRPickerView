# 框架介绍
BRPickerView是iOS的选择器组件，主要包括：日期选择器、时间选择器、地址选择器、自定义字符串选择器。

【特别提示】：

- 当前最新版本为： `2.0.0` 。
- 如果不能找到最新版本，请先执行一下 `pod setup` ，待更新完成后；再执行 `pod search BRPickerView` 进行搜索，就会看到最新版本。

#### 更新记录

- 2018-01-24（V2.0.0）：

  >1. 更新了地址数据源（BRCity.plist），地区信息是2018年最新最全的，与微信的地区信息完全一致。
  >2. 支持自定义默认选择地址（格式：@[@"浙江省", @"杭州市", @"西湖区"]），支持下次点击进入地址选择器时，默认地址为上次选择的结果。
  >3. 修改了日期选择器、地址选择器、字符串选择器的接口方法（删除了之前的方法2）。
  >4. 添加了地址选择器显示类型，支持3种显示：只显示省份、显示省份和城市、显示省市区。



- 2018-01-05（V1.3.0）:

  >1. 添加取消选择的回调方法（点击背景或取消按钮会执行 `cancelBlock` ）
  >2. 合并了字符串选择器 数组数据源和plist数据源对应的方法，`dataSource` 参数支持两种类型：
  >   - 1> 可以直接传数组：NSArray类型；
  >   - 2> 可以传plist文件名：NSString类型，带后缀名，plist文件的内容必须是数组格式。


- 2018-01-02（V1.2.0）：

  >添加支持自定义主题颜色的方法

- 2017-11-26（V1.1.0）：

  >替换了第三方依赖库，用MJExtension 替换了 原来的YYModel，以前没有注意导入YYModel，同时又导入YYKit会导致重复导入而冲突（另外使用YYModel时，手动导入和pod导入 其中的头文件和方法名也不一样，所以很容易出错），推荐使用1.1.0版本！！！


- 2017-11-16（V1.0.0）：

  >初始版本。

# 效果演示

查看并运行 `BRPickerViewDemo.xcodeproj`

| ![Demo运行效果图](https://github.com/borenfocus/BRPickerView/blob/ace50fb90d32e80a3a94116a925c631e13c6f4cc/BRPickerViewDemo/%E6%95%88%E6%9E%9C%E5%9B%BE/%E6%95%88%E6%9E%9C%E5%9B%BE.gif?raw=true) |
| :--------------------------------------: |
|               框架Demo运行效果图                |

# 安装

#### CocoaPods

1. 在 Podfile 中添加 `pod 'BRPickerView', '~> 2.0.0'`。

2. 执行 `pod install` 或 `pod update` 。

   推荐使用：`pod update --verbose --no-repo-update`  (安装速度快一点)

3. 导入头文件 ` #import <BRPickerView.h>`。

   >注意：
   >
   >​	先搜索框架：pod search BRPickerView （最新版本号为2.0.0）
   >
   >​	如果无法搜索到框架（或没有显示最新版本），执行下面操作：
   >
   >​		1》pod setup
   >
   >​		2》rm ~/Library/Caches/CocoaPods/search_index.json
   >
   >​		3》pod search BRPickerView
   >
   >导入指定版本的框架：pod 'BRPickerView', '~> 2.0.0'

#### 手动导入

1. 将与 `README.md` 同级目录下的 `BRPickerView` 文件夹拽入项目中

2. 导入头文件 ` #import "BRPickerView.h"`。

   > 注意：
   >
   > 本框架依赖第三方MJExtension，所以手动导入框架时，还需要导入MJExtension框架。

# 系统要求

- iOS 8.0+
- ARC

# 使用

#### 1. 时间选择器：`BRDatePickerView`

​	查看 BRDatePickerView.h 头文件，里面提供了3个方法，可根据自己的需求选择其中的一个方法进行使用。

```objective-c
/**
 *  1.显示时间选择器
 *
 *  @param title            标题
 *  @param type             类型（枚举类型：UIDatePickerModeTime、UIDatePickerModeDate、UIDatePickerModeDateAndTime、UIDatePickerModeCountDownTimer）
 *  @param defaultSelValue  默认选中的时间（为空，默认选中现在的时间）
 *  @param resultBlock      选择结果的回调
 *
 */
+ (void)showDatePickerWithTitle:(NSString *)title
                       dateType:(UIDatePickerMode)type
                defaultSelValue:(NSString *)defaultSelValue
                    resultBlock:(BRDateResultBlock)resultBlock;

/**
 *  2.显示时间选择器（支持 设置自动选择 和 自定义主题颜色）
 *
 *  @param title            标题
 *  @param type             类型（枚举类型：UIDatePickerModeTime、UIDatePickerModeDate、UIDatePickerModeDateAndTime、UIDatePickerModeCountDownTimer）
 *  @param defaultSelValue  默认选中的时间（为空，默认选中现在的时间）
 *  @param minDateStr       最小时间（如：2015-08-28 00:00:00），可为空
 *  @param maxDateStr       最大时间（如：2018-05-05 00:00:00），可为空
 *  @param isAutoSelect     是否自动选择，即选择完(滚动完)执行结果回调，传选择的结果值
 *  @param themeColor       自定义主题颜色
 *  @param resultBlock      选择结果的回调
 *
 */
+ (void)showDatePickerWithTitle:(NSString *)title
                       dateType:(UIDatePickerMode)type
                defaultSelValue:(NSString *)defaultSelValue
                     minDateStr:(NSString *)minDateStr
                     maxDateStr:(NSString *)maxDateStr
                   isAutoSelect:(BOOL)isAutoSelect
                     themeColor:(UIColor *)themeColor
                    resultBlock:(BRDateResultBlock)resultBlock;

/**
 *  3.显示时间选择器（支持 设置自动选择、自定义主题颜色、取消选择的回调）
 *
 *  @param title            标题
 *  @param type             类型（枚举类型：UIDatePickerModeTime、UIDatePickerModeDate、UIDatePickerModeDateAndTime、UIDatePickerModeCountDownTimer）
 *  @param defaultSelValue  默认选中的时间（为空，默认选中现在的时间）
 *  @param minDateStr       最小时间（如：2015-08-28 00:00:00），可为空
 *  @param maxDateStr       最大时间（如：2018-05-05 00:00:00），可为空
 *  @param isAutoSelect     是否自动选择，即选择完(滚动完)执行结果回调，传选择的结果值
 *  @param themeColor       自定义主题颜色
 *  @param resultBlock      选择结果的回调
 *  @param cancelBlock      取消选择的回调
 *
 */
+ (void)showDatePickerWithTitle:(NSString *)title
                       dateType:(UIDatePickerMode)type
                defaultSelValue:(NSString *)defaultSelValue
                     minDateStr:(NSString *)minDateStr
                     maxDateStr:(NSString *)maxDateStr
                   isAutoSelect:(BOOL)isAutoSelect
                     themeColor:(UIColor *)themeColor
                    resultBlock:(BRDateResultBlock)resultBlock
                    cancelBlock:(BRDateCancelBlock)cancelBlock;
```

- 日期选择器的四种类型（dateType的4个枚举值）：

| ![样式1：UIDatePickerModeTime](https://github.com/borenfocus/BRPickerView/blob/0e4519a28bd0ce462b9e2c15d63834645228a605/BRPickerViewDemo/%E6%95%88%E6%9E%9C%E5%9B%BE/date_type1.png?raw=true) | ![样式2：UIDatePickerModeDate](https://github.com/borenfocus/BRPickerView/blob/0e4519a28bd0ce462b9e2c15d63834645228a605/BRPickerViewDemo/%E6%95%88%E6%9E%9C%E5%9B%BE/date_type2.png?raw=true) |
| :--------------------------------------: | :--------------------------------------: |
|         样式1：UIDatePickerModeTime         |         样式2：UIDatePickerModeDate         |
|                                          |                                          |
| ![样式3：UIDatePickerModeDateAndTime](https://github.com/borenfocus/BRPickerView/blob/0e4519a28bd0ce462b9e2c15d63834645228a605/BRPickerViewDemo/%E6%95%88%E6%9E%9C%E5%9B%BE/date_type3.png?raw=true) | ![样式4：UIDatePickerModeCountDownTimer](https://github.com/borenfocus/BRPickerView/blob/0e4519a28bd0ce462b9e2c15d63834645228a605/BRPickerViewDemo/%E6%95%88%E6%9E%9C%E5%9B%BE/date_type4.png?raw=true) |
|     样式3：UIDatePickerModeDateAndTime      |    样式4：UIDatePickerModeCountDownTimer    |



#### 2. 地址选择器：`BRAddressPickerView`

​	查看 BRAddressPickerView.h 头文件，里面提供了3个方法，可根据自己的需求选择其中的一个方法进行使用。

```objective-c
/**
 *  1.显示地址选择器
 *
 *  @param defaultSelectedArr       默认选中的值(传数组，如：@[@"浙江省", @"杭州市", @"西湖区"])
 *  @param resultBlock              选择后的回调
 *
 */
+ (void)showAddressPickerWithDefaultSelected:(NSArray *)defaultSelectedArr
                                 resultBlock:(BRAddressResultBlock)resultBlock;

/**
 *  2.显示地址选择器（支持 设置自动选择 和 自定义主题颜色）
 *
 *  @param defaultSelectedArr       默认选中的值(传数组，如：@[@"浙江省", @"杭州市", @"西湖区"])
 *  @param isAutoSelect             是否自动选择，即选择完(滚动完)执行结果回调，传选择的结果值
 *  @param themeColor               自定义主题颜色
 *  @param resultBlock              选择后的回调
 *
 */
+ (void)showAddressPickerWithDefaultSelected:(NSArray *)defaultSelectedArr
                                isAutoSelect:(BOOL)isAutoSelect
                                  themeColor:(UIColor *)themeColor
                                 resultBlock:(BRAddressResultBlock)resultBlock;

/**
 *  3.显示地址选择器（支持 设置选择器类型、设置自动选择、自定义主题颜色、取消选择的回调）
 *
 *  @param showType                 地址选择器显示类型
 *  @param defaultSelectedArr       默认选中的值(传数组，如：@[@"浙江省", @"杭州市", @"西湖区"])
 *  @param isAutoSelect             是否自动选择，即选择完(滚动完)执行结果回调，传选择的结果值
 *  @param themeColor               自定义主题颜色
 *  @param resultBlock              选择后的回调
 *  @param cancelBlock              取消选择的回调
 *
 */
+ (void)showAddressPickerWithShowType:(BRAddressPickerMode)showType
                      defaultSelected:(NSArray *)defaultSelectedArr
                         isAutoSelect:(BOOL)isAutoSelect
                           themeColor:(UIColor *)themeColor
                          resultBlock:(BRAddressResultBlock)resultBlock
                          cancelBlock:(BRAddressCancelBlock)cancelBlock;
```

方法使用：

```objective-c
// 【转换】：以@" "子字符串为基准将字符串分离成数组，如：@"浙江省 杭州市 西湖区" ——》@[@"浙江省", @"杭州市", @"西湖区"]
NSArray *defaultSelArr = [weakSelf.addressTF.text componentsSeparatedByString:@" "];
[BRAddressPickerView showAddressPickerWithShowType:BRAddressPickerModeArea defaultSelected:defaultSelArr isAutoSelect:YES themeColor:nil resultBlock:^(NSArray *selectAddressArr) {
    weakSelf.addressTF.text = [NSString stringWithFormat:@"%@ %@ %@", selectAddressArr[0], selectAddressArr[1], selectAddressArr[2]];
} cancelBlock:^{
    NSLog(@"点击了背景视图或取消按钮");
}];
```

效果图（3种样式）：

| ![省份](https://github.com/borenfocus/BRPickerView/blob/d400c274ff270ac4c805ac8b33f9ea3988e927e4/BRPickerViewDemo/%E6%95%88%E6%9E%9C%E5%9B%BE/BRAddressPickerModeProvince.png?raw=true) | ![城市](https://github.com/borenfocus/BRPickerView/blob/d400c274ff270ac4c805ac8b33f9ea3988e927e4/BRPickerViewDemo/%E6%95%88%E6%9E%9C%E5%9B%BE/BRAddressPickerModeCity.png?raw=true) | ![地区](https://github.com/borenfocus/BRPickerView/blob/d400c274ff270ac4c805ac8b33f9ea3988e927e4/BRPickerViewDemo/%E6%95%88%E6%9E%9C%E5%9B%BE/BRAddressPickerModeArea.png?raw=true) |
| :--------------------------------------: | :--------------------------------------: | :--------------------------------------: |
|       BRAddressPickerModeProvince        |         BRAddressPickerModeCity          |         BRAddressPickerModeArea          |

#### 3.  自定义字符串选择器：`BRStringPickerView`

​	查看 BRStringPickerView.h 头文件，里面提供了6个方法，可根据自己的需求选择其中的一个方法进行使用。

```objective-c
/**
 *  1.显示自定义字符串选择器
 *
 *  @param title            标题
 *  @param dataSource       数据源（1.直接传数组：NSArray类型；2.可以传plist文件名：NSString类型，带后缀名，plist文件内容要是数组格式）
 *  @param defaultSelValue  默认选中的行(单列传字符串，多列传一维数组)
 *  @param resultBlock      选择后的回调
 *
 */
+ (void)showStringPickerWithTitle:(NSString *)title
                       dataSource:(id)dataSource
                  defaultSelValue:(id)defaultSelValue
                      resultBlock:(BRStringResultBlock)resultBlock;

/**
 *  2.显示自定义字符串选择器（支持 设置自动选择 和 自定义主题颜色）
 *
 *  @param title            标题
 *  @param dataSource       数据源（1.直接传数组：NSArray类型；2.可以传plist文件名：NSString类型，带后缀名，plist文件内容要是数组格式）
 *  @param defaultSelValue  默认选中的行(单列传字符串，多列传一维数组)
 *  @param isAutoSelect     是否自动选择，即选择完(滚动完)执行结果回调，传选择的结果值
 *  @param themeColor       自定义主题颜色
 *  @param resultBlock      选择后的回调
 *
 */
+ (void)showStringPickerWithTitle:(NSString *)title
                       dataSource:(id)dataSource
                  defaultSelValue:(id)defaultSelValue
                     isAutoSelect:(BOOL)isAutoSelect
                       themeColor:(UIColor *)themeColor
                      resultBlock:(BRStringResultBlock)resultBlock;

/**
 *  3.显示自定义字符串选择器（支持 设置自动选择、自定义主题颜色、取消选择的回调）
 *
 *  @param title            标题
 *  @param dataSource       数据源（1.直接传数组：NSArray类型；2.可以传plist文件名：NSString类型，带后缀名，plist文件内容要是数组格式）
 *  @param defaultSelValue  默认选中的行(单列传字符串，多列传一维数组)
 *  @param isAutoSelect     是否自动选择，即选择完(滚动完)执行结果回调，传选择的结果值
 *  @param themeColor       自定义主题颜色
 *  @param resultBlock      选择后的回调
 *  @param cancelBlock      取消选择的回调
 *
 */
+ (void)showStringPickerWithTitle:(NSString *)title
                       dataSource:(id)dataSource
                  defaultSelValue:(id)defaultSelValue
                     isAutoSelect:(BOOL)isAutoSelect
                       themeColor:(UIColor *)themeColor
                      resultBlock:(BRStringResultBlock)resultBlock
                      cancelBlock:(BRStringCancelBlock)cancelBlock;
```

方法使用：

```objective-c
// 自定义单列字符串
NSArray *dataSources = @[@"大专以下", @"大专", @"本科", @"硕士", @"博士", @"博士后"];
[BRStringPickerView showStringPickerWithTitle:@"学历" dataSource:dataSources defaultSelValue:@"本科" isAutoSelect:YES themeColor:nil resultBlock:^(id selectValue) {
    weakSelf.educationTF.text = selectValue;
} cancelBlock:^{
    NSLog(@"点击了背景视图或取消按钮");
}];
// 自定义多列字符串
NSArray *dataSources = @[@[@"第1周", @"第2周", @"第3周", @"第4周", @"第5周", @"第6周", @"第7周"], @[@"第1天", @"第2天", @"第3天", @"第4天", @"第5天", @"第6天", @"第7天"]];
[BRStringPickerView showStringPickerWithTitle:@"自定义多列字符串" dataSource:dataSources defaultSelValue:@[@"第3周", @"第3天"] isAutoSelect:YES themeColor:RGB_HEX(0xff7998, 1.0f) resultBlock:^(id selectValue) {
    weakSelf.otherTF.text = [NSString stringWithFormat:@"%@，%@", selectValue[0], selectValue[1]];
} cancelBlock:^{
    NSLog(@"点击了背景视图或取消按钮");
}];
```

效果图：

| ![自定义单列字符串](https://github.com/borenfocus/BRPickerView/blob/d400c274ff270ac4c805ac8b33f9ea3988e927e4/BRPickerViewDemo/%E6%95%88%E6%9E%9C%E5%9B%BE/string_single.png?raw=true) | ![自定义多列字符串](https://github.com/borenfocus/BRPickerView/blob/d400c274ff270ac4c805ac8b33f9ea3988e927e4/BRPickerViewDemo/%E6%95%88%E6%9E%9C%E5%9B%BE/string_more.png?raw=true) |
| :--------------------------------------: | :--------------------------------------: |
|                 自定义单列字符串                 |                 自定义多列字符串                 |

# 许可证

BRPickerView 使用 MIT 许可证，详情见 LICENSE 文件。