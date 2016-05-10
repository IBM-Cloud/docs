# 为 iOS 应用程序初始化推送 SDK
{: #enable-push-ios-notifications-install}

对于现有 Xcode 项目，可以使用 CocoaPods 依赖关系管理工具来设置 Bluemix Mobile Services 客户机 SDK。替代方法是手动安装该 SDK。

**注**：要查看 Swift Push 自述文件，请转至 https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master

##安装 CocoaPods

1. 在 Mac 终端中，使用以下命令安装 CocoaPods：
```
$ sudo gem install cocoapods
```
2. 在终端中输入以下命令来初始化 CocoaPods。发出此命令时，确保此命令是在 Xcode 项目所在目录中运行。`pod init` 命令会创建文件标题。
```
$ pod init
```
3. 在生成的 Podfile 中，添加所需的 SDK 依赖关系。复制以下 Podfile。

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. 在终端中，转至项目文件夹，然后使用以下命令安装依赖关系：
```
$ pod update
```
该命令会安装依赖关系并创建新的 Xcode 工作空间。**注**：确保始终打开新的 Xcode 工作空间，而不是原始 Xcode 项目文件：

	```
	$ open App.xcworkspace
	```
该工作空间包含原始项目，以及包含依赖关系的 Pods 项目。如果要修改 Bluemix Mobile Services 源文件夹，那么可以在 Pods 项目的 `Pods/yourImportedSourceFolder` 下找到该文件夹，例如：`Pods/IMFGoogleAuthentication`。

##使用导入的框架和源文件夹

在代码中引用 SDK。


### Objective-C

针对相关头编写 #import 伪指令，例如：

```
//Objective-C

#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**注**：使用 CocoaPods 命令 `pod install` 或 `pod update` 更新 Pods 项目可能会覆盖 Bluemix Mobile Services 源文件夹。如果要保留原始文件的定制版本，请确保在发出其中某个命令之前已备份这些文件。

###Swift

**先决条件**

- iOS 8.0 或更高版本
- Xcode 7


针对相关头编写 #import 伪指令，例如：

```
//swift
import BMSCore
import BMSPush
```


##构建设置

转至 **Xcode > 构建设置 > 构建选项**，然后将**启用位代码**设置为**否**。

**注意**：自 iOS 9 起，对应用程序传输安全性 (ATS) 功能的更改可能会影响您处理认证过程的方式。以下博客帖子描述了有关这些更改的更多信息：[ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) 和 [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)
