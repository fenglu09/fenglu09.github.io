---
title: React-native采坑
date: 2018-07-01 14:59:45
tags:
- React-native
---
<font face='Menlo'>

1. 键盘遮挡问题: 使用插件`react-native-keyboard-aware-scroll-view`

2. Android端`border dashed/dotted` 不起作用，解决办法：设置`borderRadius`,设置后起作用。

3. iOS中，设置横屏后，只要显示Modal就报错和闪退。

```
Exception thrown while executing UI block: Supported orientations has no common orientation with the         
application, and [RCTModalHostViewController shouldAutorotate] is returning YES
```
原因：Modal支持的屏幕方向中没有横屏。
解决办法：在Modal上添加 `supportedOrientations` 属性即可。
`supportedOrientations={['portrait', 'landscape', 'landscape-left', 'landscape-right']}`

4. 在自己写Native组件的时候，iOS引入进去后，会报错`library not found for xxx.a`的错误。

解决：

    1. 检查模块有没有导入

    2. 检查`build phases`中，是否有引入包，

    3. 如果使用了pod，删除`Podfile`, `Pods`, `Podfile.lock`,  然后重新运行`pod install `。



5. `TextInput`在Android的上面默认有一个underline，设置为`underlineColorAndroid="transparent"`。但是设置高度后，会出现如下的效果。
![](./img/41668601.png)

给`TextInput`设置`paddingVertical: 0`后，可解决
![](./img/41691255.png)


6. 自己写的组件,iOS 中debug build没问题，archive的时候就报错，找不到lib

![](./img/58757502.png)

   解决办法，在找不到的那个静态库中，`build settings` 中的`target device family`改成`1`，默认是`1,2`，将`iOS deployment target` 改成9就好了
![](./img/58856031.png)

7. iOS真机运行编译失败
```
Undefined symbols for architecture arm64:
"_RCTSetLogFunction", referenced from:
-[PropertyFinderTests testRendersWelcomeScreen] in PropertyFinderTests.o
```
解决办法: 选择`TargetNameTest`， `Build Phases`-> `Link Binary With Libraries` 在添加`libReact.a`即可

</font>