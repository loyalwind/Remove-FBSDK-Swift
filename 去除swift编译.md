# FBSDK 去除swift模块的编译方法

### 简单介绍

下载指定版本源码 Source code(zip)  https://github.com/facebook/facebook-ios-sdk/tags

- 打开FacebookSDK.xcworkspace 项目

  ` FBSDKCoreKit、FBSDKLoginKit、FBSDKShareKit 分别做如下操作 `

  + 删除swift相关：移除编译swift代码，bridge-swift 头文件， FBSDK*.modulemap等配置

  + General -- Deloyment Info 中取消勾选 Mac

  + Build Settings -- Excluded Architectures -- Release 选择 Any iOS Simulator SDK 值填写（arm64）; 意思是编译任意模拟器SDK时不包含 arm64模拟器架构

  + Edit Scheme --  Run -- 改成Release

    

- 分别编译 FBSDKLoginKit、FBSDKShareKit 的 真机、模拟器架构SDK

- 使用`lipo`命令进行架构合并 ` FBSDKCoreKit、FBSDKLoginKit、FBSDKShareKit`

  ```sh
  lipo -create 模拟器静态库路径1 真机静态库路径2 -output 存放路径
  ```

  

