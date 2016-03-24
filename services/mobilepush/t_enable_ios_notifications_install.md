# Initializing Push SDK for iOS apps
{: #enable-push-ios-notifications-install}

For an existing Xcode project, you can set up the Bluemix Mobile Services Client SDK using the CocoaPods dependency management tool. An alternative is to install the SDK manually.

**Note**: To view the Swift Push readme file, go https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master

##Installing CocoaPods

1. Install CocoaPods by using the following command in your Mac terminal.
```
$ sudo gem install cocoapods
```
2. Enter the following command in the terminal to initilalize CocoaPods. When you issue this command, make sure the run it in the directory where your Xcode project is. The `pod init`command creates a file title.  
```
$ pod init
```
3. In the generated Podfile, add the SDK dependencies you need. Copy the following Podfile.

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
3. From the Terminal, go to your project folder and install the dependencies with the following command:
```
$ pod update
```
That command installs your dependencies and creates a new Xcode workspace. git **Note**: Ensure that you always open the new Xcode workspace, instead of the original Xcode project file:

	```
	$ open App.xcworkspace
	```
The workspace contains your original project and Pods project that contains your dependencies. If you would like to modify an Bluemix Mobile Services source folder, you can find it in your Pods project, under `Pods/yourImportedSourceFolder`, for example: `Pods/IMFGoogleAuthentication`.

##Using imported frameworks and source folders

Reference the SDK in your code.


### Objective-C

Write #import directives for the relevant headers, for example:

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Note**: Updating your Pods project using the CocoaPods commands `pod install` or `pod update` might override the Bluemix Mobile Services source folders. If you want to retain your customized versions of the original files, ensure that they are backed up before you issue one of these commands.

###Swift

**Pre-requisites**

- iOS 8.0 or greater
- Xcode 7


Write #import directives for the relevant headers, for example:

```
//swift
import BMSCore
import BMSPush
```


##Build Settings

Go to **Xcode > Build Settings > Build Options and Set Enable Bitcode** to **No**.

**Attention**: As of iOS 9, changes to the App Transport Security (ATS) feature might affect the way you handle the authentication process. The following blog posts describe more information about the changes:[ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) and [Connect your iOS 9 app to Bluemix today](https://www.ng.bluemix.net/docs/services/mobilepush/%20https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/%20)
